---
title: 設定OpenSearch服務
description: 瞭解如何在雲端基礎結構上啟用Adobe Commerce的OpenSearch服務。
feature: Cloud, Search, Services
exl-id: 10dc6367-3f90-4ab6-a84e-15e8c3b32a38
source-git-commit: d4c36b084094846cfad69adc2bffd567a58fab26
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# 設定OpenSearch服務

此 [OpenSearch](https://www.opensearch.org) 服務是Elasticsearch7.10.2的開放原始碼復本，在Elasticsearch的授權變更後執行。 請參閱 [OpenSource專案](https://github.com/opensearch-project) 在GitHub中。

{{elasticsearch-support}}

OpenSearch可讓您從任何來源、任何格式取得資料，並即時搜尋和視覺化資料。

- 產品目錄中的產品的快速和進階搜尋
- OpenSearch分析器支援多種語言
- 支援停用字和同義字
- 在重新索引操作完成之前，索引不會影響客戶

{{service-instruction}}

>[!TIP]
>
>Adobe建議您一律在雲端基礎結構專案中為您的Adobe Commerce設定OpenSearch，即使您計畫為您的Adobe Commerce應用程式設定協力廠商搜尋工具亦然。 如果協力廠商搜尋工具失敗，設定OpenSearch可提供後援選項。

**啟用OpenSearch**：

1. 對於入門和專業整合環境，請新增 `opensearch` 服務至 `.magento/services.yaml` 檔案的適當版本，以及配置的磁碟空間（以MB為單位）。 在這種情況下，版本2是合適的。 不需要次要版本，因為雲端基礎結構使用最新版的OpenSearch。

   ```yaml
   opensearch:
       type: opensearch:2
       disk: 1024
   ```

   若為Pro專案，您必須 [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 以變更測試和生產環境中的OpenSearch版本。

1. 設定或驗證 `relationships` 中的屬性 `.magento.app.yaml` 檔案。

   ```yaml
   relationships:
       opensearch: "opensearch:opensearch"
   ```

1. 新增、提交和推送程式碼變更。

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable OpenSearch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   如需這些變更如何影響您環境的詳細資訊，請參閱 [設定服務](services-yaml.md).

1. 部署程式完成後，請使用SSH登入遠端環境。

   ```bash
   magento-cloud ssh
   ```

1. 重新索引目錄搜尋索引。

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. 清除快取。

   ```bash
   bin/magento cache:clean
   ```

{{service-change-tip}}

## OpenSearch軟體相容性

在雲端基礎結構專案上安裝或升級Adobe Commerce時，請務必檢查OpenSearch服務版本與 [OpenSearch PHP](https://github.com/opensearch-project/opensearch-php) Adobe Commerce使用者端。

- **首次設定** — 確認指定的OpenSearch版本 `services.yaml` 檔案與為Adobe Commerce設定的OpenSearch PHP使用者端相容。

- **專案升級** — 確認新應用程式版本中的OpenSearch PHP使用者端與安裝在雲端基礎結構上的OpenSearch服務版本相容。

服務版本和相容性支援取決於在雲端基礎結構上測試和部署的版本，有時與Adobe Commerce內部部署支援的版本不同。 另請參閱 [系統需求](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) 在 _安裝指南_ 以取得支援版本的清單。

**驗證OpenSearch軟體相容性**：

1. 在本機工作站上，變更至專案目錄。

1. 顯示使用中環境的OpenSearch詳細資訊。

   ```bash
   magento-cloud relationships --property=opensearch
   ```

1. 或者，您可以使用SSH登入遠端環境。

   ```bash
   magento-cloud ssh
   ```

1. 擷取OpenSearch服務連線詳細資料。

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   在回應中，尋找OpenSearch服務端點的IP位址和連線埠：

   ```terminal
   +------------------------------------------+--------------------------------------------------------+
   | opensearch:                                                                                       |
   +------------------------------------------+--------------------------------------------------------+
   | username                                 | null                                                   |
   | scheme                                   | http                                                   |
   | service                                  | opensearch                                             |
   | fragment                                 | null                                                   |
   | ip                                       | 169.254.220.11                                         |
   | hostname                                 | hostf75wi3sd24l.opensearch.service._.magentosite.cloud |
   | port                                     | 9200                                                   |
   | cluster                                  | projectID-develop-4ranwui                              |
   | host                                     | opensearch.internal                                    |
   | rel                                      | opensearch                                             |
   | path                                     | null                                                   |
   | query                                    |                                                        |
   | password                                 | null                                                   |
   | type                                     | opensearch:2                                           |
   | public                                   | false                                                  |
   | host_mapped                              | false                                                  |
   ```

1. 擷取已安裝的OpenSearch服務 `version:number` 服務端點。

   ```bash
   curl -XGET <opensearch-service-endpoint-ip-address>:9200
   ```

   ```terminal
   {
      "name" : "opensearch.0",
      "cluster_name" : "opensearch",
      "cluster_uuid" : "_yzaae6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "distribution" : "opensearch",
        "number" : "2.5.0",
        "build_type" : "deb",
        "build_hash" : "aaaaaaa",
        "build_date" : "2023-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "9.4.2",
        "minimum_wire_compatibility_version" : "7.10.0",
        "minimum_index_compatibility_version" : "7.0.0"
   },
   "tagline" : "The OpenSearch Project: https://opensearch.org/"
   }
   ```

{{pro-update-service}}

## 重新啟動OpenSearch服務

如果您需要重新啟動OpenSearch服務，必須聯絡Adobe Commerce支援。

## 其他搜尋設定

- 根據預設，雲端環境的搜尋設定會在您每次部署時重新產生。 您可以使用 `SEARCH_CONFIGURATION` 部署變數，以在部署之間保留自訂搜尋設定。 另請參閱 [部署變數](../environment/variables-deploy.md#search_configuration).

- 在您為專案設定OpenSearch服務後，請使用管理員UI來測試OpenSearch連線並自訂Adobe Commerce的OpenSearch設定。

### 新增OpenSearch的外掛程式

您可以選擇新增外掛程式以進行OpenSearch `configuration:plugins` 區段至中的OpenSearch服務 `.magento/services.yaml` 檔案。 例如，下列程式碼會啟用ICU分析和注音分析外掛程式。

```yaml
opensearch:
    type: opensearch:2
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

請參閱 [OpenSearch專案](https://github.com/opensearch-project) 瞭解更多外掛程式。

### 移除OpenSearch的外掛程式

從移除外掛程式專案 `opensearch:` 的區段 `.magento/services.yaml` 檔案會 **非** 解除安裝或停用服務。 若要完全停用服務，您必須從移除外掛程式之後，重新索引OpenSearch資料 `.magento/services.yaml` 檔案。 此設計可防止依賴這些外掛程式的資料可能遺失或損毀。

**移除OpenSearch外掛程式**：

1. 從您的OpenSearch外掛程式專案移除 `.magento/services.yaml` 檔案。
1. 新增、提交和推送您的程式碼變更。

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Remove OpenSearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. 認可 `.magento/services.yaml` 對您的雲端存放庫進行的變更。
1. 重新索引目錄搜尋索引。

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. 清除快取。

   ```bash
   bin/magento cache:clean
   ```
