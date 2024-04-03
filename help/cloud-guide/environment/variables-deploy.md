---
title: 部署變數
description: 檢視在雲端基礎結構部署階段的Adobe Commerce中控制動作的環境變數清單。
feature: Cloud, Configuration, Cache, Deploy, SCD, Storage, Search
recommendations: noDisplay, catalog
role: Developer
exl-id: 673880b5-830b-4837-ac0c-5fa5643ae34c
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 0%

---

# 部署變數

下列專案 _部署_ 變數可控制部署階段的動作，並可繼承及覆寫以下專案的值： [全域變數](variables-global.md). 將這些變數插入 `deploy` 的階段 `.magento.env.yaml` 檔案：

```yaml
stage:
  deploy:
    DEPLOY_VARIABLE_NAME: value
```

如需自訂建置和部署程式的詳細資訊：

- [部署設定](configure-env-yaml.md)
- [部署流程](../deploy/process.md)

## `CACHE_CONFIGURATION`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

設定Redis頁面和預設快取。 設定時 `cm_cache_backend_redis` 引數，您必須指定 `server`， `port`、和 `database` 選項。

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          backend: file
        page_cache:
          backend: file
```

{{merge-options}}

以下範例會將新值合併至現有設定：

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          backend_options:
            database: 10
        page_cache:
          backend_options:
            database: 11
```

