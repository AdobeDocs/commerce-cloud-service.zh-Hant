---
title: 設定環境
description: 瞭解如何使用環境變數，在雲端基礎結構環境（包括Pro測試和生產）上跨所有Commerce設定建置和部署動作。
feature: Cloud, Build, Configuration, Deploy, SCD
role: Developer
exl-id: 66e257e2-1eca-4af5-9b56-01348341400b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# 設定用於部署的環境變數

此 `.magento.env.yaml` 檔案會使用環境變數，集中管理所有環境的建置和部署動作，包括Pro測試和生產。 若要在每個環境中設定唯一的動作，您必須在每個環境中修改此檔案。

>[!TIP]
>
>YAML檔案區分大小寫，不允許使用索引標籤。 請留意在整個過程中使用一致的縮排 `.magento.env.yaml` 檔案或您的設定可能無法如預期運作。 檔案和範例檔案中的範例使用 _雙空格鍵_ 縮排。 使用 [ece-tools validate指令](#validate-configuration-file) 以檢查您的設定。

## 檔案結構

此 `.magento.env.yaml` 檔案包含兩個區段： `stage` 和 `log`. 此 `stage` 區段控制階段期間發生的動作 [雲端部署程式](../deploy/process.md).

- `stage` — 使用階段區段來定義下列部署階段的特定動作：
   - `global` — 控制建置、部署和部署後階段的動作。 您可以在「建置」、「部署」和「部署後」區段中覆寫這些設定。
   - `build` — 僅控制建置階段中的動作。 如果您未在此區段中指定設定，則建置階段會使用全域區段的設定。
   - `deploy` — 僅控制部署階段中的動作。 如果您未在此段落中指定設定，部署階段會使用全域段落中的設定。
   - `post-deploy` — 控制動作 _晚於_ 部署您的應用程式和 _晚於_ 容器開始接受連線。
- `log` — 使用記錄區段來設定 [通知](set-up-notifications.md)，包括通知型別和詳細資訊層級。
   - `slack` — 設定要傳送給Slack機器人的訊息。
   - `email` — 設定要傳送給一或多個電子郵件收件者的電子郵件。
   - [記錄處理常式](log-handlers.md) — 設定傳送至遠端記錄伺服器的軟硬體應用程式訊息。

### 環境變數

此 `ece-tools` 套件會在 `env.php` 根據下列專案的值的檔案： [雲端變數](variables-cloud.md)，在中設定的變數 [!DNL Cloud Console]，以及 `.magento.env.yaml` 組態檔。 中的環境變數 `.magento.env.yaml` 檔案透過覆寫您現有的Commerce設定來自訂雲端環境。 若預設值為 `Not Set`，然後 `ece-tools` 封裝取用 **否** 動作並使用 [!DNL Commerce] 預設值或MAGENTO_CLOUD_RELATIONSHIPS設定的值。 若已設定預設值，則 `ece-tools` 封裝會設定該預設值。

下列主題包含您可在下列專案中使用的所有變數的詳細定義，例如預設值是否已設定 `.magento.env.yaml` 檔案：

- [全域](variables-global.md) — 變數控制每個階段的動作：建置、部署和部署後
- [建置](variables-build.md) — 變數控制建置動作
- [部署](variables-deploy.md) — 變數控制部署動作
- [部署後](variables-post-deploy.md) — 變數控制部署後的動作

### 從CLI建立組態檔

您可以產生 `.magento.env.yaml` 使用以下專案的雲端環境設定檔 `ece-tools` 命令。

>建立組態檔

```bash
php ./vendor/bin/ece-tools cloud:config:create `<configuration-json>`
```

>更新設定檔案中的值

```bash
php ./vendor/bin/ece-tools cloud:config:update `<configuration-json>`
```

兩個命令都需要單一引數：為至少一個組建、部署或部署後變數指定值的JSON格式陣列。 例如，下列指令會設定 `SCD_THREADS` 和 `CLEAN_STATIC_FILES` 變數：

```bash
php vendor/bin/ece-tools cloud:config:create '{"stage":{"build":{"SCD_THREADS":5}, "deploy":{"CLEAN_STATIC_FILES":false}}}'
```

並建立 `.magento.env.yaml` 檔案的下列設定：

```yaml
stage:
  build:
    SCD_THREADS: 5
  deploy:
    CLEAN_STATIC_FILES: false
```

您可以使用 `cloud:config:update` 命令以更新新檔案。 例如，下列指令會變更 `SCD_THREADS` 值並新增 `SCD_COMPRESSION_TIMEOUT` 設定：

```bash
php vendor/bin/ece-tools cloud:config:update '{"stage":{"build":{"SCD_THREADS":3, "SCD_COMPRESSION_TIMEOUT":1000}}}'
```

更新的檔案包含以下設定：

```yaml
stage:
  build:
    SCD_THREADS: 3
    SCD_COMPRESSION_TIMEOUT: 1000
  deploy:
    CLEAN_STATIC_FILES: false
```

### 驗證組態檔

使用下列專案 `ece-tools` 命令來驗證 `.magento.env.yaml` 將變更推送至遠端雲端環境前的設定檔。

```bash
php ./vendor/bin/ece-tools cloud:config:validate
```

下列範例回應提供要修正的專案清單：

```terminal
Environment configuration is not valid. Correct the following items in your .magento.env.yaml file:
The SCD_THREADS variable contains an invalid value of type string. Use the following type: integer.
The SCD_STRATEGY variable contains an invalid value fast. Use one of the available value options: compact, quick, standard.
The NOT_EXIST_OPTION variable is not allowed in configuration.
```

## PHP常數

您可以在下列位置使用PHP常數： `.magento.env.yaml` 檔案定義，而非硬式編碼值。 以下範例會定義 `driver_options` 使用PHP常數：

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          driver_options:
            !php/const:\PDO::MYSQL_ATTR_LOCAL_INFILE : 1
        indexer:
          driver_options:
            !php/const:\PDO::MYSQL_ATTR_LOCAL_INFILE : 1
      _merge: true
```

>[!WARNING]
>
>使用時常數剖析無法運作 `symfony/yaml` 3.2之前的套件版本。

## 錯誤處理

當失敗是由於 `.magento.env.yaml` 組態檔時，您會收到錯誤訊息。 例如，下列錯誤訊息會對每個具有非預期值的專案顯示建議變更清單，有時會提供有效選項：

```terminal
- Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:
  Item CRON_CONSUMERS_RUNNER is not supposed to be in stage build. Please move it to one of possible stages: global, deploy
  Item SKIP_SCD has unexpected type string. Please use one of next types: boolean
  Item VERBOSE_COMMANDS has unexpected type boolean. Please use one of next types: string
  Item SKIP_HTML_MINIFICATION has unexpected type string. Please use one of next types: boolean
  Item CRON_CONSUMERS_RUNNER has unexpected type boolean. Please use one of next types: array
  Item VAR_WARM_UP_PAGES is not allowed in configuration.
  Item WARM_UP_PAGES has unexpected type string. Please use one of next types: array
```

進行任何更正、認可及推送變更。 如果您沒有收到錯誤訊息，則對設定檔案的變更會通過驗證。

## 設定管理最佳化

如果您在傾印設定後啟用了「設定管理」，您應該將SCD_*變數從部署移至建置階段。 另請參閱 [靜態內容部署策略](../deploy/static-content.md).

>組態管理之前：

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
    REDIS_USE_SLAVE_CONNECTION: 1
```

>啟用「組態管理」後，將SCD_*變數移至建置階段：

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    REDIS_USE_SLAVE_CONNECTION: 1
  build:
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
```
