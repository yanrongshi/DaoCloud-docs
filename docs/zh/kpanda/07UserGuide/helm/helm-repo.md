# 管理 Helm 仓库

Helm 仓库是 Helm 组件中用来存储和发布 Chart 的存储库。
Helm 应用模块支持通过 HTTP(s) 协议来访问存储库中的 Chart 包。
系统默认内置了如下表所示的 4 个 Helm 仓库用来满足企业生产过程中的常见需求。

| 仓库      | 描述                                                         | 示例  |
| --------- | ------------------------------------------------------------ | ------------ |
| partner   | 由生态合作伙伴所提供的各类优质特色 Chart                     | tidb         |
| system    | 系统核心功能组件及部分高级功能所必需依赖的 Chart，发行版中默认安装。如必需安装 insight-agent 才能够获取集群的监控信息 | Insight      |
| addon     | 业务场景中常见的 Chart                                       | cert-manager |
| community | Kubernetes 社区较为热门的开源组件 Chart                      | Istio        |

除了上述系统提供的 Chart，您也可以通过界面操作，添加第三方 Helm 仓库。本文将介绍如何添加、更新第三方 Helm 仓库。

## 前提条件

- 容器管理平台[已接入 Kubernetes 集群](../Clusters/JoinACluster.md)或者[已创建 Kubernetes](../Clusters/CreateCluster.md)，且能够访问集群的 UI 界面

- 已完成一个[命名空间的创建](../Namespaces/createns.md)、[用户的创建](../../../ghippo/04UserGuide/01UserandAccess/User.md)，并将用户授权为 [`NS Admin`](../Permissions/PermissionBrief.md#ns-admin) 角色 ，详情可参考[命名空间授权](../Permissions/Cluster-NSAuth.md)。

- 如果使用私有仓库，当前操作用户应拥有对此仓库的读写权限。

## 引入第三方 Helm 仓库

本节将以 Kubevela 公开的镜像仓库为例，引入 Helm 仓库并管理。

1. 点击一个集群名称，进入`集群详情`。

    ![ns](../../images/crd01.png)

2. 在左侧导航栏，依次点击 `Helm 应用` -> `Helm 仓库`，进入 Helm 仓库页面。

    ![helm-repo](../../images/helmrepo01.png)

3. 在 Helm 仓库页面点击`创建仓库`按钮，进入创建仓库页面，按照下表配置相关参数。

    - 仓库名称：设置新接入的仓库名称。最长 63 个字符，只能包含小写字母、数字及分隔符 `_`，且必须以小写字母或数字开头及结尾，例如 kubevela
    - 仓库地址：用来指向目标 Helm 仓库的 http（s）地址。例如 https://charts.kubevela.net/core
    - 认证方式：连接仓库地址后用来进行身份校验的方式。对于公开仓库，可以选择 `None`，私有的仓库需要输入用户名/密码以进行身份校验。
    - 标签：为即将创建的 Helm 仓库添加标签。例如 key: repo4；value: Kubevela
    - 注解：为即将创建的 Helm 仓库添加注解。例如 key: repo4；value: Kubevela
    - 描述：为即将创建的 Helm 仓库添加描述。例如：这是一个 Kubevela 公开 Helm 仓库

    ![helm-repo](../../images/helmrepo02.png)

4. 点击`确定`，完成 Helm 仓库的创建。将自动跳转至 Helm 仓库列表。

    ![helm-repo](../../images/helmrepo03.png)

## 更新第三方 Helm 仓库

当 Helm 仓库的地址信息发生变化时，可以通过更新操作来完成对 Helm 仓库的地址及认证方式的更新，也可以对 Helm 仓库的标签、注解及描述信息进行修改。

1. 点击一个集群名称，进入`集群详情`。

    ![ns](../../images/crd01.png)

2. 在左侧导航栏，依次点击`Helm 应用` -> `Helm 仓库`，进入 Helm 仓库列表页面。

    ![helm-repo](../../images/helmrepo01.png)

3. 在仓库列表页面找到需要更新的 Helm 仓库，在列表右侧点击 `⋮` 按钮，在弹出菜单中点击`更新`。

    ![helm-repo](../../images/helmrepo04.png)

4. 在`编辑 Helm 仓库`页面，完成对 Helm 仓库的更新后点击`确定`。

    ![helm-repo](../../images/helmrepo05.png)

5. 返回 Helm 仓库列表，屏幕提示更新成功。