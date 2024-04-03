---
title: 靜態內容部署
description: 瞭解在Adobe Commerce上雲端基礎結構專案部署靜態內容（例如影像、指令碼和CSS）的策略。
feature: Cloud, Build, Deploy, SCD
exl-id: e128d0d5-1326-44e5-a822-009e11ba105f
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# 靜態內容部署策略

靜態內容部署(SCD)對存放區部署程式有重大影響，這取決於要產生多少內容（例如影像、指令碼、CSS、影片、主題、區域設定和網頁）以及何時產生內容。 例如，預設策略會在以下期間產生靜態內容： [部署階段](process.md#deploy-phase-deploy-phase) 當網站處於維護模式時，然而，此部署策略需要一些時間才能將內容直接寫入已掛載的 `pub/static` 目錄。 您有多種選項或策略可協助您根據需求改善部署時間。

## 最佳化JavaScript和HTML內容

您可以使用套件和縮制在靜態內容部署期間建置最佳化的JavaScript和HTML內容。

### 將內容縮制

如果您略過複製中的靜態檢視檔案，則可以改善部署程式期間的SCD載入時間。 `var/view_preprocessed` 目錄並產生 _縮制_ 提出要求時HTML。 您可以設定 [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skiphtmlminification) 全域環境變數至 `true` 在 `.magento.env.yaml` 檔案。

>[!NOTE]
>
>從 `ece-tools` 套裝程式2002.0.13版，SKIP_HTML_MINIFICATION變數的預設值設為 `true`.

您可以儲存 **更多** 減少不必要的佈景主題檔案數目，以節省部署時間和磁碟空間。 例如，您可以部署 `magento/backend` 英文佈景主題以及其他語言的自訂佈景主題。 您可以使用這些佈景主題設定 [SCD_MATRIX](../environment/variables-deploy.md#scdmatrix) 環境變數。

## 選擇部署策略

部署策略會因您選擇在期間是否產生靜態內容而有所不同 _版本編號_ 階段， _部署_ 階段，或 _隨選_. 如下圖所示，在部署階段期間產生靜態內容是最不理想的選擇。 即使使用最小化HTML，每個內容檔案也必須複製到已掛載的 `~/pub/static` 目錄，這可能需要很長的時間。 隨選產生靜態內容似乎是最佳選擇。 不過，如果內容檔案不存在於其產生之快取中，則會在請求該檔案時增加使用者體驗的載入時間。 因此，在建置階段期間產生靜態內容是最理想的作法。

![SCD載入比較](../../assets/scd-load-times.png)

### 在建置時設定SCD

在建置階段期間使用最小化HTML產生靜態內容是以下專案的最佳設定： [**零停機時間** 部署](reduce-downtime.md)，也稱為 **理想狀態**. 它不會將檔案複製到已掛載的磁碟機，而是會從以下位置建立符號連結： `./init/pub/static` 目錄。

產生靜態內容需要存取主題和區域設定。 Adobe Commerce會將主題儲存在檔案系統中（可在建置階段存取），但Adobe Commerce會將地區設定儲存在資料庫中。 資料庫為 _非_ 建置階段期間提供。 若要在建置階段期間產生靜態內容，您必須使用 `config:dump` 中的命令 `ece-tools` 封裝以將語言環境移至檔案系統。 它會讀取地區設定並將它們儲存在 `app/etc/config.php` 檔案。

**若要設定您的專案以在建置時產生SCD**：

1. 在本機工作站上，變更至專案目錄。
1. 使用SSH登入遠端環境。

   ```bash
   magento-cloud ssh
   ```

1. 將地區設定移至檔案系統，然後更新 [`config.php` 檔案](../development/commerce-version.md#create-a-configphp-file).

1. 此 `.magento.env.yaml` 設定檔案應包含以下值：

   - [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skip_html_minification) 是 `true`
   - [SKIP_SCD](../environment/variables-build.md#skip_scd) 在建置階段為 `false`
   - [SCD_STRATEGY](../environment/variables-build.md#scd_strategy) 是 `compact`

1. 驗證 [部署後勾點](../application/hooks-property.md) 在 `.magento.app.yaml` 檔案。

1. 執行 [適用於理想狀態的智慧型精靈](smart-wizards.md).

   ```bash
   php ./vendor/bin/ece-tools wizard:ideal-state
   ```

### 隨選設定SCD

針對整合環境中的開發工作流程，建議依需求產生SCD。 這可縮短部署時間，讓您快速檢閱實作並執行整合測試。 啟用 [SCD_ON_DEMAND](../environment/variables-global.md#scdondemand) 的環境變數 `.magento.env.yaml` 檔案。 SCD_ON_DEMAND變數會覆寫與SCD相關的所有其他組態，並從 `~/pub/static` 目錄。

使用SCD隨選策略時，有助於使用您預期請求的頁面（例如首頁）預先載入快取。 將您的預期頁面清單新增至 [WARMUP_PAGE](../environment/variables-post-deploy.md#warmuppages) 環境變數（在的部署後階段） `.magento.env.yaml` 檔案。

>[!WARNING]
>
>請勿在生產環境中使用SCD隨選策略。

### 跳過SCD

有時您可以選擇完全略過產生靜態內容。 您可以設定 [SKIP_SCD](../environment/variables-build.md#skipscd) 全域階段中的環境變數，以忽略與SCD相關的其他設定。 這不會影響中的現有內容 `~/pub/static` 目錄。
