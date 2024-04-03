---
title: 智慧型精靈
description: 瞭解如何使用智慧型精靈，評估雲端基礎結構專案上的Adobe Commerce是否遵循部署最佳實務。
feature: Cloud, Build, Deploy, SCD
exl-id: eb79431c-8835-4ae4-b453-9c4932c5d5ac
source-git-commit: 225fba1acfd8b3ce4d7ce989c7851e7b0b218680
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 智慧型精靈

智慧型精靈可協助您判斷雲端設定是否遵循最佳實務。 可用的精靈可協助進行下列設定：

- 最理想的狀態，可將部署停機時間降到最低
- 資料庫和Redis的負載平衡設定
- 隨選、建置階段或部署階段的靜態內容部署(SCD)

每個智慧型精靈指令都會提供驗證回應，以及適當設定的建議（如適用）。

| 命令 | 說明 |
| ------- | ------------|
| `wizard:ideal-state` | 檢查SCD是否位於 _版本編號_ 階段， `SKIP_HTML_MINIFICATION` 變數為 `true`，以及在雲端環境中設定的post_deploy掛接。 不用於本機開發環境。 |
| `wizard:master-slave` | 檢查 `REDIS_USE_SLAVE_CONNECTION` 變數和 `MYSQL_USE_SLAVE_CONNECTION` 變數為 `true`. |
| `wizard:scd-on-demand` | 檢查 `SCD_ON_DEMAND` 全域環境變數為 `true`. |
| `wizard:scd-on-build` | 檢查 `SCD_ON_DEMAND` 全域環境變數為 `false` 和 `SKIP_SCD` 環境變數為 `false` 針對 _版本編號_ 階段。 驗證 `config.php` 檔案包含商店、商店群組和網站的資訊。 |
| `wizard:scd-on-deploy` | 檢查 `SCD_ON_DEMAND` 全域環境變數為 `false` 和 `SKIP_SCD` 環境變數為 `false` 針對 _部署_ 階段。 驗證 `config.php` 檔案會 _NOT_ 包含商店、商店群組和網站清單及相關資訊。 |

例如，您可以驗證您的設定是否正確啟用SCD隨選功能：

```bash
./vendor/bin/ece-tools wizard:scd-on-demand
```

成功的設定傳回：

```terminal
SCD on-demand is enabled
```

失敗的設定傳回：

```terminal
SCD on-demand is disabled
```

## 驗證理想的設定

此 _理想_ 您的雲端專案設定可讓快取暖身分並在使用者要求時產生靜態內容，藉此將部署停機時間降至最低。 此精靈會在部署過程中自動執行。 如果您的雲端未針對此設定 _理想狀態_，接著您會收到類似下列的訊息：

```terminal
- SCD on build is not configured
- Post-deploy hook is not configured
- Skip HTML minification is disabled

Ideal state is not configured
```

根據輸出，您需要對設定進行下列更正：

1. 啟用略過HTML縮制變數。

   > .magento.env.yaml

   ```yaml
   stage:
     global:
       SKIP_HTML_MINIFICATION: true
   ```

1. 設定部署後鉤點。

   > .magento.app.yaml

   ```yaml
       post_deploy: |
           php ./vendor/bin/ece-tools post-deploy
   ```

1. 推送您的程式碼變更，然後再次執行測試。 當您的設定為 _理想_，您會收到下列訊息。

   ```terminal
   Ideal state is configured
   ```
