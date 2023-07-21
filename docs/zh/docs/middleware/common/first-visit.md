---
hide:
  - toc
---

# 首次进入中间件

首次使用 DCE 5.0 的 [Elasticsearch 搜索服务](../elasticsearch/intro/what.md)、[Kafka 消息队列](../kafka/intro/what.md)、[MinIO 对象存储](../minio/intro/what.md)、[MySQL 数据库](../mysql/intro/what.md)、[RabbitMQ 消息队列](../rabbitmq/intro/what.md)、[PostgreSQL 数据库](../postgresql/intro/what.md)，或 [Redis 缓存服务](../redis/intro/what.md)、[MongoDB 数据库](../mongodb/intro/what.md)等中间件时，需要选择工作空间。

有关工作空间的详细介绍，可参考[工作空间与层级](../../ghippo/user-guide/workspace/ws-folder.md)。

下面以 MinIO 为例介绍如何选择工作空间，其他数据服务组件同理。

## 前提条件

1. 在 DCE 5.0 平台中创建[工作空间](../../ghippo/user-guide/workspace/workspace.md)
2. 如需直接创建中间件实例，还需要在 DCE 5.0 容器管理模块中[创建](../../kpanda/user-guide/clusters/create-cluster.md)或[接入](../../kpanda/user-guide/clusters/integrate-cluster.md)集群。

## 操作步骤

1. 在左侧导航栏中选择`中间件` -> `MinIO 存储`。

    ![选择工作空间](https://docs.daocloud.io/daocloud-docs-images/docs/middleware/minio/images/first-visit01.png)

2. 在弹窗中选择一个工作空间后，点击`确认`。

    ![选择工作空间](https://docs.daocloud.io/daocloud-docs-images/docs/middleware/minio/images/login02.png)

    !!! note

        如果未出现弹窗/想要切换工作空间，可手动点击红框中的切换图标选择新的工作空间。

3. 初次使用时，可以点击[`立即部署`](../minio/user-guide/create.md)来创建 MinIO 实例。

    ![立即部署](https://docs.daocloud.io/daocloud-docs-images/docs/middleware/minio/images/what03.png)