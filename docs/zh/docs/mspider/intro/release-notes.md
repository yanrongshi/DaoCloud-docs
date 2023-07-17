# 服务网格 Release Notes

本页列出服务网格各版本的 Release Notes，便于您了解各版本的演进路径和特性变化。

## 2023-06-29

### v0.17.0

#### 升级

- **新增** 新增 `mspider.io/mesh-gateway-name` Label 规范，用于定义网格网关名称。
- **新增** 命名空间新增字段 `injectionStatus`，用于列表搜索。
- **新增** 在拓扑查询中，新增字段 `label_selectors`,条件查询拓扑结果。
- **新增** 边车工作负载信息新增字段 `Labels` 和 `PodLabels`。
- **新增** 服务工作负载信息新增字段 `Labels` 和 `PodLabels`。
- **新增** 集群信息新增组件信息（components）与 Istio 版本（meshVersion）字段。
- **新增** 集群列表与网格管理集群列表新增 `include_components` 字段，用于选择是否需要展示集群组件信息，例如 Insight 等外部组件。
- **新增** 为所有需要的接口，增加审计信息。
- **新增** 工作负载注入策略清除策略操作。
- **新增** 命名空间列表新增索引搜索实现。
- **新增** 审计日志能力。
- **新增** 工作负载注入策略清除能力。
- **新增** 集群列表新增组件状态实现。
- **新增** 新增 `mspider.io/mesh-gateway-name` Label 规范，用于定义网关网关名称。
- **新增** `MCPC Controller` 实现纳管服务自动注入能力。
- **新增** Ghippo 资源上报功能，按照规范自动创建并且更新 `GProductResource` 资源。
- **新增** `MCPC Controller` 新增配置 `global.config.enableAutoInitPolicies`，用于是否开启纳管服务自动初始化治理策略。
- **新增** `MCPC Controller` 新增配置 `global.config.enableAutoInjectedSidecar`，用于是否开启纳管服务自动注入策略。
- **新增** K8s 各版本兼容性测试。
- **优化** 新增 cache 优化查询集群 `Insight Agent` 状态接口过慢问题。
- **优化** 网格创建时对托管集群检测加强，避免创建冲突网格。
- **优化** 网格网关更新操作将忽略名称 (Name)、命名空间 (Namespace)、标签 (Labels) 更新，避免更新触发异常。
- **优化** Kpanda 集群 kubeconfig 同步方式。
- **优化** `WorkloadShadow controller watcher` 创建逻辑。
- **升级** 支持查询集群与集群组件，允许不传 MeshID，独立获取信息。
- **升级** go package istio.io/istio 到 `v0.0.0-20230131034922-50fb2905d9f5` 版本。
- **升级** CloudTTY 到 `v0.5.3` 版本。
- **升级** 前端版本至 `v0.15.0` 版本。

#### 修复

- **修复** 创建集群东西网关的审计日志描述不准确的问题。
- **修复** 东西网关副本数不生效问题。
- **修复** 网格删除检测边车部分无效。
- **修复** 监控拓扑无法筛选命名空间。
- **修复** 监控拓扑服务错误率数据不准确问题。
- **修复** 修复网格不存在时应该返回 404 错误。
- **修复** Audit 存在 `nil pointer` 导致 panic 的问题。
- **修复** 审计日志中，Enum 类型的资源类型显示为数字的问题。
- **修复** GRPC 请求带用户认证信息时，行为和 HTTP 请求不一致的情况。
- **修复** 创建专有网格时，`Telemetry` 资源没有被正确创建。
- **修复** `RegProxy watcher` 不重建。
- **修复** `traffic-lane` 插件会给流量打上错误的标签，导致流量泳道无法工作。
- **修复** 删除网格时，没有正确清理集群配置。
- **修复** `MCPC Controller` 接入不健康集群，运行不正常的问题。
- **修复** 修复网格删除或者移除集群过程中，无法正常移除组件问题。
- **修复** GlobalMesh 和 MeshCluster 一直处于删除状态，无法强制删除的逻辑。
- **修复** 默认不注入的系统命名空间注入状态不正确的问题。
- **修复** 代理 `HostedAPIServe`r 的时候，选择到了没就绪的 Pod，导致网格无法就绪。
- **修复** 网格删除时，Telemetry 删除失败导致网格删除流程失败的问题。因该资源在卸载 Istio / 移除 `Hosted ApiServer` 时会被清理，所以不需要在删除网格流程中进行删除。
- **修复** `HostedAPIServer` 因为权限问题无法再 OCP 上安装的问题。
- **修复** helm chart 中的描述信息。

