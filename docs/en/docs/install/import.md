# Offline Resource Import

## Overview

The DCE5 installer (only supports version v0.9.0 and above) introduces the `import-artifact` command for importing offline resources. Currently, the following offline resources can be imported:

- `*.iso` operating system ISO image files

- `os-pkgs-${disto}-${kubean_version}.tar.gz` osPackage offline package provided by Kubean

- `offline-${install_version}-${arch}.tar` Full mode offline image package for the installer:

  - K8S binaries & images

  - Images files and charts packages for various modules of DCE5

## Use Cases

### Use Case 1

When the operating system of the global service cluster is different from the one used to create the working cluster, it is necessary to import the corresponding ISO image files and osPackage offline package for the working cluster.

Example: [Create a working cluster with Ubuntu operating system on CentOS global service cluster](../kpanda/best-practice/create-ubuntu-on-centos-platform.md)

### Use Case 2

In a hybrid architecture offline deployment scenario, it is required to import and integrate the corresponding resources for arm64 based on existing amd64 offline resources (K8S binaries) && (K8S images + images files and charts packages for various modules).

Example: [How to Add Heterogeneous Nodes to a Working Cluster](../kpanda/best-practice/multi-arch.md)

## Introduction to Import Commands

Pre-download the dce5-installer binary file.

### Import Operating System ISO Image File

Taking TencentOS-Server-3.1-TK4-x86_64-minimal-2209.3.iso as an example:

``` bash
# When deploying the SparklingCluster in build-in mode, we don't need to specify the clusterConfig.yml configuration file
dce5-installer import-artifact --iso-path=/home/iso/TencentOS-Server-3.1-TK4-x86_64-minimal-2209.3.iso

# When deploying the SparklingCluster in external mode, we need to specify the clusterConfig.yml configuration file
dce5-installer import-artifact -c clusterConfig.yml --iso-path=/home/iso/TencentOS-Server-3.1-TK4-x86_64-minimal-2209.3.iso
```

### Import osPackage Offline Package Provided by Kubean

Taking os-pkgs-tencent31-v0.6.2.tar.gz as an example:

``` bash
# When deploying the SparklingCluster in build-in mode, we don't need to specify the clusterConfig.yml configuration file
dce5-installer import-artifact --os-pkgs-path=/home/os-pkgs/os-pkgs-tencent31-v0.6.2.tar.gz

# When deploying the SparklingCluster in external mode, we need to specify the clusterConfig.yml configuration file
dce5-installer import-artifact -c clusterConfig.yml --os-pkgs-path=/home/os-pkgs/os-pkgs-tencent31-v0.6.2.tar.gz
```

### Import Offline Image Package Content of Installer's Offline Directory

``` bash
# When deploying the SparklingCluster in build-in mode, we don't need to specify the clusterConfig.yml configuration file
dce5-installer import-artifact --offline-path=/home/offline/

# When deploying the SparklingCluster in external mode, we need to specify the clusterConfig.yml configuration file
dce5-installer import-artifact -c clusterConfig.yml --offline-path=/home/offline/
```

### Import Multiple Offline Resources Simultaneously

``` bash
# When deploying the SparklingCluster in build-in mode, we don't need to specify the clusterConfig.yml configuration file
dce5-installer import-artifact \
      --offline-path=/home/offline/ \
      --os-pkgs-path=/home/os-pkgs/os-pkgs-tencent31-v0.6.2.tar.gz \
      --iso-path=/home/iso/TencentOS-Server-3.1-TK4-x86_64-minimal-2209.3.iso

# When deploying the SparklingCluster in external mode, we need to specify the clusterConfig.yml configuration file
dce5-installer import-artifact -c clusterConfig.yml \
      --offline-path=/home/offline/ \
      --os-pkgs-path=/home/os-pkgs/os-pkgs-tencent31-v0.6.2.tar.gz \
      --iso-path=/home/iso/TencentOS-Server-3.1-TK4-x86_64-minimal-2209.3.iso
```
