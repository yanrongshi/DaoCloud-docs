# Istio 资源管理

`Istio 资源管理`页面按资源类型列出了 Istio 的主要资源文件，为用户提供了各类资源的展示、创建等功能。

![img](../../images/istio01.png)

本页面提供了以下几种资源类型：

### 流量治理类

| **资源类型**                | **描述**                                                     |
| --------------------------- | ------------------------------------------------------------ |
| DestinationRule（目标规则） | 目标规则是服务治理中重要的组成部分，目标规则通过端口、服务版本等方式对请求流量进行划分，并对各请求分流量订制envoy流量策略，应用到流量的策略不仅有负载均衡，还有最小连接数、熔断等。 |
| EnvoyFilter                 | 该资源提供了对 envoy 配置的能力，可以定义新的过滤器、监听器\集群等。使用该资源时需谨慎，错误配置可能会对整个网格环境的稳定性造成较大影响。  注意：  -EnvoyFilter  可以配置在Istio根目录（对所有工作负载生效）或某个工作负载（使用工作负载选择标签）；  -当多个 EnvoyFilter 作用于同一个工作负载时，会按创建顺序优先执行； |
| Gateway（网关规则）         | 网关规则用于定义网格边缘的负载均衡器，用于将服务暴露于网格之外，或提供内部服务的对外访问。相较于k8s的ingress对象，istio的网关规则增加了更多的功能：  l L4-L6负载均衡  l 对外mTLS  l SNI的支持  l 其他istio中已经实现的内部网络功能： Fault  Injection，Traffic Shifting， Circuit Breaking， Mirroring  对于L7的支持，网关规则通过与虚拟服务配合实现。 |
| ProxyConfig                 | 用于暴露代理的配置选项，例如：代理的线程数。该资源为可选资源，如不创建，系统将使用内建默认值；  注意：  -ProxyConfig  中任何配置变更需要重启相关工作负载才会生效；  -作用于网格或命名空间的 ProxyConfig 不可以包含任何工作负载选择标签，否则将仅作用于选定的工作负载； |
| WorkloadEntry               | 该资源提供了对非k8s标准工作负载的描述，例如：运行于虚拟机的工作负载。WorkloadEntry需要与服务条目配合使用，由服务条目通过筛选器建立服务与工作负载之间的对应关系； |
| ServiceEntry（服务条目）    | 服务条目允许向Istio的内部服务注册表中添加其他条目，以便网格中自动发现的服务可以访问/路由到这些手动指定的服务。服务条目描述服务的属性包括：DNS名称、VIP、端口、协议、端点等。这些服务可以是网格外部的（例如：web API）或网格内部无法自动注册的服务（例如：一个数据库，几个VM）。 |
| SideCar                     | Sidecar用于描述边车对工作负载实例之间的流量转发配置。默认情况下，Istio将支持转发网格中所有工作负载实例之间的通信，并接受与工作负载相关的所有端口流量。  注意：  -根命名空间下的 SideCar 对所有没有配置 SideCar 的命名空间及工作负载生效；  -任意命名空间或工作负载如果存在多个 SideCar，将被定义为行为未定义（无生效资源）； |
| VirtualService（虚拟服务）  | 在虚拟服务中，提供了HTTP、TCP、TLS三种协议的路由支持，可以通过多种匹配方式（端口、host、header等）实现对不同的地域、用户请求做路由转发，分发至特定的服务版本中，按权重比划分负载，并提供了故障注入、流量镜像等多种治理工具。 |
| WorkloadGroup               | WorkloadGroup  描述了工作负载实例的集合，定义了工作负载实例引导代理的规范细节，包括元数据和标识。WorkloadGroup 仅用于非 k8s 工作负载，模拟k8s中边车注入和部署方式，引导Istio代理， |

### 安全治理类

| **资源类型**                          | **描述**                                                     |
| ------------------------------------- | ------------------------------------------------------------ |
| AuthorizationPolicy（授权策略）       | 授权策略类似于一种四层到七层的“防火墙”，它会像传统防火墙一样，对数据流进行分析和匹配，然后执行相应的动作。无论是来自外部的请求，或是网格内服务间的请求，都适用授权策略。 |
| PeerAuthentication（对等身份认证）    | 对等身份认证提供服务间的双向安全认证，同时密钥以及证书的创建、分发、轮转也都由系统自动完成，对用户透明，从而大大降低了安全配置管理的复杂度。 |
| RequestAuthentication（请求身份认证） | 请求身份认证用于外部用户对网格内部服务发起请求的认证，用户使用jwt实现请求加密；每个请求身份认证需要配置一个授权策略 |

### 代理扩展类

| **资源类型** | **描述**                                                     |
| ------------ | ------------------------------------------------------------ |
| WasmPlugin   | WasmPlugin  通过WebAssembly过滤器为Istio代理提供扩展功能，其提供的过滤器能力可以和Istio内部过滤器形成复杂交互关系。 |

### 系统设置类

| **资源类型** | **描述**                                                     |
| ------------ | ------------------------------------------------------------ |
| Telementry   | 该资源定义了如何为网格内的工作负载生成遥测，为Istio提供了指标、日志、全链路追踪三项可观测性工具的配置。  注意：创建在Istio根目录并且不包含工作负载选择器的遥测资源将对网格全局生效。 |

## UI 操作示例

用户可以用 YAML 形式对资源进行增删改查操作。此处是一个 telementry 遥测资源的创建/删除示例。

1. 在左侧导航栏中点击`网格配置` -> `Istio 资源管理`，点击右上角的 `YAML 创建`按钮。

    ![img](../../images/istio01.png)

2. 在 YAML 创建页面中，输入正确的 YAML 语句后点击`确定`。

    ![img](../../images/istio02.png)

    ```yaml
    apiVersion: telemetry.istio.io/v1alpha1
    kind: Telemetry
    metadata:
    name: namespace-metrics
    namespace: default
    spec:
    # 未指定选择算符，应用到命名空间中的所有工作负载
    metrics:
    - providers:
        - name: prometheus
        overrides:
        - tagOverrides:
    ​        request_method:
    ​          value: "request.method"
    ​        request_host:
    ​          value: "request.host"
    ```

3. 返回资源列表，点击操作一列的 `⋮` 按钮，可以从弹出菜单中选择编辑和删除等更多操作。

    ![img](../../images/istio03.png)