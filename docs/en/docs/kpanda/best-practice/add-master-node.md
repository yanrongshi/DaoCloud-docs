# Scaling Controller Nodes in a Worker Cluster

This article provides a step-by-step guide on how to manually scale the control nodes in a worker cluster to achieve high availability for self-built clusters.

!!! note

    It is recommended to enable high availability mode when creating the worker cluster in the interface. Manually scaling the control nodes of the worker cluster involves certain operational risks, so please proceed with caution.

## Prerequisites

- A worker cluster has been created using the DCE 5.0 platform. You can refer to the documentation on [Creating a Worker Cluster](../user-guide/clusters/create-cluster.md).
- The managed cluster associated with the worker cluster exists in the current platform and is running normally.

!!! note

    Managed cluster refers to the cluster specified during the creation of the worker cluster, which provides capabilities such as Kubernetes version upgrades, node scaling, uninstallation, and operation records for the current cluster.

## Modifying the Host manifest

1. Log in to the container management platform and go to the overview page of the cluster where you want to scale the control nodes. In the `Basic Information` section, locate the **Managed Cluster** of the current cluster and click its name to enter the overview page.


2. In the overview page of the managed cluster, click **Console** to open the cloud terminal console. Run the following command to find the host manifest of the worker cluster that needs to be scaled.

    ```bash
    kubectl get cm -n kubean-system ${ClusterName}-hosts-conf -oyaml
    ```
    "${ClusterName}" is the name of the worker cluster to be scaled.


3. In the host manifest, add the information of the control nodes to be added. Make the necessary modifications and save the file.

!!! "Sample Host manifest"

    === "Before adding nodes"

        ``` yaml
        apiVersion: v1
        kind: ConfigMap
        metadata:
          name: tanghai-dev-hosts-conf
          namespace: kubean-system
        data:
          hosts.yml: |
            all:
              hosts:
                node1:
                  ip: 10.6.175.10 
                  access_ip: 10.6.175.10
                  ansible_host: 10.6.175.10 
                  ansible_connection: ssh
                  ansible_user: root
                  ansible_password: password01
              children:
                kube_control_plane:
                  hosts:
                    node1:
                kube_node:
                  hosts:
                    node1:
                etcd:
                  hosts:
                    node1:
                k8s_cluster:
                  children:
                    kube_control_plane:
                    kube_node:
                calico_rr:
                  hosts: {}
        ......
        ```

    === "After adding nodes"

        ``` yaml
        apiVersion: v1
        kind: ConfigMap
        metadata:
          name: tanghai-dev-hosts-conf
          namespace: kubean-system
        data:
          hosts.yml: |
            all:
              hosts:
                node1:
                  ip: 10.6.175.10
                  access_ip: 10.6.175.10 
                  ansible_host: 10.6.175.10
                  ansible_connection: ssh
                  ansible_user: root
                  ansible_password: password01
                node2: # Add controller node2
                  ip: 10.6.175.20
                  access_ip: 10.6.175.20
                  ansible_host: 10.6.175.20
                  ansible_connection: ssh
                  ansible_user: root
                  ansible_password: password01
                node3:
                  ip: 10.6.175.30 
                  access_ip: 10.6.175.30
                  ansible_host: 10.6.175.30 
                  ansible_connection: ssh
                  ansible_user: root
                  ansible_password: password01
              children:
                kube_control_plane:
                  hosts:
                    node1:
                    node2: # Add controller node2 
                    node3: # Add controller node3
                kube_node:
                  hosts:
                    node1:
                    node2: # Add controller node2
                    node3: # Add controller node3
                etcd:
                  hosts:
                    node1:
                    node2: # Add controller node2
                    node3: # Add controller node3
                k8s_cluster:
                  children:
                    kube_control_plane:
                    kube_node:
                calico_rr:
                  hosts: {}
        ```

**Important Parameters:**

>* `all.hosts.node1`: Existing master node in the original cluster
>* `all.hosts.node2`, `all.hosts.node3`: Control nodes to be added during cluster scaling
>* `all.children.kube_control_plane.hosts`: Control plane group in the cluster
>* `all.children.kube_node.hosts`: Worker node group in the cluster
>* `all.children.etcd.hosts`: ETCD node group in the cluster

## Adding a Cluster Expansion Task "scale-master-node-ops.yaml" using the ClusterOperation.yml Template

Use the following ClusterOperation.yml template to add a cluster control node expansion task called "scale-master-node-ops.yaml". 

```yaml title="ClusterOperation.yml"
apiVersion: kubean.io/v1alpha1
kind: ClusterOperation
metadata:
  name: cluster1-online-install-ops
spec:
  cluster: ${cluster-name} # Specify cluster name
  image: ghcr.m.daocloud.io/kubean-io/spray-job:v0.4.6 # Specify the image for the kubean job
  backoffLimit: 0
  actionType: playbook
  action: cluster.yml
  extraArgs: --limit=etcd,kube_control_plane -e ignore_assert_errors=yes
  preHook:
    - actionType: playbook
      action: ping.yml
    - actionType: playbook
      action: disable-firewalld.yml
  postHook:
    - actionType: playbook
      action: upgrade-cluster.yml
      extraArgs: --limit=etcd,kube_control_plane -e ignore_assert_errors=yes
    - actionType: playbook
      action: kubeconfig.yml
    - actionType: playbook
      action: cluster-info.yml
```

!!! note

    - Ensure that the spec.image URL matches the image used in the previous deployment job.
    - Set spec.action to scale.yml.
    - Set spec.extraArgs to --limit=g-worker.
    - In spec.preHook, make sure to provide the correct repo_list parameter for the enable-repo.yml playbook based on the OS.
    - If adding more than three master (etcd) nodes at once, include the additional parameter -e etcd_retries=10 to increase the number of retries for etcd node join.

Create and deploy scale-master-node-ops.yaml based on the above configuration.

```bash
# Copy the above manifest

vi cale-master-node-ops.yaml

kubectl apply -f cale-master-node-ops.yaml -n kubean-system
```

Perform the following command to verify it.

```bash
kubectl get node
```