#### 移除

- **移除** 托管网格模式下，`istiod-[meshID]-hosted-lb` 服务中 443 端口。

## 2023-05-31

### v0.16.2

#### 升级

- **新增** Ckube 按需加载资源。
- **新增** IstioResource 字段：`labels` 与 `annotations`，能够更新 Label 与 Annotation。
- **新增** MeshCluster 中 ClusterProvider 同步实现。
- **新增** `mspider.io/protected` Label 定义，用于网格保护能力。
- **新增** 边车升级支持多工作负载能力，`SidecarUpgrader` 中 `workloads` 同时支持 `workloadshadow.name` 和 `deployment.name`。
- **新增** 工作负载类型改造成 string 实现。
- **新增** 工作负载相关接口新增字段 `localized_name`，展示工作负载名称。
- **新增** 工作负载注入策略清除能力
- **新增** 获取全局配置接口 `/apis/mspider.io/v3alpha1/settings/global-configs`。
- **新增** `clusterPhase` 字段，用于标记集群的状态（以前在 phase 字段中标记，现在剥离开）。
- **新增** `clusterProvider` 字段，用于标记集群提供商。
- **新增** 流量泳道 CRD 能力实现。
- **新增** 默认启用 Reg-Proxy 组件。
- **新增** 实现 Service 的 selector 字段输出。
- **新增** 通过给 Namespace 加 Network label 解决未注入 Sidecar 跨集群访问问题。
- **新增** 托管网格 hosted-apiserver 自定义参数配置能力。(该参数只有安装时生效，暂时不支持更新)，(更多参数请参考 helm 参数配置)：
- **新增** 网格控制面组件状态
- **新增** 网格网格查询接口新增 `loadBalancerStatus` 字段，用于描述实际分配的 LB 地址。
- **新增** 网格组件进度详情接口 `/apis/mspider.io/v3alpha1/meshes/{mesh_id}/components-progress`。
- **新增** 为控制面组件增加 HPA。
- **新增** 新增获取集群 `StorageClass` 接口定义。
- **新增** 新增获取集群安装组件接口（目前支持 Insight Agent）。
- **优化** 绑定/解绑工作空间的使用体验。
- **优化** 工作负载相关接口字段 `workload_kind` 类型从枚举优化为 `string`。
- **优化** 托管网格情况下，对于集群 k8s 版本检测：除包含工作集群外，也包含对控制面集群的版本检测。
- **升级** 升级 CloudTTY 到 `0.5.3` 版本。
- **升级** WorkloadShadow controller watcher 创建逻辑。

#### 修复

- **修复** `helm chart` 中的描述信息
- **修复** RegProxy watcher 不重建。
- **修复** `traffic-lane` 插件会给流量打上错误的标签，导致流量泳道无法工作。
- **修复** 修复网格删除或者移除集群过程中，无法正常移除组件问题。
- **修复** 修复网格不存在时应该返回 404 错误。
- **修复** CloudShell 权限问题。
- **修复** MeshCluster Status RemotePilotAddress 无效数据没有及时清理。
- **修复** MeshCluster 无法被删除的问题。
- **修复** TrafficLane 的 FailedReason 中缺失内容。
- **修复** TrafficLaneActionsRequest 中的 action 字段缺失。
- **修复** 当存在不健康集群时，网格列表无法展示的问题。
- **修复** 当实例异常时，有效注入实例数不正确。
- **修复** 当一个服务被多个泳道选择时，WasmPlugin 无法创建多个的问题。
- **修复** 服务标签可能存在残留旧的工作负载。
- **修复** 服务列表无法获取工作负载有效的工作负载数，动态获取 ReadyReplicas 的类型解析错误。
- **修复** 工作负载发生变更时，无法将变更的状态同步到对应的 Service。
- **修复** 会对未接入网格的集群一直检查状态的问题。
- **修复** 集群状态不可搜索。
- **修复** 没有边车时，网格无法移除集群的情况。
- **修复** 网格名称正则表达式，不允许数字开头。
- **修复** 网格状态显示不正确，没有边车时有时仍然显示状态为正常。
- **修复** 修复网格网格的自动注入的模板不生效问题。
- **修复** 由于集群缺少默认值，导致非 Admin 用户无法获取流量拓扑。
- **修复** 自动注入服务策略空指针异常。

## 2023-04-27

### v0.15.0

#### 升级

