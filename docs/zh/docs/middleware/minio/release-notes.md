# MinIO 对象存储 Release Notes

本页列出 MinIO 对象存储的 Release Notes，便于您了解各版本的演进路径和特性变化。

## 2023-06-30

### v0.7.0

#### 新功能

- **新增** 对接全局管理审计日志模块

#### 优化

- **优化** 监控图表，去除干扰元素并新增时间范围选择

## 2023-04-27

### v0.5.1

#### 新功能

- **新增** `mcamel-minio` 详情页面展示相关的事件
- **新增** `mcamel-minio` 支持自定义角色

#### 优化

- **优化** `mcamel-minio` 调度策略增加滑动按钮

## v0.4.1

发布日期：2023-03-28

### API

- **修复** `mcamel-minio` 页面展示 LoadBalancer 地址错误。
- **修复** `mcamel-minio` 删除 MinIO 时不应该校验野生存储配置的问题。
- **修复** `mcamel-minio` 修复 创建 Bucket 偶尔会失败。

### 其他

- **升级** `mcamel-minio` golang.org/x/net 到 v0.7.0。

## v0.3.0

发布日期：2023-02-23

### API

- **新增** `mcamel-minio` helm-docs 模板文件。
- **新增** `mcamel-minio` 应用商店中的 Operator 只能安装在 mcamel-system。
- **新增** `mcamel-minio` 支持 cloud shell。
- **新增** `mcamel-minio` 支持导航栏单独注册。
- **新增** `mcamel-minio` 支持查看日志。
- **新增** `mcamel-minio` Operator 对接 chart-syncer。
- **修复** `mcamel-minio` 实例名太长导致自定义资源无法创建的问题。
- **修复** `mcamel-minio` 工作空间 Editor 用户无法查看实例密码。
- **升级** `mcamel-minio` 升级离线镜像检测脚本。  

### 文档

- **新增** 日志查看操作说明，支持自定义查询、导出等功能。

## v0.2.0

发布日期：2022-12-25

### API

- **新增** `mcamel-minio` NodePort 端口冲突提前检测。
- **新增** `mcamel-minio` 节点亲和性配置。
- **修复** `mcamel-minio` 修复单实例的时候，状态显示异常的问题。
- **修复** `mcamel-minio` 创建实例时未校验名字。

### UI

- **优化** `mcamel-minio` 取消认证信息输入框。

## v0.1.4

发布日期：2022-11-28

- **改进** 更新获取前端的接口，增加 sc 列表是否可以扩容
- **改进** 密码校验调整为 MCamel 中等密码强度
- **新增** 创建 MinIO 集群时配置 Bucket
- **新增** 返回列表或者详情时的公共字段
- **新增** 返回告警列表
- **新增** 校验 Service 注释
- **修复** 创建 MinIO 时，密码校验从 between 调整为 length
- **改进** 完善优化复制功能
- **改进** 实例详情 - 访问设置，移除 集群 IPv4
- **改进** 中间件密码校验难度调整
- **新增** minio 支持创建的时候内置 BUCKET 创建
- **新增** 对接告警能力
- **新增** 新增判断 sc 是否支持扩容并提前提示功能
- **优化** 优化安装环境检测的提示逻辑&调整其样式
- **优化** 中间件样式走查优化

## v0.1.2

发布日期：2022-11-08

- **新增** 获取用户列表接口
- **新增** minio 实例创建
- **新增** minio 实例的修改
- **新增** minio 实例的删除
- **新增** minio 实例的配置修改
- **新增** minio 实例支持 nodeport 的 svc
- **新增** minio 实例的监控数据导出
- **新增** minio 实例的监控查看
- **新增** 多租户全局管理的对接
- **新增** mcamel-minio-ui 的创建/列表/修改/删除/查看
- **新增** APIServer/UI 支持 mtls
- **修复** 单例模式下，只有一个 pod，修复 grafana 无法获取数据问题
- **优化** 完善了计算器功能