以下範例使用 [Redis預先載入功能](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/redis-pg-cache.html#redis-preload-feature) 如 _設定指南_：

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          id_prefix: '061_'
          backend_options:
            preload_keys:
              - '061_EAV_ENTITY_TYPES:hash'
              - '061_GLOBAL_PLUGIN_LIST:hash'
              - '061_DB_IS_UP_TO_DATE:hash'
              - '061_SYSTEM_DEFAULT:hash'
```

使用自訂 [REDIS_BACKEND](#redis_backend) 模型（不僅從允許清單），設定 `_custom_redis_backend` 選項至 `true` 如下列範例所示，啟用正確的驗證：

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          _custom_redis_backend: true
          backend: '\CustomRedisModel'
```

## `CLEAN_STATIC_FILES`

- **預設**—`true`
- **版本**—Adobe Commerce 2.1.4和更新版本

啟用或停用清潔功能 [靜態內容檔案](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html) 產生於建置或部署階段。 使用預設值 _true_ 作為最佳實務的開發中。

- **`true`** — 在部署更新的靜態內容之前，移除所有現有的靜態內容。
- **`false`** — 只有在產生的內容包含較新版本時，部署才會覆寫現有的靜態內容檔案。

如果您透過個別程式修改靜態內容，請將值設為 _false_.

```yaml
stage:
  deploy:
    CLEAN_STATIC_FILES: false
```

如果在部署之前未清除靜態檢視檔案，則在不移除先前版本的情況下將更新部署到現有檔案時，可能會導致問題。 因為 [靜態檔案遞補](https://developer.adobe.com/commerce/frontend-core/guide/caching/#clean-static-files-cache) 如果目錄包含相同檔案的多個版本，則後援作業可能會顯示錯誤的檔案。

## `CRON_CONSUMERS_RUNNER`

- **預設**—`cron_run = false`， `max_messages = 1000`
- **版本**—Adobe Commerce 2.2.0和更新版本

使用此環境變數來確認訊息佇列在部署後是否執行。

- `cron_run` — 布林值，可啟用或停用 `consumers_runner` cron工作(預設= `false`)。
- `max_messages` — 指定每個取用者在終止前必須處理的最大訊息數(預設值= `1000`)。 您可以將值設為 `0` 以防止消費者終止。
- `consumers` — 字串陣列，指定要執行的使用者。 空陣列執行 _全部_ 消費者。

- `multiple_processes` — 一個數字，指定每個使用者要衍生的處理作業數目。 Commerce支援 **2.4.4** 或更高。

>[!NOTE]
>
>傳回訊息佇列清單的方式 `consumers`，執行 `./bin/magento queue:consumers:list` 命令來修改遠端環境。

執行特定的陣列範例 `consumers` 和 `multiple_processes` 為每個取用者繁衍：

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers:
        - example_consumer_1
        - example_consumer_2
-     multiple_processes:
        example_consumer_1: 4
        example_consumer_2: 3
```

執行全部的空白陣列範例 `consumers`：

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers: []
```

依預設，部署程式會覆寫 `env.php` 檔案。 另請參閱 [管理訊息佇列](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/manage-message-queues.html) 在 _Commerce設定指南_ 適用於內部部署Adobe Commerce。

## `CONSUMERS_WAIT_FOR_MAX_MESSAGES`

- **預設**—`false`
- **版本**—Adobe Commerce 2.2.0和更新版本

設定方式 `consumers` 選擇下列其中一個選項，處理來自訊息佇列的訊息：

- `false`—`Consumers` 處理佇列中的可用訊息、關閉TCP連線，然後終止。 `Consumers` 即使已處理的訊息數小於 `max_messages` 中指定的值 `CRON_CONSUMERS_RUNNER` 部署變數。

- `true`—`Consumers` 繼續處理來自訊息佇列的訊息，直到達到訊息數目上限(`max_messages`)中指定的 `CRON_CONSUMERS_RUNNER` 在關閉TCP連線並終止取用者處理序之前部署變數。 如果佇列在到達之前排空 `max_messages`，消費者會等待更多訊息到達。

>[!WARNING]
>
>如果您使用背景工作來執行 `consumers` 將此變數設為true，而不使用cron工作。

```yaml
stage:
  deploy:
    CONSUMERS_WAIT_FOR_MAX_MESSAGES: false
```

## `CRYPT_KEY`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

>[!WARNING]
>
>設定 `CRYPT_KEY` 值透過 [!DNL Cloud Console] 而非 `.magento.env.yaml` 檔案中的金鑰，避免在您的環境的原始程式碼存放庫中公開金鑰。 另請參閱 [設定環境和專案變數](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html#configure-environment).

將資料庫從一個環境移動到另一個環境時，若沒有安裝程式，則需要相應的密碼編譯資訊。 Adobe Commerce會使用 [!DNL Cloud Console] 作為 `crypt/key` 中的值 `env.php` 檔案。

## `DATABASE_CONFIGURATION`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

如果您在 [關係屬性](../application/properties.md#relationships) 的 `.magento.app.yaml` 檔案時，您可以自訂資料庫連線以進行部署。

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_value'
```

{{merge-options}}

以下範例會將新值合併至現有設定：

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_new_value'
      _merge: true
```

您也可以設定表格首碼。

>[!WARNING]
>
>如果您未將合併選項與表格首碼搭配使用，則必須提供預設連線設定，否則部署會驗證失敗。

以下範例使用 `ece_` 具有預設連線設定的表格首碼，而非使用 `_merge` 選項：

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          username: user
          host: host
          dbname: magento
          password: password
      table_prefix: 'ece_'
```

範例輸出：

```terminal
MariaDB [main]> SHOW TABLES;
+-------------------------------------+
| Tables_in_main                      |
+-------------------------------------+
| ece_admin_passwords                 |
| ece_admin_system_messages           |
| ece_admin_user                      |
| ece_admin_user_session              |
| ece_adminnotification_inbox         |
| ece_amazon_customer                 |
| ece_authorization_rule              |
| ece_cache                           |
| ece_cache_tag                       |
| ece_captcha_log                     |
...
```

## `ELASTICSUITE_CONFIGURATION`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.2.0和更新版本

保留自訂 [!DNL Elastic Suite] 部署之間的服務設定，並在主要頁面的「system/default/smile_elasticsuite_core_base_settings」區段使用 [!DNL Elastic Suite] 設定。 如果 [!DNL Elastic Suite] Composer套件已安裝，且已自動設定。

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      es_client:
        servers: 'remote-host:9200'
      indices_settings:
        number_of_shards: 1
        number_of_replicas: 0
```

{{merge-options}}

以下範例會將新值合併至現有設定：

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      indices_settings:
        number_of_shards: 3
        number_of_replicas: 2
      _merge: true
```

**已知限制**：

- 將搜尋引擎變更為任何型別 `elasticsuite` 導致部署失敗，並伴隨適當的驗證錯誤
- 移除Elasticsearch服務會導致部署失敗，並伴隨適當的驗證錯誤

>[!NOTE]
>
>有關使用或疑難排解的詳細資訊 [!DNL Elastic Suite] 外掛程式搭配Adobe Commerce，請參閱 [[!DNL Elastic Suite] 檔案](https://github.com/Smile-SA/elasticsuite).

## `ENABLE_GOOGLE_ANALYTICS`

- **預設**—`false`
- **版本**—Adobe Commerce 2.1.4和更新版本

在部署至中繼和整合環境時，啟用和停用Google Analytics。 依預設，Google Analytics僅適用於生產環境。 將此值設為 `true` 在中繼和整合環境中啟用Google Analytics。

- **`true`** — 在中繼和整合環境中啟用Google Analytics。
- **`false`** — 在中繼和整合環境中停用Google Analytics。

新增 `ENABLE_GOOGLE_ANALYTICS` 環境變數至 `deploy` 中的階段 `.magento.env.yaml` 檔案：

```yaml
stage:
  deploy:
    ENABLE_GOOGLE_ANALYTICS: true
```

>[!NOTE]
>
>部署程式一律會在生產環境中啟用Google Analytics。

## `FORCE_UPDATE_URLS`

- **預設**—`true`
- **版本**—Adobe Commerce 2.1.4和更新版本

在部署至Pro或Starter Staging和生產環境時，此變數會以指定的專案URL取代資料庫中的Adobe Commerce基底URL。 [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) 變數中。 使用此設定覆寫 [UPDATE_URL](#update_urls) 部署變數，在部署到中繼或生產環境時會忽略該變數。

```yaml
stage:
  deploy:
    FORCE_UPDATE_URLS: true
```

## `LOCK_PROVIDER`

- **預設**—`file`
- **版本**—Adobe Commerce 2.2.5和更新版本

鎖定提供者可防止啟動重複的cron作業和cron群組。 使用 `file` 在生產環境中鎖定提供者。 入門環境和Pro整合環境不使用 [Magento_CLOUD_LOCKS_DIR](variables-cloud.md) 變數，因此 `ece-tools` 套用 `db` 自動鎖定提供者。

```yaml
stage:
  deploy:
    LOCK_PROVIDER: "db"
```

另請參閱 [設定鎖定](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/lock-provider.html) 在 _安裝指南_.

## `MYSQL_USE_SLAVE_CONNECTION`

- **預設**—`false`
- **版本**—Adobe Commerce 2.1.4和更新版本

>[!TIP]
>
>此 `MYSQL_USE_SLAVE_CONNECTION` 變數僅在雲端基礎結構測試和生產Pro叢集環境的Adobe Commerce上受支援，且在入門專案上不受支援。

Adobe Commerce可以非同步讀取多個資料庫。 將設為 `true` 以自動使用 _唯讀_ 連線至資料庫，以接收非主節點上的唯讀流量。 此連線透過負載平衡來改善效能，因為只有一個節點處理讀寫流量。 將設為 `false` 以從移除任何現有的唯讀連線陣列 `env.php` 檔案。

```yaml
stage:
  deploy:
    MYSQL_USE_SLAVE_CONNECTION: true
```

當 `MYSQL_USE_SLAVE_CONNECTION` 變數設為 `true`，則 `synchronous_replication` 引數已設為 `true` 根據預設，在 `env.php` Pro測試和生產環境上的檔案。 當 `MYSQL_USE_SLAVE_CONNECTION` 設為 `false`，則 `synchronous_replication` 引數未設定。

## `QUEUE_CONFIGURATION`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

使用此環境變數可保留部署間的自訂AMQP服務設定。 例如，如果您偏好使用現有的訊息佇列服務，而非依賴雲端基礎結構為您建立，請使用 `QUEUE_CONFIGURATION` 環境變數來連線到您的網站：

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      amqp:
        host: test.host
        port: 1234
      amqp2:
        host: test.host2
        port: 12345
      mq:
        host: mq.host
        port: 1234
```

{{merge-options}}

以下範例會將新值合併至現有設定：

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      _merge: true
      amqp:
        host: changed1.host
        port: 5672
      amqp2:
        host: changed2.host2
        port: 12345
      mq:
        host: changedmq.host
        port: 1234
```

## `REDIS_BACKEND`

- **預設**—`Cm_Cache_Backend_Redis`
- **版本**—Adobe Commerce 2.3.0和更新版本

指定Redis快取的後端模型設定。

Adobe Commerce 2.3.0版和更新版本包含下列後端模型：

- `Cm_Cache_Backend_Redis`
- `\Magento\Framework\Cache\Backend\Redis`
- `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache`

如何設定的範例 `REDIS_BACKEND`

```yaml
stage:
  deploy:
    REDIS_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
```

>[!NOTE]
>
>如果您指定 `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache` 作為Redis後端模型來啟用 [L2快取](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html)， `ece-tools` 會自動產生快取設定。 檢視範例 [組態檔](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html#configuration-example) 在 _Adobe Commerce設定指南_. 若要覆寫產生的快取設定，請使用 [快取組態](#cache_configuration) 部署變數。

## `REDIS_USE_SLAVE_CONNECTION`

- **預設**—`false`
- **版本**—Adobe Commerce 2.1.16和更新版本

>[!WARNING]
>
>執行 _非_ 在上啟用此變數 [擴充架構](../architecture/scaled-architecture.md) 專案。 這會導致Redis連線錯誤。 Redis從屬仍然有效，但不會用於Redis讀取。 作為替代方法，Adobe建議使用Adobe Commerce 2.3.5或更新版本，實作新的Redis後端設定，並實作Redis的L2快取。

>[!TIP]
>
>此 `REDIS_USE_SLAVE_CONNECTION` 變數僅在雲端基礎結構測試和生產Pro叢集環境的Adobe Commerce上受支援，且在入門專案上不受支援。

Adobe Commerce可以非同步方式讀取多個Redis執行個體。 將設為 `true` 以自動使用 _唯讀_ 連線至Redis執行個體，以接收非主節點上的唯讀流量。 此連線透過負載平衡來改善效能，因為只有一個節點處理讀寫流量。 將設為 `false` 以從移除任何現有的唯讀連線陣列 `env.php` 檔案。

```yaml
stage:
  deploy:
    REDIS_USE_SLAVE_CONNECTION: true
```

您必須在中設定Redis服務 `.magento.app.yaml` 檔案和 `services.yaml` 檔案。

[ECE-Tools 2002.0.18版](../release-notes/cloud-release-archive.md#v2002018) 和之後會使用更多容錯設定。 如果Adobe Commerce無法從Redis讀取資料 _從屬_ 執行個體，則會從Redis讀取資料 _主版_ 執行個體。

唯讀連線無法用於整合環境，或者如果您使用 [`CACHE_CONFIGURATION` 變數](#cache_configuration).

## `RESOURCE_CONFIGURATION`

- **預設** — 未設定
- **版本**—Adobe Commerce 2.1.4和更新版本

將資源名稱對應到資料庫連線。 此設定對應至 `resource` 的區段 `env.php` 檔案。

{{merge-options}}

以下範例會將新值合併至現有設定：

```yaml
stage:
  deploy:
    RESOURCE_CONFIGURATION:
      _merge: true
      default_setup:
        connection: default
```

## `SCD_COMPRESSION_LEVEL`

- **預設**—`4`
- **版本**—Adobe Commerce 2.1.4和更新版本

指定哪些 [gzip](https://www.gnu.org/software/gzip) 壓縮等級(`0` 至 `9`)來使用於壓縮靜態內容； `0` 停用壓縮。

```yaml
stage:
  deploy:
    SCD_COMPRESSION_LEVEL: 5
```

## `SCD_COMPRESSION_TIMEOUT`

- **預設**—`600`
- **版本**—Adobe Commerce 2.1.4和更新版本

當壓縮靜態資產所花的時間超過壓縮逾時限制時，就會中斷部署程式。 設定靜態內容壓縮命令的執行時間上限（秒）。

```yaml
stage:
  deploy:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_MATRIX`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

您可以為每個主題設定多個地區設定。 此自訂功能可減少不必要的佈景主題檔案數目，進而加快部署程式。 例如，您可以部署 _magento/後端_ 英文佈景主題以及其他語言的自訂佈景主題。

以下範例部署 `Magento/backend` 三種地區設定的主題：

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

此外，您也可以選擇 _非_ 部署主題：

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.2.0和更新版本

可讓您增加靜態內容部署的最大預期執行時間。

依預設，Adobe Commerce會將最大預期執行時間設為900秒，但在某些情況下，您可能需要更多時間才能完成雲端專案的靜態內容部署。

```yaml
stage:
  deploy:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **預設**—`false`
- **版本**—Adobe Commerce 2.4.2和更新版本

在部署階段，設定 `SCD_NO_PARENT: true` 因此父系主題的靜態內容不會在部署階段產生。 此設定將部署時間縮到最短，並防止在部署期間靜態內容建置失敗時可能發生的網站停機時間。 另請參閱 [靜態內容部署](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SCD_NO_PARENT: true
```

## `SCD_STRATEGY`

- **預設**—`quick`
- **版本**—Adobe Commerce 2.2.0和更新版本

可讓您自訂 [部署策略](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) 用於靜態內容。 另請參閱 [部署靜態檢視檔案](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

使用這些選項 _僅限_ 如果您有多個地區設定：

- `standard` — 為所有封裝部署所有靜態檢視檔案。
- `quick`—(_預設_)將部署時間縮到最短。
- `compact` — 節省伺服器上的磁碟空間。 在Adobe Commerce 2.2.4版和更早版本中，此設定會覆寫以下專案的值： `scd_threads` ，值為 `1`.

```yaml
stage:
  deploy:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **預設** — 自動
- **版本**—Adobe Commerce 2.1.4和更新版本

設定靜態內容部署的執行緒數目。 預設值是根據偵測到的CPU執行緒計數而設定，不會超過4的值。 增加執行緒數目會加速靜態內容部署；減少執行緒數目會減慢速度。 您可以設定螺紋值，例如：

```yaml
stage:
  deploy:
    SCD_THREADS: 2
```

若要進一步縮短部署時間，請使用 [設定管理](../store/store-settings.md) 使用 `scd-dump` 將靜態部署移至建置階段的命令。

## `SEARCH_CONFIGURATION`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

使用此環境變數，可保留部署間的自訂搜尋服務設定。 例如：

Elasticsearch設定：

```yaml
stage:
  deploy:
   SEARCH_CONFIGURATION:
     engine: elasticsearch
     elasticsearch_server_hostname: http://elasticsearch.internal
     elasticsearch_server_port: '9200'
     elasticsearch_index_prefix: magento2
     elasticsearch_server_timeout: '15'
```

OpenSearch設定（適用於Commerce 2.4.6和更新版本）：

```yaml
stage:
  deploy:
   SEARCH_CONFIGURATION:
     engine: opensearch
     opensearch_server_hostname: 'http://opensearch.internal'
     opensearch_server_port: '9200'
     opensearch_index_prefix: 'magento2'
     opensearch_server_timeout: '15'
```

{{merge-options}}

以下範例會將新值合併至現有設定：

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_port: '9200'
      _merge: true
```

## `SESSION_CONFIGURATION`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

設定Redis工作階段存放區。 需要 `save`， `redis`， `host`， `port`、和 `database` 作業階段儲存體變數的選項。 例如：

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      redis:
        bot_first_lifetime: 100
        bot_lifetime: 10001
        database: 0
        disable_locking: 1
        host: redis.internal
        max_concurrency: 10
        max_lifetime: 10001
        min_lifetime: 100
        port: 6379
      save: redis
```

{{merge-options}}

以下範例會將新值合併至現有設定：

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      _merge: true
      redis:
        max_concurrency: 10
```

## `SKIP_SCD`

- **預設**— _未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

將設為 `true` 以在部署階段期間略過靜態內容部署。

在部署階段，設定 `SKIP_SCD: true` 以便在部署階段不會進行靜態內容建置。 此設定將部署時間縮到最短，並防止在部署期間靜態內容建置失敗時可能發生的網站停機時間。 另請參閱 [靜態內容部署](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SKIP_SCD: true
```

## `UPDATE_URLS`

- **預設**—`true`
- **版本**—Adobe Commerce 2.1.4和更新版本

部署時，將資料庫中的Adobe Commerce基底URL取代為指定的專案URL。 [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) 變數中。 此設定對於本機開發非常有用，因為在本機環境中會設定基本URL。 當您部署至雲端環境時，URL會更新，以便您可以使用專案URL存取店面和管理員。

如果您在部署至Pro或Starter Staging和生產環境時必須更新URL，請使用 [`FORCE_UPDATE_URLS`](#force_update_urls) 變數中。

```yaml
stage:
  deploy:
    UPDATE_URLS: false
```

## `VERBOSE_COMMANDS`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

啟用或停用 [Symfony](https://symfony.com/doc/current/console/verbosity.html) 偵錯詳細資訊層級 `bin/magento` 在部署階段執行的CLI命令。

>[!NOTE]
>
>若要使用VERBOSE_COMMANDS設定來控制命令輸出中成功和失敗的細節 `bin/magento` CLI命令，您必須設定 [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug`.

選擇記錄中提供的詳細資訊等級：

- `-v`=一般輸出
- `-vv`=更多詳細資訊輸出
- `-vvv` =詳細輸出適用於偵錯

```yaml
stage:
  deploy:
    VERBOSE_COMMANDS: "-vv"
```
