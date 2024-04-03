---
title: 部署流程
description: 瞭解部署如何適用於Adobe Commerce的雲端基礎結構專案。
feature: Cloud, Build, Deploy, SCD
exl-id: 378fa290-5a71-4ac2-816a-a7c837e45b2f
source-git-commit: 3d9e3294872fedcc43744f54a71c71d8951ed853
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# 部署流程

當您執行環境的合併、推播或同步化作業，或當您觸發 [手動重新部署](../dev-tools/cloud-cli-overview.md#redeploy-the-environment). 部署過程需要時間，但最佳化部署的方法取決於您是開發、測試還是使用即時網站。 最明顯的是，您可以控制 [靜態內容部署](static-content.md).

部署流程有三個不同的階段：建置、部署和部署後。 每個階段會使用有限的資源執行特定動作：

## ![建置階段](../../assets/status-build.png) 建置階段

此 _版本編號_ 階段會為組態檔中定義的服務組裝容器，並根據 `composer.lock` 檔案中定義的建置掛接，並執行 `.magento.app.yaml` 檔案。 由於無法連線到任何服務或存取資料庫，所以組建階段會視環境所限定的資源而定。

## ![部署階段](../../assets/status-deploy.png) 部署階段

此 _部署_ 階段會暫時保留傳入的請求，並將網站轉換為 [維護模式](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html). 部署階段會使用新的容器，並在掛載檔案系統後開啟網路連線，並啟動中定義的服務。 `relationships` 的區段 `.magento.app.yaml` 檔案中定義的部署鉤點，並執行 `.magento.app.yaml` 檔案。 一切都是 _唯讀_，但中定義的目錄除外 `.magento.app.yaml` 檔案。 根據預設， [`mounts` 屬性](../application/properties.md#mounts) 包含下列目錄：

- `app/etc` — 包含 `env.php` 和 `config.php` 組態檔
- `pub/media` — 包含所有媒體資料，例如產品或類別
- `pub/static` — 包含產生的靜態檔案
- `var` — 包含執行期間建立的暫存檔案

所有其他目錄具有唯讀許可權。 當新網站從維護模式轉換出，並解除對傳入請求的臨時保留時，會在部署階段結束時變為使用中。

在部署階段， `app/etc/config.php` 和 `app/etc/env.php` 部署組態檔會以BAK副檔名儲存。 另請參閱 [商店設定](../store/store-settings.md#restore-configuration-files) 以瞭解如何還原這些檔案。

## ![部署後階段](../../assets/status-post-deploy.png) 部署後階段

此 _部署後_ 階段會執行中定義的部署後鉤點 `.magento.app.yaml` 檔案。 在此階段執行任何動作都可能會影響網站效能；不過，您可以使用 [WARMUP_PAGE](../environment/variables-post-deploy.md#warmuppages) 環境變數填入快取。

## ![驗證狀態](../../assets/status-verify.png) 驗證設定

您可以透過執行 [智慧型精靈](smart-wizards.md).

>[!NOTE]
>
>替換為 `ece-tools` 2002.1.0和更新版本，您可以使用情境式部署功能，在雲端基礎結構專案上自訂Adobe Commerce的建置、部署和部署後程式。 另請參閱 [以案例為基礎的部署](scenario-based.md).
