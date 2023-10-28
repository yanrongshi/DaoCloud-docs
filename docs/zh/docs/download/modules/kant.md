# 云边协同 kant

本页可下载云边协同各版本的离线安装包。

## 下载

| 版本                                          | 架构     | 文件大小    | 安装包                                                                                                                                                     | 校验文件                                                                                                                                                                                  | 更新日期      |
|---------------------------------------------|--------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| [0.5.0](../../kant/intro/release-notes.md) | AMD 64 | 92.49MB | [:arrow_down: kant_0.5.0_amd64.tar](https://qiniu-download-public.daocloud.io/DaoCloud_Enterprise/kant_0.5.0_amd64.tar)                                 | [:arrow_down: kant_0.5.0_amd64_checksum.sha512sum](https://qiniu-download-public.daocloud.io/DaoCloud_Enterprise/kant_0.5.0_amd64_checksum.sha512sum)                                 | 2023-10-27 |
| [0.5.0](../../kant/intro/release-notes.md) | AMD 64 | 28.4MB  | [:arrow_down: kantadm_installation_0.5.0_amd64.tar](https://qiniu-download-public.daocloud.io/DaoCloud_Enterprise/kantadm_installation_0.5.0_amd64.tar) | [:arrow_down: kantadm_installation_0.5.0_amd64_checksum.sha512sum](https://qiniu-download-public.daocloud.io/DaoCloud_Enterprise/kantadm_installation_0.5.0_amd64_checksum.sha512sum) | 2023-10-27 |
| [0.5.0](../../kant/intro/release-notes.md) | ARM 64 | 28.1MB  | [:arrow_down: kantadm_installation_0.5.0_arm64.tar](https://qiniu-download-public.daocloud.io/DaoCloud_Enterprise/kantadm_installation_0.5.0_arm64.tar) | [:arrow_down: kantadm_installation_0.5.0_arm64_checksum.sha512sum](https://qiniu-download-public.daocloud.io/DaoCloud_Enterprise/kantadm_installation_0.5.0_arm64_checksum.sha512sum) | 2023-10-27 |


## 校验

在下载离线安装包和校验文件的目录，执行以下命令校验完整性：

```sh
echo "$(cat kant_0.5.0_amd64_checksum.sha512sum)" | sha512sum -c
```

校验成功后打印结果类似于：

```none
kant_0.5.0_amd64.tar: ok
```

## 安装

参阅[离线升级云边协同模块](../../kant/intro/offline-upgrade.md)进行安装。

如果是初次安装，请[申请免费体验](../../dce/license0.md)或联系我们授权：电邮 info@daocloud.io 或致电 400 002 6898。
如果有任何许可密钥相关的问题，请联系 DaoCloud 交付团队。