- **新增** 引入 d2 作为绘图工具
- **新增** 一个新的 wasm 插件，用于根据 trace id，给请求加上不同的 header。
- **新增** 网格配置托管 Istiod 的 LoadBalancer Annotations 实现
- **新增** 网格网关配置服务 Annotations 实现
- **新增** 增加网格字段 load_balancer_annotations，支持自定义负载均衡 Annotations
- **新增** 在 mspider-api 中，手动执行 pipeline，设置 SYNC_OPENAPI_DOCS 为 key，既可触发上传文档站（提 PR）
- **新增** MCPC Controller 感知到 Service 的中存在 mspider.io/managed 的标签时，将触发自动创建该服务对应的治理策略。
- **新增** MCPC Controller 多工作负载类型支持。
- **新增** 健康检查功能，当某个网格 APIServer 代理出现无法连通的情况时，自动重建该代理，
  防止 PortForward 自身逻辑不可靠（可能和 Istio Sidecar 有关）

#### 修复

- **修复** 未兼容 grpcgateway-accept-language（等价与 HTTP 的 Accept-Language）Header，导致无法正确切换中英文模式模式。
  当前同时兼容 Accept 与 Accept-Language 两种模式
- **修复** 同步 OpenAPI 时，由于 shadow clone 代码导致 upstream 无法 push 的问题
- **修复** 无法更新带 `.` 的 Istio 资源
- **修复** 在 1.17.1 版本中，istio-proxy 无法正常启动的问题
- **修复** ingress gateway 缺少 name 导致 merge 失败无法部署的问题
- **修复** 服务地址无法搜索的问题
- **修复** 无法更新带 `.` 的 Istio 资源 的问题
- **修复** 之前 controller 内存泄漏的问题。
- **修复** add/delete cluster 有时没有正确触发的逻辑。
- **修复** 了托管模式下 istio-system 可能被误删的情况。
- **修复** ingress gateway 缺少 name 导致 merge 失败无法部署的问题。
- **修复** 在开启全局注入情况下，更新网格可能导致 istio-operator pod 被注入，从而使网格创建失败的问题
- **修复** 服务与 WorkloadShadow 关联的两个部分没有清理逻辑，导致服务被错误绑定在工作负载上
- **修复** 一个导致虚拟集群被同步到 Mspider 导致接入失败的问题
- **优化** controller 命名空间、服务资源处理逻辑，减少频繁触发 workloadShadow 资源更新。
- **优化** workloadShadow 资源频繁获取/更新的问题，现在只对某些发生特定改变的资源进行 reconcile。
- **优化** 减少 pod 变更不断更新 WorkloadShadow
- **修复** relok8s 中 wasm 插件镜像地址拼写错误的问题。
- **修复** TrafficLane 默认 repository 错误。
- **优化** Helm 镜像渲染模板。镜像结构拆分为三个部分：registry/repository:tag

#### 移除

- **移除** 同步全局集群到网格的逻辑
- **弃用** 弃用 Deployment Controller 的逻辑
- **弃用** ui.version 参数，改为 ui.image.tag 参数设定前端版本

## 2023-03-31

### v0.14.3

#### 升级

- **升级** 前端版本至 v0.12.2

#### 修复

- **修复** 无法更新带 `.` 的 Istio 资源
- **修复** 在 1.17.1 版本中，istio-proxy 无法正常启动的问题
- **修复** ingress gateway 缺少 name 导致 merge 失败无法部署的问题。

## 2023-03-30

### v0.14.0

#### 新功能

- **新增** CloudShell 相关接口定义
- **新增** 更新服务的标签实现
- **新增** 服务列表和详情会返回 labels
- **新增** CloudShell 相关实现
- **新增** 服务列表支持对服务标签的查询
- **新增** 一个新的 API，用于更新服务的标签
- **新增** istio 1.17.1 支持
- **新增** 一个新的 etcd 高可用方案
- **新增** 场景化测试框架，用于测试场景化的功能
- **新增** 选择不同网格规模时，自动调整组件资源配置
- **新增** 自定义角色的实现，支持自定义角色的创建、更新、删除、绑定、解绑等操作

#### 优化

- **优化** mcpc controller 启动逻辑，避免出现工作集群没有正确注册的情况
- **优化** WorkloadShadow 清理逻辑：由定时触发改造事件触发：控制器启动时、检测到工作集群发生变化时；
  WorkloadShadow 发生变化时，自健康检测，对应工作负载不存在时，触发清理逻辑
- **优化** mcpc controller 启动逻辑，避免出现工作集群没有正确注册的情况
- **升级** Insight api 升级到 v0.14.7 版本
- **升级** ckube 支持 labels 的复杂条件查询
- **移除** 移除 Helm 升级时间限制

