# One-click Download of All Offline Packages

This page provides a script to easily download all the offline packages required for installing DCE 5.0.

## Download the Script

```bash
export VERSION= v0.8.0
curl -LO https://qiniu-download-public.daocloud.io/DaoCloud_Enterprise/dce5/download_packages_${VERSION}.sh
chmod +x download_packages_${VERSION}.sh
```

## Execute the Script

```bash
./download_packages_${VERSION}.sh ${DISTRO} ${INSTALLER_VERSION} ${ARCH}
```

Parameter explanation:

| Parameter | Default Value | Valid Values |
| ---- | ---- | ---- |
| VERSION | Current script version | Only supports v0.8.0 currently |
| INSTALLER_VERSION | Specify the version of DCE 5.0 to download | Any valid release version of DCE 5.0 |
| DISTRO | `centos7` | `centos7` `kylinv10` `redhat8` `ubuntu2004` |
| ARCH | `amd64` | `amd64` `arm64` |

!!! note

    - Supported operating systems for amd64: centos7, redhat8, ubuntu2004
    - Supported operating system for arm64: kylinv10
