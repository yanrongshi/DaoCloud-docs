# Offline Upgrade Backup and Restore Module

This page explains how to install or upgrade the backup and restore module after [downloading it from the Download Center](../../../download/modules/kcoral.md).

!!! info

    The term 'kcoral' used in the following commands or scripts is the internal development code name for the backup and restore module.

## Load Images from Downloaded Package

You can load the images using one of the following two methods. When an image repository exists in the environment, it is recommended to use chart-syncer to synchronize the images to the image repository, as it is more efficient and convenient.

#### Method 1: Use chart-syncer to Synchronize Images

Using chart-syncer, you can upload the charts and their dependent image packages from the downloaded package to the image repository and Helm repository used by the installer.

First, find a node that can connect to the image repository and Helm repository (such as the Spark node), and create a `load-image.yaml` configuration file on the node, filling in the configuration information for the image repository and Helm repository.

1. Create `load-image.yaml` file

    !!! note  

        All parameters in this YAML file are required.

    === "Helm repo already added"

        If the current environment has already installed the chart repo, chart-syncer also supports exporting the chart as a tgz file.

        ```yaml title="load-image.yaml"
        source:
          intermediateBundlesPath: kcoral # Path where the load-image.yaml file is executed on the node.
        target:
          containerRegistry: 10.16.10.111 # Image repository address
          containerRepository: release.daocloud.io/kcoral # Image repository path
          repo:
            kind: HARBOR # Helm Chart repository type
            url: http://10.16.10.111/chartrepo/release.daocloud.io # Helm repository address
            auth:
              username: "admin" # Image repository username
              password: "Harbor12345" # Image repository password
          containers:
            auth:
              username: "admin" # Helm repository username
              password: "Harbor12345" # Helm repository password
        ```

    === "Helm repo not added"

        If the current node does not have a helm repo added, chart-syncer also supports exporting the chart as a tgz file and storing it in the specified path.

        ```yaml title="load-image.yaml"
        source:
          intermediateBundlesPath: kcoral # Path where the load-image.yaml file is executed on the node.
        target:
          containerRegistry: 10.16.10.111 # Image repository URL
          containerRepository: release.daocloud.io/kcoral # Image repository path
          repo:
            kind: LOCAL
            path: ./local-repo # Local path to the chart
          containers:
            auth:
              username: "admin" # Image repository username
              password: "Harbor12345" # Image repository password
        ```

1. Execute the command to synchronize the images.

    ```shell
    charts-syncer sync --config load-image.yaml
    ```

#### Method 2: Load Images using Docker or containerd

Unpack and load the image files.

1. Extract the tar package.

    ```shell
    tar xvf kcoral.bundle.tar
    ```

    After successful extraction, you will get three files:

    - hints.yaml
    - images.tar
    - original-chart

2. Load the images into Docker or containerd from the local directory.

    === "Docker"

        ```shell
        docker load -i images.tar
        ```

    === "containerd"

        ```shell
        ctr image import images.tar
        ```

!!! note

    Each node needs to perform the Docker or containerd image loading operation.
    After loading is complete, tag the images to ensure consistency with the Registry and Repository used during installation.

## Upgrade

There are two upgrade methods. You can choose the appropriate upgrade method based on the preconditions:

=== "Upgrade via Helm Repo"

    1. Check if the backup and restore Helm repository exists.

        ```shell
        helm repo list | grep kcoral
        ```

        If the result is empty or shows the following prompt, proceed to the next step. Otherwise, skip the next step.

        ```none
        Error: no repositories to show
        ```

    1. Add the backup and restore Helm repository.

        ```shell
        heml repo add kcoral http://{harbor url}/chartrepo/{project}
        ```

    1. Update the backup and restore Helm repository.

        ```shell
        helm repo update kcoral
        ```

    1. Select the backup and restore version you want to install (it is recommended to install the latest version version).

        ```shell
        helm search repo kcoral/kcoral --versions
        ```

        ```none
        [root@master ~]# helm search repo kcoral/kcoral --versions
        NAME                   CHART VERSION  APP VERSION  DESCRIPTION
        kcoral/kcoral  0.20.0          v0.20.0       A Helm chart for kcoral
        ...
        ```

    1. Backup the `--set` parameters.

        Before upgrading the backup and restore version, it is recommended to run the following command to back up the `--set` parameters of the old version.

        ```shell
        helm get values kcoral -n kcoral-system -o yaml > bak.yaml
        ```

    1. Update kcoral crds

        ```shell
        helm pull kcoral/kcoral --version 0.5.0 && tar -zxf kcoral-0.5.0.tgz
        kubectl apply -f kcoral/crds
        ```

    1. Execute `helm upgrade`.

        Before upgrading, it is recommended to replace the `global.imageRegistry` field in the `bak.yaml` file with the image repository address you are currently using.

        ```shell
        export imageRegistry={your image repository}
        ```

        ```shell
        helm upgrade kcoral kcoral/kcoral \
          -n kcoral-system \
          -f ./bak.yaml \
          --set global.imageRegistry=$imageRegistry \
          --version 0.5.0
        ```

=== "Upgrade via Chart Package"

    1. Backup the `--set` parameters.

        Before upgrading the backup and restore version, it is recommended to run the following command to back up the `--set` parameters of the old version.

        ```shell
        helm get values kcoral -n k pan da-system -o yaml > bak.yaml
        ```

    1. Update kcoral crds

        ```shell
        kubectl apply -f ./crds
        ```

    1. Execute `helm upgrade`.

        Before upgrading, it is recommended to replace the `global.imageRegistry` in the `bak.yaml` file with the image repository address you are currently using.

        ```shell
        export imageRegistry={your image repository}
        ```

        ```shell
        helm upgrade kcoral . \
          -n kcoral-system \
          -f ./bak.yaml \
          --set global.imageRegistry=$imageRegistry
        ```
