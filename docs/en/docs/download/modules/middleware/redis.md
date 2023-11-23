# Redis

This page provides downloadable offline packages for various versions of Redis.

## Download

| Version                                                       | Architecture | File Size | Installation Package                                                                                                               | Checksum File | Update Date |
|---------------------------------------------------------------| ------------ |---------- |-----------------------------------------------------------------------------------------------------------------------------------| ------------- |--------------|
| [v0.11.1](../../../middleware/redis/release-notes.md)         | AMD 64       | 296.23MB  | [:arrow_down: redis_0.11.1_amd64.tar](https://qiniu-download-public.daocloud.io/DaoCloud_Enterprise/redis_0.11.1_amd64.tar) | [:arrow_down: redis_0.11.1_amd64_checksum.sha512sum](https://qiniu-download-public.daocloud.io/DaoCloud_Enterprise/redis_0.11.1_amd64_checksum.sha512sum) | 2023-10-10 |

## Validation

In the directory where you downloaded the offline package and checksum file, run the following command to validate integrity:

```sh
echo "$(cat redis_0.11.1_amd64_checksum.sha512sum)" | sha512sum -c
```

Upon successful validation, the result will be printed similar to:

```none
redis_0.11.1_amd64.tar: OK
```

## Installation

If this is your first installation, please [apply for a free trial](../../../dce/license0.md) or contact us for authorization: email info@daocloud.io or call 400 002 6898.
If you have any inquiries related to license keys, please contact the DaoCloud delivery team.
