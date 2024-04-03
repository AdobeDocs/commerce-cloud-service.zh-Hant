---
title: 全域變數
description: 請參閱環境變數清單，這些變數可控制Adobe Commerce對雲端基礎結構部署程式的動作。
feature: Cloud, Configuration, Build, Deploy, Eventing, Logs, SCD
recommendations: noDisplay, catalog
role: Developer
exl-id: 04c2861d-746d-42d4-a678-f6c7b464eb51
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# 全域變數

全域變數可控制每個階段的 [!DNL Commerce] 部署程式：建置、部署和部署後。 由於全域變數會影響每個階段，因此您必須在 `global` 的階段 `.magento.env.yaml` 檔案：

```yaml
stage:
  global:
    GLOBAL_VARIABLE_NAME: value
```

如需自訂建置和部署程式的詳細資訊：

- [部署設定](configure-env-yaml.md)
- [部署流程](../deploy/process.md)

## `ENABLE_EVENTING`

- **預設**-_未設定_
- **版本**—Adobe Commerce 2.4.5和更新版本

當設定為 `true`，可讓cron執行訊息佇列取用者。 Adobe Commerce的Adobe I/O事件使用訊息佇列來加速傳送關鍵事件。

Adobe建議您同時新增 [`CRON_CONSUMERS_RUNNER`](./variables-deploy.md#cron_consumers_runner) 變數至 `deploy` 的階段 `.magento.env.yaml` 檔案與 `cron_run` 設為 `true`.

下列範例顯示已完整設定的 `ENABLE_EVENTING` 變數中。

```yaml
stage:
  global:
    ENABLE_EVENTING: true
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 0
      consumers: []
```

## ENABLE_WEBHOOKS

- **預設**-_未設定_
- **版本**—Adobe Commerce 2.4.4和更新版本

當設定為 `true`，會啟用Commerce Webhook。 webhook會在外部端點上執行，例如App Builder執行階段動作或協力廠商詳細目錄管理系統。 此 [_Webhooks指南_](https://developer.adobe.com/commerce/extensibility/webhooks) 詳細說明此功能。

```yaml
stage:
  global:
    ENABLE_WEBHOOKS: true
```

## `MIN_LOGGING_LEVEL`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

覆寫所有輸出資料流的最低記錄層級，而不變更程式碼，這在疑難排解部署問題時很有幫助。 例如，如果您的部署失敗，您可以使用此變數在全域提高記錄粒度。 另請參閱 [記錄層級](log-handlers.md#log-levels). 此 `min_level` 記錄處理常式中的值會覆寫此設定。

```yaml
stage:
  global:
    MIN_LOGGING_LEVEL: debug
```

>[!WARNING]
>
>的設定 `MIN_LOGGING_LEVEL` 變數不會變更檔案處理常式的記錄層級組態，其設定為 `debug` 依預設。

## `SCD_ON_DEMAND`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

當使用者(SCD)要求時，啟用產生靜態內容的功能。 隨選靜態內容最適合用於開發和測試工作流程，因為這可縮短部署時間。

使用預先載入快取 [`post_deploy` 勾點](../application/hooks-property.md) 減少網站停機時間。 快取預熱僅適用於包含中繼和生產環境的Pro專案 [!DNL Cloud Console] 和適用於入門專案。 新增 `SCD_ON_DEMAND` 環境變數至 `global` 中的階段 `.magento.env.yaml` 檔案：

```yaml
stage:
  global:
    SCD_ON_DEMAND: true
```

此 `SCD_ON_DEMAND` 變數會以兩個階段（建置和部署）略過SCD，並清除 `pub/static` 和 `var/view_preprocessed` 資料夾，並將下列內容寫入 `app/etc/env.php` 檔案：

```php?start_inline=1
return array(
   ...
   'static_content_on_demand_in_production' => 1,
   ...
);
```

## `SCD_MAX_EXECUTION_TIME`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.2.0和更新版本

可讓您增加靜態內容部署的最大預期執行時間。

依預設，Adobe Commerce會將最大預期執行時間設為900秒，但在某些情況下，您可能需要更多時間才能完成雲端專案的靜態內容部署。

```yaml
stage:
  global:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.4.2和更新版本

將設為 `true` 以防止在建置和部署階段期間為父級主題產生靜態內容。 當此選項設定為 `true`，產生的靜態內容較少，因此可縮短您的整體建置和部署時間。

```yaml
stage:
  global:
    SCD_NO_PARENT: true
```

## `SCD_USE_BALER`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.3.0和更新版本

[貝勒](https://github.com/magento/baler) 是一個模組，可掃描您產生的JavaScript程式碼並建立最佳化的JavaScript套件組合。 將最佳化的套件組合部署至您的網站，可以減少載入網站時的網路要求數目，並改善頁面載入時間。

將設為 `true` 以在執行靜態內容部署後執行Baler。

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>使用此功能之前，請先安裝並設定Baler模組。 因為Baler是Alpha發行版本，僅在中繼環境中啟用此選項。

## `SKIP_HTML_MINIFICATION`

- **預設**：
   - `true`—for `ece-tools` 2002.0.13和更新版本
   - `false` — 適用於舊版的 `ece-tools`
- **版本**—Adobe Commerce 2.1.4和更新版本

啟用或停用將靜態檢視檔案複製到 `<magento_root>/init/` 建置階段結束時的目錄。 如果設為 `true`，不會複製檔案，且可依請求提供HTML縮制。 將此值設為 `true` 以減少部署到中繼和生產環境時的停機時間。

- **`false`** — 複製 `view_preprocessed` 目錄到 `<magento_root>/init/` 目錄，並還原中的目錄 `<magento_root>/var` 部署階段開始的目錄。
- **`true`** — 啟用隨選HTML縮制；執行 _非_ 複製 `<magento_root>var/view_preprocessed` 至 `<magento_root>/init/` 建置階段結束時的目錄。

新增 `SKIP_HTML_MINIFICATION` 環境變數至 `global` 中的階段 `.magento.env.yaml` 檔案：

```yaml
stage:
  global:
    SKIP_HTML_MINIFICATION: true
```

## `X_FRAME_CONFIGURATION`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

使用 `X_FRAME_CONFIGURATION` 變數變更 [`X-Frame-Options`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/security/xframe-options.html) Adobe Commerce網站的標題設定。 此設定可控制瀏覽器如何呈現 `<frame>`， `<iframe>`，或 `<object>`. 使用下列其中一個選項：

- `DENY` — 頁面無法顯示在框架中。
- `SAMEORIGIN`—(預設的Adobe Commerce設定。) 頁面只能在與頁面本身相同原點的框架中顯示。

>[!WARNING]
>
>此 `ALLOW-FROM <uri>` 選項已淘汰，因為Adobe Commerce支援的瀏覽器不再支援它。 另請參閱 [瀏覽器相容性](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility).

新增 `X_FRAME_CONFIGURATION` 環境變數至 `global` 中的階段 `.magento.env.yaml` 檔案：

```yaml
stage:
  global:
    X_FRAME_CONFIGURATION: SAMEORIGIN
```
