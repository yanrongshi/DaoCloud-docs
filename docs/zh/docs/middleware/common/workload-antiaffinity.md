# 工作负载反亲和性

创建[Elasticsearch 搜索服务](../elasticsearch/intro/what.md)、[Kafka 消息队列](../kafka/intro/what.md)、[MinIO 对象存储](../minio/intro/what.md)、[MySQL 数据库](../mysql/intro/what.md)、[RabbitMQ 消息队列](../rabbitmq/intro/what.md)、[PostgreSQL 数据库](../postgresql/intro/what.md)、[Redis 缓存服务](../redis/intro/what.md)或 [MongoDB 数据库](../mongodb/intro/what.md)实例时，可以在服务设置页面配置工作负载反亲和性。

工作负载反亲和性的作用原理是，在一定的拓扑域（作用域）范围内，如果检测到已经有工作负载带有反亲和性配置中添加的某个标签，则不会将新建的工作负载部署到该拓扑域。这样做的好处是：

- 性能优化

    通过工作负载反亲和性，将实例的多个副本部署到不同的节点/可用区/区域，避免副本间的资源竞争，确保每个副本都有充足的可用资源，从而提供应用的性能和可靠性。

- 故障隔离

    实例副本分布在不同的节点/可用区/区域，有效避免了单点故障问题。某个环境中的副本出现故障时，其他环境中的副本不受影响，从而保障服务整体的可用性。

## 操作步骤

下面以 `Redis` 为例，介绍如何设置`工作负载反亲和性`。

!!! note

    本文侧重介绍如何配置`工作负载反亲和性`。如需了解详细的 `Redis` 实例创建过程，可参考[创建实例](../redis/user-guide/create.md)。

1. 在创建 `Redis` 实例过程中，在`服务设置`->`高级设置`中启用`工作负载反亲和性`。

    ![创建](images/anti-affinity01.png)

2. 参考以下说明填写工作负载反亲和性的配置。

    - 条件：分为`尽量满足`和`必须满足`两种。
        - 尽量满足：尽量尝试满足反亲和性要求，最终的部署结果不一定满足反亲和性要求
        - 必须满足：必须满足反亲和性要求。如果找不到可调度的节点/可用区/区域，则 Pod 会一直处于 Pending 状态。
    - 权重：条件设置为`必须满足`时无需设置权重。条件设置为`尽量满足`时，为反亲和性规则设置权重值，优先满足权重高的规则。
    - 拓扑域：拓扑域定义反亲和性的作用范围，可以为节点标签、zone 标签、region 标签，也可以由用户自定义。
    - Pod 选择器：设置 Pod 标签。**同一个拓扑域内，只能有一个带有此标签的 Pod**。
    - 有关反亲和性以及各种操作符的详细介绍，可参考[操作符](../../kpanda/user-guide/workloads/pod-config/scheduling-policy.md#_4)

        ![创建](images/anti-affinity02.jpg)
    
    !!! note

        上图配置的含义是，在同一个节点上只能有一个带有 `app.kubernetes.io/name` 标签且值为 `redis-test` 的 Pod。如果没有满足条件的节点，则 Pod 会一直处于 Pending 状态。

3. 参考[创建实例](../redis/user-guide/create.md)完成后续操作。

## 效果验证

配置好工作负载反亲和性并且实例创建成功后，进入[容器管理](../../kpanda/intro/what.md)模块查看 `Pod` 调度信息。

![查看 Pod](images/anti-affinity04.jpg)

可见一共 3 个 Pod，两个已经在正常运行并且分布在不同的节点上。

第三个 Pod 处于等待状态，点击 Pod 名称查看详情，发现原因是污点和反亲和性规则导致没有可以部署的节点。

![事件日志](images/anti-affinity03.jpg)

!!! success

    这说明前面配置的工作负载反亲和性已经生效，即一个节点上之后只能有一个带有 `app.kubernetes.io/name` 标签且值为 `redis-test` 的 Pod。如果没有满足条件的节点，则 Pod 一直处于 Pending 状态。