#### 修复

- **修复** 东西网关没 Ready 时界面无显示的问题
- **修复** 多云互联会自动注册东西网关 LB IP，可能导致内部网络异常（移除东西网关实例 label：topology.istio.io/network，该标签会将东西网关自动注册）
- **修复** 携带东西网关的集群迁移会出错问题（无法修改实例的 label，如果需要修改组件 label 只能删除组件再重建）
- **修复** 了一个导致 Mesh 绑定 workspace 服务失败（界面显示成功）的问题
- **修复** 由于异常导致虚拟集群中存在游离的命名空间，在启动 mcpc-controller 时增加自检并且清除行为
- **修复** 由于 controller 更新网格，导致 api 下发网格配置失败
- **修复** 创建托管网格时，ServicePort 的 TargetPort 未正确设置的问题
- **修复** GlobalMesh.Status.MeshVersion 错误覆盖问题
- **修复** mcpc-controller 无法开启 debug 模式问题
- **修复** mcpc-controller 无法触发集群删除事件
- **修复** 删除 Mesh 再重建同名的 Mesh 时，会导致 Mesh 无法正常创建的问题（hosted proxy 无法正常更新）
- **修复** mcpc controller 在某些情况下没有正确修改 istiod-remote 的 service 的问题

## 2023-02-28

### v0.13.1

#### 新功能

- **新增** 多云网络互联管理及相关接口
- **新增** 网格全局配置能力（网格系统配置、全局流量治理能力、全局边车注入设置）增强
- **新增** 支持 zookeeper 代理

#### 优化

- **优化** Namespace 控制器加上 Cache，当集群中 Namespace 过多时会造成太多的重复的 Get 请求
- **优化** 减少正常模式下 ckube 的日志输出

#### 修复

- **修复** 由容器管理平台移除集群导致的网格相关逻辑错误
- **修复** RegProxy 注入 Sidecar 会导致 Nacos 无法注册的问题
- **修复** Spring Cloud 服务识别错误的问题
- **修复** 没有同步容器管理平台 Cluster 状态信息
- **修复** 流量透传策略 - 流量筛选 IP 段配置未生效
- **修复** 流量透传策略 - 流量透传策略无法删除
- **修复** 获取网格配置时，由于配置路径不存在导致返回错误

## 2022-12-29

### v0.12.0

#### 新功能

- **新增** 流量透传功能的接口实现
- **新增** 对 istio 1.15.4、1.16.1 的支持

#### 优化

- **优化** 命名空间边车管理页面中增加“未设置”边车策略，避免命名空间层面的边车策略对工作负载层面产生连带影响；
- **优化** 发布流水线参数
- **优化** 边车注入、边车资源限制逻辑、避免出现不同步现象

#### 修复

- **修复** 网格升级后部分组件未更新的问题
- **修复** 网格移除后部分资源未清除的问题 - 边车资源同步不正确，改为通过 Pod 中的 istio-proxy 容器的实际边车资源
- **修复** 托管集群无法作为工作集群
- **修复** 当边车注入实例为 0/0 时注入情况显示不正确
- **修复** 取消边车注入后仍然显示边车相关信息

## 2022-11-30

### v0.11.1

#### 新功能

- **新增** `密钥管理`相关 API
- **新增** 在`虚拟服务`、`目标规则`、`网关规则`列表
- **新增**治理策略标签及相关筛选能力
- **新增** 网格中集群健康状态检查能力
- **新增** otel sdk 接入
- **新增** secret 的多个接口实现
- **新增** 对 istio 1.15.3 的支持

#### 优化

- **优化** 重工作负载边车注入接口，防止出现问题
- **优化** 网格服务监控面板默认展开
- **优化** 禁用网格全局监控面板子链接跳转，避免出现界面混乱现象
- **优化** 网格控制面处理流程，避免更新已经更新过的 object 导致冲突
- **优化** 网格的集群接入、移除逻辑

#### 修复

- **修复** 当控制面 MSpider 升级之后，mcpc 等组件未更新的问题
- **修复** 获取集群资源错误
- **修复** 获取集群命名空间列表接口集群名称不存在时响应码为 200 情况
- **修复** 网格升级流程中前置条件判断有误的问题
- **修复** 网格升级未执行 k8s 版本限制的问题
- **修复** 边车管理接口工作负载边车资源配置失效的问题
- **修复** 因网格内集群的监控检测失败导致集群无法移除的问题
- **修复** 数据面的镜像没有被打包到 DCE 5.0 的离线包中
- **修复** Ckube 无法自动更新配置的问题
