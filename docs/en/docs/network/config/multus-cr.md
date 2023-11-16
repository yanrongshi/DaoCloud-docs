# Creating a Multus CR

Multus CR management is the secondary encapsulation of configuration instances in Multus CNI by Spiderpool. It aims to provide more flexible network connectivity and configuration options for containers to meet different network requirements and provide users with a simpler and more cost-effective experience. This page explains how to create a Multus CR before using multiple NIC configurations for creating workloads.
If you need to create a new **Multus CR instance**, you can refer to this document.


## Prerequisites

[SpiderPool successfully deployed](../modules/spiderpool/install.md), the new version of SpiderPool includes all the features of Multus-underlay.

## UI Interface Operations

1. After logging in to the DCE UI, click `Container Management` -> `Cluster List` in the left navigation menu to find the corresponding cluster. Then click `Container Network` -> `Network Configuration` on the left navigation menu.

    ![config](../images/networkconfig01.png)

2. Go to `Network Configuration` -> `Multus CR Management`, and click `Create Multus CR`.

    ![Multus CR management](../images/networkconfig02.png)

    !!! note

        When creating a Multus CR, the CNI type can only be one of the following four types: `macvlan`, `ipvlan`, `sriov`, or `custom`. There are three scenarios available.

### Create a Multus CR for macvlan or ipvlan

Enter the following parameters:

![multus cr](../images/networkconfig03.png)

- `Name`: The instance name of the Multus CNI configuration, which is the Multus CR name.
- `Description`: Description of the instance.
- `CNI Type`: The type of CNI. Currently, you can choose between `macvlan` and `ipvlan`.
- `IPv4 Default Pool`: IPv4 default pool in the CNI configuration file.
- `IPv6 Default Pool`: IPv6 default pool in the CNI configuration file.
- `Vlan ID`: Only allowed to be configured when the CNI type is `macvlan`, `ipvlan`, or `sriov`. "0" and "" have the same effect.
- `NIC Configuration`: NIC configuration includes interface configuration information. When the number of NIC interfaces is one, there will only be one NIC interface in the default NIC configuration. When the number of added interfaces is greater than or equal to two, bond-related configuration can be done.
- `NIC Interface`: Only used for `macvlan` and `ipvlan` CNI types, at least one element is required. If there are two or more elements, bond must not be empty.
- `Bond Information`: The name cannot be empty, and the mode must be within the range [0, 6], corresponding to the seven modes:
    - balance-rr
    - active-backup
    - balance-xor
    - broadcast
    - 802.3ad
    - balance-tlb
    - balance-alb

Parameters are optional, and the input format is `k1=v1;k2=v2;k3=v3`, separated by `;`.

#### Vlan Configuration

- The underlay network is the underlying physical network, which usually involves a VLAN network. If the underlay network does not involve a VLAN network, you do not need to configure a `VLAN ID` (the default value is 0).
- **VLAN Subinterfaces**:
    - If the network administrator has already created **VLAN sub-interfaces**, then you do not need to fill in the `VLAN ID` (the default value is 0), you only need to fill in the `NIC Interface` (Master) field with the created **VLAN sub-interfaces**.
    - If you want to create **VLAN sub-interfaces** automatically, you need to configure the `VLAN ID` and set the main `NIC interface` (Master) to the corresponding **parent**. The **sub-interface** named `<master>.<vlanID>` is created dynamically on the host to connect the Pod to the VLAN network.
- **Bond NIC**:
    - If the network administrator has already created a **Bond NIC** and is using the **Bond NIC** to connect to the Pod's Underlay network, there is no need to fill in the `VLAN ID` (the default value of 0 will work). Just fill in the `NIC Interface` (Master) field with the name of the **Bond NIC** that was created.
    - 如果需要自动创建 **Bond 网卡** 而不需要创建 **Vlan 子接口** ，设置 `VLAN ID` 为 `0`，并配置至少 2 个 `网卡接口`(Master)  以组成 `Bond` 的 `Slave` 网卡。Spiderpool 在创建 Pod 时，在主机上动态创建一张 **Bond 网卡**，以用于连接 Pod 的 Underlay 网络。If you need to create a **Bond NIC** automatically without creating a **VLAN sub-interface**, set the `VLAN ID` to `0` and configure at least 2 `NIC interfaces` (Master) to form the `Slave` NIC of the `Bond`. Spiderpool dynamically creates a **Bond NIC** on the host when creating a Pod to connect to the Pod's underlay network.

- **Use the Bond NIC to create VLAN sub-interfaces**：
    - If you need to create a **VLAN sub-interface** to take over the Pod network at the same time as creating a **Bond NIC**, you need to configure a `VLAN ID`. Spiderpool dynamically creates a **VLAN sub-interface** named: `<bondName>. <vlanID>` on the host for connecting to the Pod's VLAN network.
- All interfaces created through Spiderpool are not configured with an IP and they are not persistent. If they are accidentally deleted or the node is restarted, these interfaces will be deleted and automatically recreated after the Pod is restarted. If you need to persist these interfaces or configure IP addresses, consider using [nmcli](https://networkmanager.dev/docs/api/latest/nmcli.html).

### Create a Multus CR for sriov

Enter the following parameters:

![multus cr](../images/networkconfig04.png)

- The `Name`, `Description`, `CNI Type`, `IPv4 Default Pool`, `IPv6 Default Pool`, and `Vlan ID` configurations are the same as in scenario 1.
- `SR-IOV Resource`: Only used for the `sriov` type, enter the resource name, which cannot be empty.

### Create a Custom  Multus CR

![multus cr](../images/networkconfig05.png)

- `JSON`: for custom types, make sure to input a valid JSON file.

After creating it, you can use the Multus CR to manage [workloads](../modules/spiderpool/usage.md).
