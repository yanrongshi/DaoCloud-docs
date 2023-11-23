# Elasticsearch

This page allows you to download offline packages for different versions of Elasticsearch.

## Download

| Version                                                         | Architecture | File Size | Package                                                                                                                                   | Checksum File | Update Date |
|-----------------------------------------------------------------|--------------|-----------|-------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------|
| [v0.10.1](../../../middleware/elasticsearch/release-notes.md) | AMD 64       | 296.23MB  | [:arrow_down: elasticsearch_0.10.1_amd64.tar](https://qiniu-download-public.daocloud.io/DaoCloud_Enterprise/elasticsearch_0.10.1_amd64.tar) | [:arrow_down: elasticsearch_0.10.1_amd64_checksum.sha512sum](https://qiniu-download-public.daocloud.io/DaoCloud_Enterprise/elasticsearch_0.10.1_amd64_checksum.sha512sum) | 2023-10-10 |

## Validation

To validate the integrity of the downloaded offline package and checksum file, run the following command in the directory where they are located:

```sh
echo "$(cat elasticsearch_0.10.1_amd64_checksum.sha512sum)" | sha512sum -c
```

After successful validation, the output will be similar to:

```none
elasticsearch_0.10.1_amd64.tar: OK
```

## Installation

If this is your first installation, please [apply for a free trial](../../../dce/license0.md) or contact us for authorization: Email info@daocloud.io or call 400 002 6898.
For any license-related questions, please contact the DaoCloud Delivery Team.
