---
title: 設定服務
description: 瞭解如何在雲端基礎結構上設定Adobe Commerce使用的服務。
feature: Cloud, Configuration, Services
exl-id: 48091c10-c53f-4aad-afbe-b4516653bda1
source-git-commit: 4d790bff2ba5d02ef10de5c36a2f0d140e31a407
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 設定服務

此 `services.yaml` 檔案會定義Adobe Commerce在雲端基礎結構上支援及使用的服務，例如MySQL、Redis以及Elasticsearch或OpenSearch。 您不需要訂閱外部服務提供者。 此檔案位於 `.magento` 專案的目錄。

部署指令碼會使用 `.magento` 目錄，以使用已設定的服務布建環境。 如果服務包含在 [`relationships`](../application/properties.md#relationships) 的屬性 `.magento.app.yaml` 檔案。 此 `services.yaml` 檔案包含 _type_ 和 _磁碟_ 值。 服務型別會定義服務 _名稱_ 和 _版本_.

變更服務設定會讓部署在環境中布建更新的服務，進而影響下列環境：

- 所有入門環境，包括生產環境 `master`
- Pro整合環境

{{pro-update-service}}

## 預設與支援的服務

雲端基礎結構支援和部署以下服務：

- [MySQL](mysql.md)
- [Redis](redis.md)
- [RabbitMQ](rabbitmq.md)
- [Elasticsearch](elasticsearch.md)
- [OpenSearch](opensearch.md)

您可以檢視目前的預設版本和磁碟值， [預設 `services.yaml` 檔案](https://github.com/magento/magento-cloud/blob/master/.magento/services.yaml). 下列範例顯示 `mysql`， `redis`， `opensearch` 或 `elasticsearch`、和 `rabbitmq` 中定義的服務 `services.yaml` 設定檔：

```yaml
mysql:
    type: mysql:10.4
    disk: 5120

redis:
    type: redis:6.2

opensearch:
    type: opensearch:2  # minor version not required; uses latest
    disk: 1024

rabbitmq:
    type: rabbitmq:3.9
    disk: 1024
```

## 服務值

您必須提供服務ID和服務型別設定 `type: <name>:<version>`. 如果服務使用永久儲存體，則必須提供磁碟值。

使用以下格式：

```yaml
<service-id>:
    type: <name>:<version>
    disk: <value-MB>
```

### `service-id`

此 `service-id` 值會識別專案中的服務。 您只能使用小寫英數字元： `a` 至 `z` 和 `0` 至 `9`，例如 `redis`.

這個 _service-id_ 值用於 [`relationships`](../application/properties.md#relationships) 的屬性 `.magento.app.yaml` 設定檔：

```yaml
relationships:
    redis: "<name>:redis"
```

您可以為每種服務型別的多個執行個體命名。 例如，您可以使用多個Redis例項，一個用於作業階段，一個用於快取。

```yaml
redis:
    type: redis:<version>

redis2:
    type: redis:<version>
```

重新命名中的服務 `services.yaml` 檔案 **永久移除** 下列專案：

- 使用您指定的新名稱建立服務之前的現有服務。
- 服務的所有現有資料都會被移除。 Adobe強烈建議您 [備份您的入門環境](../storage/snapshots.md) 變更現有服務的名稱之前。

### `type`

此 `type` 值會指定服務名稱和版本。 例如：

```yaml
mysql:
    type: mysql:10.4
```

### `disk`

此 `disk` 值指定要配置給服務的永久磁碟儲存大小（以MB為單位）。 使用永久儲存體的服務（例如MySQL）必須提供磁碟值。 使用記憶體而非永久儲存體的服務（例如Redis）不需要磁碟值。

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
```

目前每個專案的預設儲存容量為5 GB，即512 0MB。 您可以在應用程式及其每項服務之間分配此金額。

## 服務關係

在Adobe Commerce中關於雲端基礎結構專案、服務 [關係](../application/properties.md#relationships) 設定於 `.magento.app.yaml` 檔案決定應用程式可使用哪些服務。

您可以從以下位置擷取所有服務關係的組態資料： [`$MAGENTO_CLOUD_RELATIONSHIPS`](../environment/variables-cloud.md) 環境變數。 設定資料包括服務名稱、型別和版本，以及任何必要的連線詳細資訊，例如連線埠號碼和登入認證。

**驗證本機環境中的關係**：

1. 在您的本機環境中，顯示使用中環境的關係。

   ```bash
   magento-cloud relationships
   ```

1. 確認 `service` 和 `type` 從回應。 回應會提供連線資訊，例如IP位址和連線埠號碼。

   >縮寫的範例回應

   ```terminal
   redis:
       -
   ...
           type: 'redis:7.0'
           port: 6379
   elasticsearch:
       -
   ...
           type: 'opensearch:2'
           port: 9200
   database:
       -
   ...
           type: 'mysql:10.6'
           port: 3306
   ```

**驗證遠端環境中的關係**：

1. 使用SSH登入遠端環境。

1. 列出在環境中設定的所有服務的關係設定資料。

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   或者，使用下列 `ece-tools` 檢視關係的命令：

   ```bash
   php ./vendor/bin/ece-tools env:config:show services
   ```

1. 確認 `service` 和 `type` 從回應。 回應會提供連線資訊，例如IP位址和連線埠號碼，以及任何必要的使用者名稱和密碼認證。

## 服務版本

雲端基礎結構上Adobe Commerce的服務版本和相容性支援取決於雲端基礎結構上部署和測試的版本，有時與Adobe Commerce內部部署支援的版本不同。 另請參閱 [系統需求](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) 在 _安裝_ Adobe已使用特定Adobe Commerce和Magento Open Source版本測試的第三方軟體相依性清單指南。

### 軟體EOL檢查

在部署程式中， `ece-tools` 套件會根據每項服務的生命週期結束(EOL)日期，檢查已安裝的服務版本。

- 如果服務版本在EOL日期後的三個月內，部署記錄中會顯示通知。
- 如果EOL日期是過去，則會顯示警告通知。

為維護商店安全性，請在已安裝軟體版本到達EOL之前更新這些版本。 您可以在以下位置檢視EOL日期： [ece-tools&#39; `eol.yaml` 檔案](https://github.com/magento/ece-tools/blob/develop/config/eol.yaml).

### 移轉至OpenSearch

{{elasticsearch-support}}

如需Adobe Commerce 2.4.4版和更新版本的相關資訊，請參閱 [設定OpenSearch服務](opensearch.md).

## 變更服務版本

您可以升級已安裝的服務版本，使其與雲端環境中部署的Adobe Commerce版本相容。

您無法直接將已安裝服務的服務版本降級。 不過，您可以建立具有所需版本的服務。 另請參閱 [降級服務版本](#downgrade-version).

### 升級已安裝的服務版本

您可以更新中提供的服務組態，升級已安裝的服務版本。 `services.yaml` 檔案。

1. 變更 [`type`](#type) 中服務的值 `.magento/services.yaml` 檔案：

   > 原始服務定義

   ```yaml
   mysql:
       type: mysql:10.3
       disk: 2048
   ```

   > 已更新服務定義

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

1. 新增、提交和推送您的程式碼變更。

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Upgrade MySQL from MariaDB 10.3 to 10.4."
   ```

   ```bash
   git push origin <branch-name>
   ```

### 降級版本

您無法直接降級已安裝的服務。 您有兩個選項：

1. 以新版本重新命名現有服務，移除現有服務和資料，並新增新服務和資料。

1. 建立服務並儲存現有服務的資料。

當您變更服務版本時，您必須更新 `services.yaml` 檔案並更新此檔案中的關係： `.magento.app.yaml` 檔案。

**若要藉由重新命名現有服務來降級服務版本**：

1. 重新命名中的現有服務 `.magento/services.yaml` 並變更版本。

   >[!WARNING]
   >
   >重新命名現有服務會取代現有服務並刪除所有資料。 如果您需要保留資料，請建立服務，而非重新命名現有服務。

   例如，若要將的MariaDB版本降級 _mysql_ 服務從10.4版到10.3版，變更現有的 _service-id_ 和 _type_ 設定。

   > 原始 `services.yaml` 定義

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

   > 新增 `services.yaml` 定義

   ```yaml
   mysql2:
        type: mysql:10.3
        disk: 5120
   ```

1. 更新以下專案中的關係： `.magento.app.yaml` 檔案。

   > 原始 `.magento.app.yaml` 設定

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > 已更新 `.magento.app.yaml` 設定

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. 新增、提交和推送您的程式碼變更。

**若要藉由建立服務來降級服務**：

1. 將服務定義新增至 `services.yaml` 具有降級版本規格的專案檔案。 另請參閱 _mysql2_ 在下列範例中：

   > services.yaml

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   mysql2:
       type: mysql:10.3
       disk: 5120
   ```

1. 變更中的關係設定 `.magento.app.yaml` 檔案以使用新服務。

   > 原始 `.magento.app.yaml` 設定

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > 新增 `.magento.app.yaml` 設定

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. 新增、提交和推送您的程式碼變更。
