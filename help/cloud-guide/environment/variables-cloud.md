---
title: 雲端專用變數
description: 請參閱雲端基礎結構上Adobe Commerce專屬的環境變數清單。
feature: Cloud, Configuration
recommendations: noDisplay, catalog
role: Developer
exl-id: 84b7c0fc-f0b0-4ff5-9f33-9d17180a9306
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# 雲端專用變數

雲端基礎結構上Adobe Commerce專屬的環境變數使用 `MAGENTO_CLOUD_*` 前置詞：

| 變數 | 說明 |
| -------- | --------------- |
| `MAGENTO_CLOUD_APP_DIR` | 應用程式目錄的絕對路徑。 |
| `MAGENTO_CLOUD_APPLICATION` | 說明應用程式的base64編碼JSON物件。 它將對應到 `.magento.app.yaml` 檔案內容且具有子索引鍵。 |
| `MAGENTO_CLOUD_APPLICATION_NAME` | 在中設定的應用程式名稱 `.magento.app.yaml` 檔案。 |
| `MAGENTO_CLOUD_DOCUMENT_ROOT` | 網頁主目錄的絕對路徑（如果適用）。 |
| `MAGENTO_CLOUD_ENVIRONMENT` | 環境分支的名稱。 |
| `MAGENTO_CLOUD_PROJECT` | 專案識別碼。 |
| `MAGENTO_CLOUD_RELATIONSHIPS` | 代表索引鍵（關係名稱）和值（關係配對陣列）端點定義的base64編碼JSON物件。 每個關係端點定義都是URL的分解形式。 它有 `scheme`， a `host`， a `port`、和 _（選擇性）_ a `username`， `password`， `path`以及中一些其他資訊 `query`. |
| `MAGENTO_CLOUD_ROUTES` | 說明環境中定義的路由 `.magento/routes.yaml` 檔案。 |
| `MAGENTO_CLOUD_TREE_ID` | 應用程式的樹狀結構ID，對應至Git中樹狀結構的SHA。 |
| `MAGENTO_CLOUD_VARIABLES` | 具有索引鍵值配對的base64編碼JSON物件，例如 `"key":"value"`. |
| `MAGENTO_CLOUD_LOCKS_DIR` | 提供雲端基礎結構上鎖定提供者的掛載點路徑。 鎖定提供者可防止啟動重複的cron作業和cron群組。 |

>[!WARNING]
>
>若要將環境變數新增至 [覆寫組態設定](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) 使用 [[!DNL Cloud Console]](../project/overview.md)，您必須在變數名稱前面加上 `env:` 如下列範例所示：
>
>![環境變數範例](../../assets/set-env-variable-ui.png)

由於值會隨著時間變更，因此最好在執行階段檢查變數，並使用它來設定應用程式。 例如，使用 `MAGENTO_CLOUD_RELATIONSHIPS` 變數來擷取環境相關的關係，如下所示：

```php
<?php
/**
  * Get relationships information from cloud environment variable.
  *
  * @return mixed
  */
    protected function getRelationships()
    {
        return json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]), true);
    }
```

## 檢視環境變數

您可以使用 `env:config:show` 命令來源 [此 `ece-tools` 封裝](../dev-tools/package-overview.md) 顯示目前環境的變數清單。

```bash
php ./vendor/bin/ece-tools env:config:show variables
```

的輸出範例 `variables` 選項：

```terminal
Magento Cloud Environment Variables:
+-----------------------------------+----------------------------------+
| Variable name                     | Value                            |
+-----------------------------------+----------------------------------+
| ADMIN_EMAIL                       | commerceadmin@company.com        |
| ADMIN_PASSWORD                    | 123123q                          |
+-----------------------------------+----------------------------------+
```
