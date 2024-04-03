---
title: ece-tools的發行說明封存
description: 瞭解ece-tools的封存改善。
hide: true
hidefromtoc: true
recommendations: noDisplay, noCatalog
exl-id: 96663d2f-ef00-4490-ad2e-06e8041b228e
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '7147'
ht-degree: 0%

---

# ece-tools的發行說明封存

>[!NOTE]
>
>這些發行說明提供以下專案的資訊和更新： `ece-tools` v2002.0.22及更高版本。 另請參閱 [Cloud Tools Suite發行說明](cloud-tools-suite.md) 以取得的最新更新 `ece-tools` 和其他雲端套件。

## v2002.0.22

此 `ece-tools` 2002.0.22發行版本變更 `ece-tools` 此套件與的發行版本脫鉤 `Adobe Commerce on cloud infrastructure` ECE-Tools發行版本的修補程式。 自此發行版本開始，我們將使用 [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) 套件，此為新的相依性 `ece-tools` 封裝。 我們進行這些變更，以降低排程版本更新及處理社群貢獻的複雜性。

- ![新圖示](../../assets/new.svg) **ECE-Tools套件的變更**

   - ![新圖示](../../assets/new.svg) 已將Adobe Commerce修補程式從 `ece-tools` 封裝到新的 [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) Composer套件。

   - ![新圖示](../../assets/new.svg) 已更新 `composer.json` 的檔案 `ece-tools` 套件以新增的相依性 `magento/magento-cloud-patches` v1.0.0套件。

   - ![修正圖示](../../assets/fix.svg) 已修正導致 `ece-tools` 修補程式，以在僅限安全性的發行版本上套用修補程式集時中斷（從2.3.2-p2版及更新版本開始）。 針對以下專案採用的新版本化Scheme已引入此問題 [僅限安全性的修補程式](https://devdocs.magento.com/guides/v2.3/release-notes/bk-release-notes.html#security-only-patches).<!--MAGECLOUD-4661-->

- ![修正圖示](../../assets/fix.svg) **修補程式和重要修正** — 使用更新您的雲端環境 `ece-tools` 2002.0.22版，可套用下列修補程式和重要修正。 這些修補程式包含在 `magento/magento-cloud-patches` v1.0.0套件。

   - ![修正圖示](../../assets/fix.svg) **2.3.1.x和2.3.2.x版本的Page Builder安全性修補程式** — 修正Page Builder預覽中，未經驗證的使用者可存取某些範本化方法的問題，這些方法可用來透過網路(RCE)觸發任意程式碼執行，進而導致全域資訊洩漏。 將不受支援的頁面產生器版本搭配Adobe Commerce版本2.3.1和2.3.2使用時，可能會發生此問題。<!--MAGECLOUD-4649-->

   - ![修正圖示](../../assets/fix.svg) **MSI修補程式** — 修正使用預設庫存設定來管理庫存時，導致索引錯誤和效能問題的問題。<!--MAGECLOUD-4428-->

   - ![修正圖示](../../assets/fix.svg) **新郵件介面的向下相容性** — 修正因下列原因造成的回溯不相容問題： `Magento\Framework\Mail\EmailMessageInterface` Adobe Commerce v2.3.3中引入的PHP介面。在此修補程式的範圍內，新的 `EmailMessageInterface` 繼承自舊的 `MessageInterface`，而Adobe Commerce核心模組將恢復為相依於 `MessageInterface`.<!--MAGECLOUD-4422-->

   - ![修正圖示](../../assets/fix.svg) **目錄分頁在Elasticsearch6.x上無法運作** — 修正搜尋結果分頁的重要問題，此問題會影響使用Elasticsearch6.x做為目錄搜尋引擎的客戶。<!--MAGECLOUD-4448-->

## v2002.0.21

- ![新圖示](../../assets/new.svg) **Docker更新**—

   - ![新圖示](../../assets/new.svg) **新Docker映像** — 由2.3.3版及更新版本支援<!-- MAGECLOUD-3345 -->

      - PHP 7.3版。<!-- MAGECLOUD-4017 -->

      - 清漆快取6.2.0<!-- MAGECLOUD-4017 -->

   - ![新圖示](../../assets/new.svg) 新增支援以套用中指定的自訂掛接設定 `.magento.app.yaml` 在Docker環境中。 以前，Docker環境僅支援預設掛接配置。<!-- MAGECLOUD-3505-->

   - ![新圖示](../../assets/new.svg) Docker構建期間不再生成Docker ENV檔案，並且 `docker:config:convert` 命令已過時。 對應的資料現在儲存在 `docker-compose.yml` 檔案。<!-- MAGECLOUD-3816-->

   - ![新圖示](../../assets/new.svg) **已更新PHP影像** — 將Node.js新增到PHP Docker映像以支援node、npm和grunt-cli功能。<!-- MAGECLOUD-3953 -->

- ![新圖示](../../assets/new.svg) **環境變數更新**-

   - ![新圖示](../../assets/new.svg) 已新增 **LOCK_PROVIDER** 部署變數來設定鎖定提供者，以防止啟動重複的cron作業和cron群組。 請參閱中的變數說明 [部署變數](../environment/variables-deploy.md#lock_provider) 主題。<!-- MAGECLOUD-4052 -->

   - ![新圖示](../../assets/new.svg) 已新增 **CONSUMERS_WAIT_FOR_MAX_MESSAGES** 環境變數，可設定消費者使用時如何處理來自訊息佇列的訊息。 `CRON_CONSUMERS_RUNNER` 用於管理cron工作的環境變數。 請參閱中的變數說明 [部署變數](../environment/variables-deploy.md#consumers_wait_for_max_messages) 主題。<!-- MAGECLOUD-4071 -->

   - ![修正圖示](../../assets/fix.svg) 修正可能導致資料庫死結錯誤的問題，當 `consumers_runner` cron作業會在不同節點上啟動相同使用者的多個執行個體。 現在，如果您已啟用 [**CRON_CONSUMERS_RUNNER**](../environment/variables-deploy.md#cron_consumers_runner) 在您的環境中部署變數， `consumers_runner` 工作使用 `single-thread` 僅在一個節點上啟動每個取用者的一個執行個體的選項。<!-- MAGECLOUD-3913 -->

   - ![修正圖示](../../assets/fix.svg) 已修正影響 [**WARMUP_PAGE**](../environment/variables-post-deploy.md#warm_up_pages) 使用預設商店URL的功能。 現在，如果 `config:show:default-url` 命令無法擷取基底URL，則會使用MAGENTO_CLOUD_ROUTES變數中的URL。<!-- MAGECLOUD-3866 -->

- ![新圖示](../../assets/new.svg) 更新傳回的記錄資訊 `module:refresh` 命令。 現在，您可以在中檢視已啟用模組的詳細清單 `cloud.log` 檔案。<!-- MAGECLOUD-2514 -->

- ![新圖示](../../assets/new.svg) 已針對Adobe Commerce版本與已安裝服務(例如Elasticsearch)之間的相容性問題，改善版本相容性驗證和警告通知。 [!DNL RabbitMQ]、Redis和DB。<!-- MAGECLOUD-3535 -->

- ![新圖示](../../assets/new.svg) 新增對RabitMQ 3.8版的支援。<!-- MAGECLOUD-4674-->

- ![新圖示](../../assets/new.svg) 更新服務相容性的互動式驗證，以反映新的Adobe Commerce 2.3.3和2.2.10版本支援的版本。 另請參閱 [系統需求](https://devdocs.magento.com/guides/v2.4/install-gde/system-requirements.html) 在 _安裝指南_ 推薦的版本。<!-- MAGECLOUD-4018 -->

- ![修正圖示](../../assets/fix.svg) 改善在部署階段的cron工作管理程式嘗試停止已完成的cron工作時，傳回的記錄訊息，以澄清此問題不是錯誤。 已將記錄層級從 `INFO` 至 `DEBUG`.<!-- MAGECLOUD-3653-->

- ![修正圖示](../../assets/fix.svg) 修正執行時的問題 `setup:upgrade` 在作業期間發生失敗時，未中斷部署程式的命令 `app:config:import` 任務。<!-- MAGECLOUD-3806 -->

- ![新圖示](../../assets/new.svg) 將檔案處理常式的預設記錄層級變更為 `debug` 減少日誌中顯示的詳細資訊量 [!DNL Cloud Console]，同時仍提供除錯的詳細資訊。<!-- MAGECLOUD-3871 -->

- ![修正圖示](../../assets/fix.svg) 修正在建置期間導致靜態內容部署錯誤的問題。 安裝及之後 `ece-tools` 設定傾印，如果在 `config.php` 檔案。 現在，管理員使用者在中有預設地區設定 `config.php` 檔案。<!-- MAGECLOUD-3957 -->

- ![修正圖示](../../assets/fix.svg) 修正 `Undefined index error` 發生於 `magento-cloud` 在未設定安全URL (https)的環境中，CLI命令會失敗。 現在，如果無法使用安全URL，ECE-Tools套件會使用基礎URL (http)。<!-- MAGECLOUD-4009 -->

## v2002.0.20

- ![新圖示](../../assets/new.svg) **Docker更新**—

   - ![新圖示](../../assets/new.svg) 您現在可以使用以下執行功能測試 `ece-tools` Docker環境中的包。 另請參閱 [應用程式測試](https://devdocs.magento.com/cloud/docker/docker-test-magecloud-pkg-code.html).<!-- MAGECLOUD-3129/3684 -->

   - ![新圖示](../../assets/new.svg) 新增對使用設定PHP模組的支援 `.magento.app.yaml` 檔案。 任何 [指定的PHP延伸模組 `.magento.app.yaml` 檔案](https://devdocs.magento.com/cloud/project/magento-app-php-application.html#php-extensions) 在Docker PHP容器中變得可用。<!-- MAGECLOUD-3357 -->

   - ![新圖示](../../assets/new.svg) 有新命令可用於改進Docker命令列體驗。 請參閱 [`bin/magento-docker` Docker參考的區段](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli).<!-- MAGECLOUD-3569 -->

   - ![新圖示](../../assets/new.svg) 新增使用Mutagen.io在本機主機和Docker之間的開發期間同步檔案的功能。<!-- MAGECLOUD-3559 -->

   - ![修正圖示](../../assets/fix.svg) 更正了使用Docker環境時的預設路徑。 現在，當您使用SSH登入Docker容器時，您位於的專案根目錄下 `/app` 目錄（如預期）。<!-- MAGECLOUD-3582 -->

   - ![修正圖示](../../assets/fix.svg) 將Na程式庫從1.0.11版更新至1.0.18版，並更新Na PHP擴充功能。<!-- MAGECLOUD-3832 -->

     >[!WARNING]
     >
     >雲端基礎結構上的Adobe Commerce客戶必須 [提交Adobe Commerce支援票證](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) 在升級至Adobe Commerce 2.3.2之前，在Pro生產和測試環境中升級libna套件。目前，您無法將入門環境升級至Adobe Commerce 2.3.2。

   - ![修正圖示](../../assets/fix.svg) 已新增 `analysis-icu` 和 `analysis-phonetic` 將外掛程式Elasticsearch到所有Docker映像。<!-- MAGECLOUD-3446 -->

   - ![修正圖示](../../assets/fix.svg) 改良驗證：針對使用選項時 `docker:build` 命令時，您必須提供選項的值。 此外，已新增使用時的節點版本驗證 `docker:build run` 命令。<!-- MAGECLOUD-3486 & MAGECLOUD-3678 -->

- ![新圖示](../../assets/new.svg) **環境變數更新**—

   - ![新圖示](../../assets/new.svg) 新增對資料庫表格首碼的支援，使用 [DATABASE_CONFIGURATION環境變數](../environment/variables-deploy.md#database_configuration).<!-- MAGECLOUD-2901 -->

   - ![新圖示](../../assets/new.svg) 已新增 **FORCE_UPDATE_URL** 部署變數，以在部署至Pro和Starter生產和中繼環境時更新基本URL。 請參閱中的定義 [部署變數](../environment/variables-deploy.md#force_update_urls) 內容。<!-- MAGECLOUD-3602 -->

   - ![新圖示](../../assets/new.svg) 已新增 **TTFB_TESTED_PAGES** 要設定的部署後變數 _到第一個位元組的時間_ 頁面測試，以檢查部署至雲端基礎建設的網站上的應用程式效能。 請參閱中的變數說明 [部署後變數](../environment/variables-post-deploy.md).<!-- MAGECLOUD-3643 -->

   - ![修正圖示](../../assets/fix.svg) 修正多執行緒SCD造成靜態內容部署隨機失敗的問題。 涉及設定「 」的因應措施 **SCD_THREADS** 變數至 `1`. 您現在可以根據需要增加計數。 請參閱以下檔案中的定義 [部署變數](../environment/variables-deploy.md#scd_threads) 和 [建立變數](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3611 -->

   - ![修正圖示](../../assets/fix.svg) 您可以設定 **WARMUP_PAGE** 環境變數來快取單一頁面、多個網域和多頁面。 請參閱中的展開定義 [部署後變數](../environment/variables-post-deploy.md#warm_up_pages) 內容。<!-- MAGECLOUD-3258 -->

- ![修正圖示](../../assets/fix.svg) 已新增 `pub/static/.htaccess` 檔案至排除清單。 [PHOENIX MEDIA GmbH的Bjorn Kraus提交的修正](https://github.com/magento/ece-tools/pull/455).<!-- MAGECLOUD-3545/Github#455 -->

- ![修正圖示](../../assets/fix.svg) 修正所有驗證訊息顯示為「 」時的錯誤 `Critical` 如果至少一個嚴重等級驗證器傳回錯誤。<!-- MAGECLOUD-3178 -->

- ![修正圖示](../../assets/fix.svg) 修正當資料庫中不存在基礎URL時，導致部署失敗的問題。<!-- MAGECLOUD-3075 -->

- ![新圖示](../../assets/new.svg) 已新增 **`env:config:show`命令** 至 `ece-tools` 顯示環境服務、路由或變數的套件。 另請參閱 [服務、路由和變數](https://devdocs.magento.com/cloud/reference/ece-tools-reference.html#services-routes-and-variables). [Vladimir Kerkhoff提交的功能](https://github.com/magento/ece-tools/pull/486).<!-- MAGECLOUD-3451 -->

- ![修正圖示](../../assets/fix.svg) 修正嘗試安裝Adobe Commerce 2.2.6或更舊版本時，導致嚴重錯誤的問題 `ece-tools` 殼層重構後開發。<!-- MAGECLOUD-3665 -->

- ![修正圖示](../../assets/fix.svg) 修正導致Adobe Commerce 2.1.x和2.2.x安裝失敗，並警告您使用已淘汰的Carbon版本的問題。<!-- MAGECLOUD-3704 -->

- ![修正圖示](../../assets/fix.svg) 降低 `cloud.log` 殼層輸出的記錄層級 `info` 至 `debug`.<!-- MAGECLOUD-3277 -->

- ![修正圖示](../../assets/fix.svg) 已新增 `--remove-definers (-d)` 的選項 `ece-tools db-dump` 命令以從傾印檔案中移除定義器。<!-- MAGECLOUD-3510 -->

## v2002.0.19

- ![修正圖示](../../assets/fix.svg) 修正覆寫 `env.php` 檔案進行部署，導致遺失自訂設定。 此更新可確保雲端基礎結構上的Adobe Commerce更新 `env.php` 檔案進行每次部署，同時保留自訂設定。<!-- MAGECLOUD-3668 -->

## v2002.0.18

- ![新圖示](../../assets/new.svg) **Docker更新**—

   - ![新圖示](../../assets/new.svg) 現在，Docker環境支援中定義的cron配置 [.magento.app.yaml檔案的crons屬性](https://devdocs.magento.com/cloud/project/magento-app-properties.html#crons).<!-- MAGECLOUD-3150 -->

   - ![新圖示](../../assets/new.svg) **新Docker容器** — 新增 [TLS終止Proxy容器](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) 促進透過HTTPS的Varnish SSL終止。<!-- MAGECLOUD-2890 -->

   - ![新圖示](../../assets/new.svg) **新Docker映像** — 新增Node.js影像以支援Gulp和其他功能，例如Jasmine JS單元測試。<!-- MAGECLOUD-3345 -->

   - ![新圖示](../../assets/new.svg) **Docker構建模式** — 現在您可以選擇在中啟動Docker環境 [生產模式或開發人員模式](https://devdocs.magento.com/cloud/docker/docker-launch.html#set-the-launch-mode). 開發人員模式透過完整的可寫入檔案系統許可權支援主動式開發。<!-- MAGECLOUD-3152/3511 -->

   - ![修正圖示](../../assets/fix.svg) 修復了導致Docker部署失敗的問題，並引發了 `Name or service not known` 如果快取設定為無法使用服務，則會發生錯誤。 現在，您可以從 [`.magento/services.yaml` 檔案](https://devdocs.magento.com/cloud/project/services.html). Docker配置生成器更新以下位置中的服務： `docker/config.php.dist` 檔案自動更新。<!-- MAGECLOUD-3369 -->

   - ![新圖示](../../assets/new.svg) 新增互動式服務相容性驗證。 現在，如果要求的服務與Adobe Commerce版本或其他服務不相容， _互動模式_ 提示使用者訊息並選擇繼續。 請參閱 [服務版本](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers) 可用於Docker。 使用 `-n` 跳過互動以進行CICD的選項。<!-- MAGECLOUD-3251 -->

   - ![修正圖示](../../assets/fix.svg) 修正Docker撰寫的問題 `db-dump` 清除現有傾印的命令。<!-- MAGECLOUD-3366 -->

   - ![修正圖示](../../assets/fix.svg) 修正指派Redis的問題 `session`， `default`、和 `page_cache` 快取儲存空間至相同的資料庫ID。<!-- MAGECLOUD-3172 -->

- ![新圖示](../../assets/new.svg) **環境變數更新**—

   - ![新圖示](../../assets/new.svg) 新的 **ELASTICSUITE\_CONFIGURATION** 環境變數會在部署之間保留您的自訂服務設定。 請參閱中的定義 [部署變數](../environment/variables-deploy.md#elasticsuite_configuration) 內容。<!-- MAGECLOUD-3205 -->

   - ![新圖示](../../assets/new.svg) 已新增 **SCD_MAX_EXECUTION_TIMEOUT** 環境變數，好讓您可以增加從以下位置完成靜態內容部署的時間： `.magento.env.yaml` 檔案。 請參閱中的定義 [部署變數](../environment/variables-deploy.md#scd_max_execution_time)，則 [建立變數](../environment/variables-build.md#scd_max_execution_time)，以及 [全域變數](../environment/variables-global.md#scd_max_execution_time).<!-- MAGECLOUD-2822 -->

      - ![新圖示](../../assets/new.svg) 已新增 **Magento_CLOUD_LOCKS_DIR** 環境變數，用於設定雲端基礎結構上鎖定提供者之掛載點的路徑。 鎖定提供者可防止啟動重複的cron作業和cron群組。 Adobe Commerce 2.2.5版及更新版本支援此變數，且可自動設定。 請參閱中的定義 [雲端變數](../environment/variables-cloud.md).<!-- MAGECLOUD-3135 -->

      - ![修正圖示](../../assets/fix.svg) 已變更 **SCD_THREADS** 環境變數預設值，可根據偵測到的CPU執行緒計數，自動判斷最佳值。 請參閱以下檔案中的更新定義： [部署變數](../environment/variables-deploy.md#scd_threads) 和 [建立變數](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3382 -->

- ![修正圖示](../../assets/fix.svg) 修正了資料庫隔離機制修補程式的問題，此問題在升級至雲端基礎結構2002.0.16版的Adobe Commerce時會導致錯誤。<!-- MAGECLOUD-3383 -->

- ![修正圖示](../../assets/fix.svg) 已新增修補程式，取代 _Google影像圖表_ 替換為 _影像圖表_. 請參閱DevBlog文章 [針對M1淘汰Google影像圖表並更新](https://community.magento.com/t5/Magento-DevBlog/Google-Image-Charts-deprecation-and-update-for-M1/ba-p/125006).<!-- MAGECLOUD-3456 -->

- ![修正圖示](../../assets/fix.svg) 已新增的驗證 [SEARCH_CONFIGURATION變數](../environment/variables-deploy.md#search_configuration). 未設定&#39;engine&#39;選項且發生錯誤時，部署會失敗 `_merge` 非必要。<!-- MAGECLOUD-3470 -->

- ![修正圖示](../../assets/fix.svg) 修正在發生例外狀況後公開敏感資料的問題。 現在，敏感資訊已適當地遮罩。<!-- MAGECLOUD-3525 -->

- ![修正圖示](../../assets/fix.svg) 改善Magento Open Source套件的容錯設定。 在Adobe Commerce無法從Redis讀取資料的情況下 `slave` 執行個體，從Redis進行讀取 `master` 執行個體。 另請參閱 [REDIS_USE_SLAVE_CONNECTION](../environment/variables-deploy.md#redis_use_slave_connection).<!-- MAGECLOUD-2899 -->

## v2002.0.17

>[!NOTE]
>
>此 `ece-tools` 2002.0.17版包含重要的安全性修補程式。 另請參閱 [技術資源：Magento Open Source修補程式](https://magento.com/tech-resources/download#download2288).

- ![新圖示](../../assets/new.svg) **服務更新** — 由下列Adobe Commerce版本支援： 2.2.8和更新版本2.2.x、2.3.1和更新版本2.3.x

   - 新增對Elasticsearch 6.x版的支援。<!-- MAGECLOUD-3196 -->

   - 新增Redis 5.0版的支援。

- ![新圖示](../../assets/new.svg) **新Docker影像** — 已將以下服務新增到Docker構建：

   - Elasticsearch6.5<!-- MAGECLOUD-3196 -->

   - Redis 5.0<!-- MAGECLOUD-3223 -->

- ![新圖示](../../assets/new.svg) **新環境變數** — 之前，SCD壓縮會有一個硬式編碼逾時。 現在您可以使用設定SCD壓縮逾時 **SCD_COMPRESSION_TIMEOUT** 環境變數。 請參閱以下檔案中的定義 [建立變數](../environment/variables-build.md#scd_compression_timeout) 和 [部署變數](../environment/variables-deploy.md#scd_compression_timeout) 內容。<!-- MAGECLOUD-2870 -->

- ![修正圖示](../../assets/fix.svg) 已新增 `--use-rewrites` 安裝命令的選項，以便它針對店面中產生的連結使用網頁伺服器重寫以及管理員存取，來改善安全性和客戶體驗。<!-- MAGECLOUD-3246 -->

- ![修正圖示](../../assets/fix.svg) 已新增時間戳記至 `var/log/install_upgrade.log` 檔案，以顯示安裝和升級事件的日期。<!-- MAGECLOUD-2895 -->

## v2002.0.16

- ![新圖示](../../assets/new.svg) **Docker更新**—

   - 現在，在Docker環境中生成的預設服務配置與雲端範本中的預設配置相同。<!-- MAGECLOUD-3025 -->

   - 您可以使用從Docker環境傳送郵件 `sendmail` 服務。<!-- MAGECLOUD-2907 -->

   - 新增以下功能： [設定Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) 以在Cloud Docker環境中偵錯。<!-- MAGECLOUD-2891 -->

   - 修正產生 `docker-compose.yml` 檔案。<!-- MAGECLOUD-2883 -->

- ![新圖示](../../assets/new.svg) **升級改善** — 新增驗證，以確認 `autoload` 中的屬性 `composer.json` 檔案包含升級至Adobe Commerce v2.3之前所需的設定變更。另請參閱 [升級版本](https://devdocs.magento.com/cloud/project/project-upgrade.html).<!-- MAGECLOUD-2392 -->

- ![新圖示](../../assets/new.svg) 部署靜態內容時的壓縮程式現在包含所有資產（原生產生或自訂），並且會在建置階段開始時發生 [`build:transfer` 區段](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks). 先前，壓縮程式會在套用自訂縮制和靜態資產套件組合前進行。 [Rafael Garcia Lepper提交的修正，來自Tryzens Limited](https://github.com/magento/ece-tools/pull/413).<!-- MAGECLOUD-3104 -->

- ![修正圖示](../../assets/fix.svg) 修正了在設定其他資料庫和服務關係後，在部署期間立即發生的資料庫連線錯誤。 此外，此修正可解決入門適用的Commerce Reporting設定程式期間發生的問題。 首先，此升級為使用Commerce Reporting的「必備」。<!-- MAGECLOUD-3035 -->

- ![修正圖示](../../assets/fix.svg) 修正資料庫組態導致部署程式失敗的驗證問題。<!-- MAGECLOUD-3003 -->

- ![修正圖示](../../assets/fix.svg) 以適當版本的 `symfony/yaml` 要搭配使用的套件 [PHP常數](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants). 使用時常數剖析無法運作 `symfony/yaml` 3.2之前的套件版本。 [Vladimir Kerkhoff提交的修正](https://github.com/magento/ece-tools/pull/404).<!-- MAGECLOUD-2956 -->

- ![新圖示](../../assets/new.svg) **環境設定檢查** — 新增驗證，以檢查PHP版本並在使用者未使用最新建議版本時警告使用者。<!--MAGECLOUD-2903-->

- ![修正圖示](../../assets/fix.svg) 修正處理錯誤JSON變數的問題。 現在，如果JSON變數造成語法錯誤，中會顯示警告 `cloud.log` 檔案和部署會使用預設變數繼續進行。<!-- MAGECLOUD-2851 -->

- ![修正圖示](../../assets/fix.svg) 修正停用Redis服務後立即部署期間發生的連線錯誤。<!-- MAGECLOUD-2747 -->

- ![新圖示](../../assets/new.svg) **正在記錄變更** — 已更新 [記錄層級](../environment/log-handlers.md#log-levels) 從 `Info` 至 `Notice` 對於下列建置和部署流程事件：<!--MAGECLOUD-2925-->

   - 調解已安裝模組的程式開始和結束 `composer.json` 共用組態設定於 `app/etc/config.php` 檔案

   - 設定驗證程式的開始和結束

   - 開始和結束 `setup:di:compile` 產生類別的程式

- ![新圖示](../../assets/new.svg) **新環境變數**—

   - **[resource_CONFIGURATION部署變數](../environment/variables-deploy.md#resource_configuration)** — 使用此變數將資源名稱對應到資料庫連線。<!-- MAGECLOUD-3026 & MAGECLOUD-2963-->

   - **[X_FRAME_CONFIGURATION全域變數](../environment/variables-global.md#x_frame_configuration)** — 使用此變數來變更 `X-Frame-Options` 在中呈現Adobe Commerce頁面的標題設定 `<frame>`， `<iframe>`，或 `<object>`.<!-- MAGECLOUD-3048 -->

- ![修正圖示](../../assets/fix.svg) **環境變數更新** — 已變更下列環境變數：

   - **[WARMUP_PAGE](../environment/variables-post-deploy.md)** — 新增在為Adobe Commerce存放區定義的所有網域上預先載入指定頁面快取的功能。 先前，如果您的網站設定有多個網域，後部署程式無法預先載入非預設網域上指定頁面的快取，並在後部署記錄中傳回下列錯誤： `ERROR: Warming up failed: <uri>`<!-- MAGECLOUD-2466 -->

   - **SCD_COMPRESSION_LEVEL** — 更新檔案和範例 `.magento.env.yaml` 檔案的SCD壓縮等級預設值正確。 請參閱以下檔案中的定義 [建立變數](../environment/variables-build.md#scd_compression_level) 和 [部署變數](../environment/variables-deploy.md#scd_compression_level) 內容。<!-- MAGECLOUD-2823 -->

   - **SCD_EXCLUDE_THEMES** — 此環境變數已遭取代。 使用 [SCD_MATRIX](../environment/variables-build.md#scd_matrix) 控制佈景主題設定。<!--MAGECLOUD-2882-->

   - **SCD\_矩陣** — 修正驗證程式，以防止在SCD_MATRIX忽略包含不同字元大小寫的主題值時發生問題。 請參閱以下檔案中的定義 [建立變數](../environment/variables-build.md#scd_matrix) 和 [部署變數](../environment/variables-deploy.md#scd_matrix) 內容。<!-- MAGECLOUD-2904 -->

   - **管理員變數**—<!-- MAGECLOUD-2573/MAGECLOUD-2848 -->

      - 改善使用環境變數管理管理員使用者認證時的安全性。 在升級期間，您無法再使用ADMIN_EMAIL、ADMIN_USERNAME和ADMIN_PASSWORD環境變數來覆寫管理員認證。 如果您無法存取「管理員」面板，請使用 _忘記密碼_ 功能或 `admin:user:create` 用來建立新管理員使用者的CLI命令。 另請參閱 [存取您的管理員面板](https://devdocs.magento.com/cloud/onboarding/onboarding-tasks.html#admin).

      - 升級或套用修補程式時不再需要ADMIN_EMAIL。

## v2002.0.15

- ![新圖示](../../assets/new.svg) **Docker更新**—

   - 現在Docker生成器使用 `.magento.app.yaml` 和 `.magento/services.yaml` 組態檔時間 [構建您的Docker環境](https://devdocs.magento.com/cloud/docker/docker-config.html). 您可以使用組建引數選擇不同的服務版本。<!-- MAGECLOUD-2888 -->

   - 新增PHP 7.2影像 — 在Cloud Docker中新增對PHP 7.2的支援；更新 [啟動Docker設定](https://devdocs.magento.com/cloud/docker/docker-config.html) 以包含 `docker:build --php` 選項來指定與您的Adobe Commerce版本相容的PHP版本。<!-- MAGECLOUD-2799 -->

   - 已新增 [Cron容器](https://devdocs.magento.com/cloud/docker/docker-containers-cli.html#cron-container) 根據PHP-CLI影像。<!-- MAGECLOUD-2565 -->

   - 已將以下服務新增到Docker構建：

      - [!DNL RabbitMQ] 3.5和3.7<!-- MAGECLOUD-2567 & 2889-->

      - Elasticsearch1.7、2.4和5.2<!-- MAGECLOUD-2569 & 2887 -->

      - Redis 3.2和4.0<!-- MAGECLOUD-2886 -->

- ![新圖示](../../assets/new.svg) **使用PHP常數進行配置** — 新增支援 [PHP常數](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants) 在 `.magento.env.yaml` 組態檔。<!-- MAGECLOUD- 2575 -->

- ![新圖示](../../assets/new.svg) **新環境變數** — 依預設，只有生產環境已啟用Google Analytics。 您可以使用在中繼和整合環境中啟用Google Analytics  [啟用GOOGLE_ANALYTICS環境變數](../environment/variables-deploy.md#enable_google_analytics).<!--MAGECLOUD-2879-->

- ![修正圖示](../../assets/fix.svg) 修正從移除自訂cron設定的問題 `env.php` 重新部署後的檔案。 現在，自訂cron設定可安全地保留在 `env.php` 檔案。<!-- MAGECLOUD-2923 -->

- ![修正圖示](../../assets/fix.svg) 修正訊息和中的不一致 [記錄層級](../environment/log-handlers.md#log-levels) 用於建置、部署和部署後階段。 增加開始和結束記錄訊息層級，從 **資訊** 至 **通知** 用於所有階段和子階段。 視情況新增開始和結束日誌訊息。<!-- MAGECLOUD-2919 -->

- ![修正圖示](../../assets/fix.svg) 修正設定後，cron程式無法啟動部署後階段的問題。 現在，如果您啟用了部署後掛接，則會在部署後階段開始時再次啟用cron流程。<!-- MAGECLOUD-2862 -->

- ![修正圖示](../../assets/fix.svg) 解決在指定自訂資料庫設定時無法成功安裝Adobe Commerce的問題。 以前，安裝程式使用的資料庫配置來自 [Magento_CLOUD_RELATIONSHIP變數](../environment/variables-cloud.md) 即使您在 [DATABASE_CONFIGURATION環境變數](../environment/variables-deploy.md#database_configuration).<!--MAGECLOUD-2736-->

- ![修正圖示](../../assets/fix.svg) 已更正 `config:dump` 命令，使其包含 `system` 的區段 `config.php` 檔案。<!--MAGECLOUD-2740-->

- ![修正圖示](../../assets/fix.svg) 已修正導致下列問題的因素 _熱身_ 透過更正來源基底URL參照，在部署後階段期間出現錯誤。<!--MAGECLOUD-2797-->

- ![修正圖示](../../assets/fix.svg) 修正以下期間不正確地產生檔案的問題： `setup:di:compile` 會影響Amazon Pay模組的程式。<!--MAGECLOUD-2850-->

## v2002.0.14

- ![新圖示](../../assets/new.svg) **驗證理想狀態** — 此 `ideal-state` 精靈現在會在每次部署期間驗證目前的設定，並提供明確的設定更新指示，以實現更快速、零停機部署。<!--MAGECLOUD-2372-->

- ![修正圖示](../../assets/fix.svg) **PCI法規遵循** — 更新雲端基礎結構上Adobe Commerce的傳訊通訊協定，使其在與協力廠商傳訊服務連線時需要Transport Layer Security (TLS) version 1.2。 如果您使用的訊息服務不支援TLS 1.2版，您必須升級服務。 否則，當您的Adobe Commerce應用程式嘗試連線至訊息伺服器以傳送電子郵件時，將會顯示下列錯誤訊息： `Unable to connect via TLS`.<!--MAGECLOUD-2521-->

- ![新圖示](../../assets/new.svg) **部署改善** — 新增驗證功能，在測試或生產環境具備下列條件時警告客戶 `dev`， `debug`，或 `debug_logging` 啟用選項以防止過度記錄活動造成的效能問題。<!--MAGECLOUD-2517-->

- ![修正圖示](../../assets/fix.svg) **部署修正**—

   - 維護模式現在會在部署階段開始時啟用，並在結束時停用。 如果部署失敗，則站點將保持維護模式，直到部署問題得到解決。 以前，即使部署失敗，網站也會返回生產模式。<!--MAGECLOUD-2603-->

      - 已重新處理部署階段驗證檢查，將下列部署問題的錯誤層級降級，從 `CRITICAL` 至 `WARNING` 以便完成部署。 以前，這些問題會導致部署失敗。

      - 環境設定包含不正確的部署或雲端變數值。

   - 雲端基礎結構上的Elasticsearch版本與雲端基礎結構上Adobe Commerce支援的elasticsearch/elasticsearch模組版本不相容。 請參閱 [Elasticsearch疑難排解文章](https://support.magento.com/hc/en-us/articles/360015758471-Deployment-fails-or-interrupts-with-cloud-log-error-Elasticsearch-version-is-not-compatible-with-current-version-of-magento) 在Adobe Commerce支援知識庫中。<!--MAGECLOUD-2600-->

   - 已修正「 」中的共用組態設定問題 `app/etc/config.php` 檔案導致 `recursion detected` 部署時發生錯誤。<!--MAGECLOUD-2173-->

- ![修正圖示](../../assets/fix.svg) **Cron相關修正**—

   - 修正了在您指定預設值（1分鐘）以外的cron頻率時，無法執行作業的cron排程問題。<!--MAGECLOUD-2602-->

   - 修正了部署階段中允許cron工作在部署期間繼續執行的問題，這可能會導致資料庫鎖定和其他嚴重問題。 現在，所有cron工作都會在部署階段開始之前停止，並在部署完成後重新啟動。&lt;!—MAGECLOUD—2537—>

   - 修正2.2.x版中的cron工作工作流程，解除鎖定凍結的cron工作，以便在開始部署之前停止。 以前，凍結的cron工作導致部署延遲。<!--MAGECLOUD-2501-->

- ![修正圖示](../../assets/fix.svg) 已變更 `config.php` 產生的檔案 `vendor/bin/ece-tools config:dump` 指令來使用短陣列語法和4個空格縮排，以符合Adobe Commerce編碼標準。<!--MAGECLOUD-2527-->

- ![修正圖示](../../assets/fix.svg) 修正以下情況發生的部署錯誤： `.magento.env.yaml` 包含 `{{ base_url }}` 和 `{{ unsecure_base_url }}` Web設定的預留位置，而不是雲端基礎結構專案上Adobe Commerce的預設URL設定。/<!--MAGECLOUD-2607-->

## v2002.0.13

- ![新圖示](../../assets/new.svg) **啟用零停機部署** — 現在，雲端基礎結構上的Adobe Commerce會在部署期間將具有所需資料庫變更的請求排入佇列，並在部署完成後立即套用變更。 請求最多可保留5分鐘，以確保不會遺失任何工作階段。 另請參閱 [減少雲端部署停機時間的靜態內容部署選項](https://support.magento.com/hc/en-us/articles/360004861194-Static-content-deployment-options-to-reduce-deployment-downtime-on-Cloud).<!--MAGECLOUD-2169-->

- ![新圖示](../../assets/new.svg) **適用於雲端的Docker撰寫** — 已進行下列改善 [Docker設定和配置](https://devdocs.magento.com/cloud/docker/docker-config.html) 程式：

   - 新增命令 — `docker:config:convert` 將PHP配置檔案轉換為Docker ENV格式以簡化環境配置。 現在，您可以將PHP配置檔案複製到Docker目錄中，並將其轉換為Docker ENV檔案。 另請參閱 [Launch Docker](https://devdocs.magento.com/cloud/docker/docker-config.html).<!--MAGECLOUD-2359-->

   - Adobe Commerce雲端基礎結構安裝程式現在支援部署至唯讀和讀寫檔案系統，以便更密切地模擬雲端檔案系統。 另請參閱 [配置Docker](https://devdocs.magento.com/cloud/docker/docker-config.html).&lt;!—MAGECLOUD—2357—>

   - **Redis服務支援** — 新增Redis映像，該映像將部署到Docker容器並自動配置為與您的Docker安裝配合使用。&lt;!—MAGECLOUD—2442—>

   - 現在您有了使用雲端Docker時的資料庫傾印功能 [資料庫容器](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#database-container). 此外，您可以 [共用檔案](https://devdocs.magento.com/cloud/docker/docker-containers.html#sharing-data-between-host-machine-and-container) 主機和容器之間，使用 `docker/mnt` 目錄。<!-- MAGECLOUD-2577 -->

   - **塗漆服務支援** — 新增Varnish影像，該影像會自動部署到Docker容器。 部署後，您可以依照Adobe Commerce最佳實務手動設定Varnish。 另請參閱 [設定及使用清漆](https://devdocs.magento.com/guides/v2.3/config-guide/varnish/config-varnish.html).&lt;!—MAGECLOUD—2358—>

   - 安全網站存取 — 新增SSL支援，可存取您的Adobe Commerce商店和管理面板。&lt;!—MAGECLOUD—2360—>

- ![修正圖示](../../assets/fix.svg) **改善雲端基礎結構擴充功能支援的Adobe Commerce** — 將雲端基礎結構上Adobe Commerce中guzzlehttp/guzzle套件的最低版本需求降級 [composer.json檔案](https://devdocs.magento.com/cloud/reference/cloud-composer.html) 至6.2版，讓 `ece-tools` 套件與更多擴充功能相容。<!--MAGECLOUD-2205-->

- ![新圖示](../../assets/new.svg) **在建置階段期間，套用自訂變更至您的Adobe Commerce應用程式** — 我們將建置階段分割為兩個單獨的程式，以便您可以使用鉤點來將自訂變更套用至產生的靜態內容，然後再封裝應用程式以進行部署。 此 _build：generate_ 程式會產生程式碼、套用修補程式，以及產生靜態內容。 此 _build：transfer_ 程式會將產生的程式碼和靜態內容傳輸到最終目的地。 另請參閱 [應用程式鉤點](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks).<!--MAGECLOUD-2363-->

- ![修正圖示](../../assets/fix.svg) **環境設定檢查** — 改善環境設定驗證，以在雲端基礎結構上建置和部署Adobe Commerce之前，警告客戶版本不相容和設定錯誤。

   - 新增版本專屬驗證，以識別不支援或已棄用的環境變數和值。<!--MAGECLOUD-2183-->

   - 新增Elasticsearch相容性檢查，以警告使用者有關Elasticsearch設定問題。 現在，如果伺服器上的Elasticsearch服務版本與Adobe Commerce不相容，部署就會失敗。 以前，即使Elasticsearch版本不相容，部署也會成功，導致網站部署後出現產品目錄問題。<!--MAGECLOUD-2389-->

     您可以透過以下方式解決不相容問題 [提交支援票證](https://devdocs.magento.com/cloud/trouble/trouble.html) 將Elasticsearch升級為相容版本，或變更Adobe Commerce組態以指定ElasticsearchPHP使用者端的相容版本。

      - 若是Adobe Commerce 2.1.x版至2.2.2版，請將Elasticsearch升級至2.4版。

      - 若是Adobe Commerce 2.2.3版或更新版本，請將Elasticsearch升級至5.2版。

      - 如果您有Elasticsearch1.x或2.x，並且不想升級，請在composer.json中將Adobe CommerceElasticsearchPHP使用者端版本要求更新為 `"elasticsearch/elasticsearch": "~2.0"`.

   - 改善環境變數的驗證，以識別在建置、部署和部署後階段期間可能導致衝突的組態設定。 例如，如果靜態內容部署的全域設定與建置或部署階段的設定衝突，則在安裝和升級過程中會顯示警告訊息。<!--MAGECLOUD-2156-->

- ![修正圖示](../../assets/fix.svg) **環境變數更新** — 已變更下列環境變數：

   - **[SKIP_HTML_縮制全域變數](../environment/variables-global.md#skip_html_minification)** — 將預設值變更為 `true` 啟用隨選HTML內容縮制，將部署至中繼和生產環境的停機時間降至最低。 零停機部署需要此設定。<!--MAGECLOUD-2435-->

   - **[CLEAN_STATIC_FILES部署變數](../environment/variables-deploy.md#clean_static_files)** — 新增管理在建置階段根據CLEAN_STATIC_FILES環境變數設定產生的靜態內容之清除靜態檔案處理的功能。 之前，系統一律會清理建置階段產生的靜態內容檔案。<!--MAGECLOUD-1506-->

- ![修正圖示](../../assets/fix.svg) **記錄** — 進行下列變更，以改善記錄訊息並減少記錄大小：

   - 部署失敗記錄專案現在包含來自造成失敗的作業的命令輸出，即使您的環境設定未指定偵錯層級記錄亦然。 另請參閱 [`MIN_LOGGING_LEVEL`](../environment/variables-global.md#min_logging_level).<!--MAGECLOUD-2489-->

   - 已新增部署失敗記錄，其發生於因檔案系統處於唯讀狀態而無法正確產生某些擴充功能所需的產生處理站時。<!--MAGECLOUD-2209-->

   - 縮小部署記錄檔大小，並修正使用互動式進度列的設定命令所導致的格式問題。<!--MAGECLOUD-2402-->

   - 消除不必要的詳細資訊，並更新某些記錄陳述式的優先等級。<!--MAGECLOUD-2227-->

- ![修正圖示](../../assets/fix.svg) **Cron特定修正**—

   - 已將歷程記錄存留期的預設cron工作組態設定從3d （4320分鐘）變更為1h （60分鐘），以防止效能問題和cron佇列過快填入時可能發生的部署失敗。<!--MAGECLOUD-2427-->

   - 改善部署階段的cron工作管理程式，以防止資料庫鎖定和其他嚴重問題。 現在，所有cron工作會在部署階段中停止，並在部署完成後重新啟動。<!--MAGECLOUD-2445-->

   - 修正Adobe Commerce 2.2.0版及更新版本中，cron工作為排程使用者而啟動的鎖定機制問題，以防止cron工作啟動重複使用者。<!--MAGECLOUD-2464-->

- ![修正圖示](../../assets/fix.svg) 已修正的問題 [靜態內容壓縮程式](../environment/variables-intro.md) (`gzip`)而導致 `not overwritten` 和 `no such file or directory` 在部署過程中參照壓縮檔案時發生錯誤。<!-- MAGECLOUD-2182-->

- ![修正圖示](../../assets/fix.svg) 已修正導致無法 `php ./vendor/bin/ece-tools config:dump` 命令移除多餘的區段 `config.php` 檔案進行傾印處理（如果未指定存放區語言環境）。 現在您可以輕鬆在環境之間移動設定檔案。 在您更新至 `ece-tools` v2002.0.13，重新產生舊版本 `config.php` 改善的檔案 `config:dump` 命令。 另請參閱 [商店設定的組態管理](https://devdocs.magento.com/cloud/live/sens-data-over.html).<!--MAGECLOUD-2444-->

- ![修正圖示](../../assets/fix.svg) 修正了在部署階段期間如果路徑配置在 `.magento/routes.yaml` 檔案重新導向 [Apex](https://blog.cloudflare.com/zone-apex-naked-domain-root-domain-cname-supp/) 網域至 `www` 網域。<!--MAGECLOUD-2556-->

- ![修正圖示](../../assets/fix.svg) 已修正的問題 `_merge` 的選項 [`SEARCH_CONFIGURATION`](../environment/variables-deploy.md#search_configuration) 導致不正確合併結果的變數(如果您不包含 `engine` 引數在更新的 `.magento.env.yaml` 組態檔。 現在，合併操作只會正確覆寫您在更新中指定的值 `.magento.env.yaml` 而不需要您設定 `engine` 引數。<!--MAGECLOUD-2520-->

- ![修正圖示](../../assets/fix.svg) 修正Redis設定問題，該問題導致在雲端基礎結構2.2.1版及更新版本上無法正確啟用Adobe Commerce的工作階段鎖定，而這可能會導致效能緩慢並逾時。 現在預設會停用工作階段鎖定。 此問題是由的預設行為變更所導致。 `disable_locking` 在Redis工作階段處理常式套件v1.3.4中引入的引數。 另請參閱 [colimollenhour/php-redis-session-abstract套件](https://github.com/colinmollenhour/php-redis-session-abstract).<!-- MAGECLOUD-2515-->

## v2002.0.12

- ![新圖示](../../assets/new.svg) **適用於雲端的Docker撰寫** — 新增指令 — `docker:build` — 產生 [Docker撰寫](https://devdocs.magento.com/cloud/docker/docker-config.html) 來自雲端的設定 `ece-tools` 存放庫。<!-- MAGECLOUD-2250 -->

- ![新圖示](../../assets/new.svg) **變更地區設定** — 現在無需匯出和匯入組態程式即可變更存放區語言環境。 當應用程式處於生產狀態且已啟用SCD_ON_DEMAND時，即可使用存放區和管理程式語言環境選項。<!-- MAGECLOUD-2019 -->

- ![新圖示](../../assets/new.svg) <!-- MAGECLOU-1998 -->**網站地圖和機器人** — 已建立 [工作流程](../store/robots-sitemap.md) 以新增 `robots.txt` 檔案並產生 `sitemap.xml` 檔案進行單一網域設定，不需要變更基礎結構。

- ![新圖示](../../assets/new.svg) **精靈** — 新增兩個 [精靈](../deploy/smart-wizards.md) 協助您進行雲端設定：<!-- MAGECLOUD-1910 -->

   - `ideal-state` — 設定理想狀態，將部署停機時間降到最低

   - `master-slave` — 設定資料庫和Redis的負載平衡

- ![新圖示](../../assets/new.svg) **模組重新整理** — 新增雲端命令 — `module:refresh` — 啟用已停用或未明確啟用的模組，類似於在建置期間自動完成的方式。<!-- MAGECLOUD-1521 -->

- ![新圖示](../../assets/new.svg) 新增以下功能：選擇合併或覆寫服務的設定，使用 `_merge` 中的選項 [快取](../environment/variables-deploy.md#cache_configuration)， [工作階段](../environment/variables-deploy.md#session_configuration)， [佇列](../environment/variables-deploy.md#queue_configuration)、和 [搜尋](../environment/variables-deploy.md#search_configuration) 設定。<!-- MAGECLOUD-2105 -->

- ![新圖示](../../assets/new.svg) **環境設定範例檔案** — 我們已新增 `.magento.env.yaml` ECE-Tools套件的範例檔案，其中包含每個環境變數的詳細說明和可能值。<!-- MAGECLOUD-1908 -->

   - 我們也新增了深層驗證 `.magento.env.yaml` 此設定可防止部署程式中因未預期的值而發生失敗。 失敗發生時，您現在會收到詳細的錯誤訊息，開頭為： `Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:`<!-- MAGECLOUD-1907 -->

- ![新圖示](../../assets/new.svg) 已新增下列專案 [**環境變數**](../environment/variables-intro.md)：

   - 現在，您可以使用新的為每個主題定義多個地區設定 [SCD_MATRIX](../environment/variables-deploy.md#scd_matrix) 環境變數，這會減少要部署的主題檔案數量。<!-- MAGECLOUD-1501 -->

   - 已新增 [DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration) 環境變數，可自訂您的資料庫連線以進行部署。<!-- MAGECLOUD-2047 -->

   - 新的 [MIN_LOGGING_LEVEL](../environment/variables-global.md#min_logging_level) 變數會覆寫所有輸出資料流的最低記錄層級，而不會變更程式碼。<!-- MAGECLOUD-2129 -->

- ![修正圖示](../../assets/fix.svg) 修正造成部署和部署後階段之間停機的問題。 現在，部署後階段開始 _立即_ 部署階段結束後。

- ![修正圖示](../../assets/fix.svg) 修正未清除成功cron工作(具有 `status = success`，從排程中。<!-- MAGECLOUD-2268 -->

- ![修正圖示](../../assets/fix.svg) 已修正的問題 `post_deploy` 在部署階段而非專案的部署後階段中清除快取的連結。<!-- MAGECLOUD-2113 -->

- ![修正圖示](../../assets/fix.svg) 修正搭配多個地區設定使用SCD時所產生的問題 `js-translation.json` 每個地區設定的檔案。<!-- MAGECLOUD-2034 -->

- ![修正圖示](../../assets/fix.svg) 已最佳化 `db:dump` 中的命令 `ece-tools` 封裝以避免鎖定表格並提高速度。<!-- MAGECLOUD-2033 -->

## v2002.0.11

>[!NOTE]
>
>2.2.4相容性需要ECE-Tools 2002.0.11版。

- ![新圖示](../../assets/new.svg) **設定與非主節點的唯讀連線** — 此版本新增了設定非主節點的唯讀連線，以接收唯讀流量的功能(適用於  [MariaDB](../environment/variables-deploy.md#mysql_use_slave_connection))。<!--MAGECLOUD-143 -->[Redis](../environment/variables-deploy.md#redis_use_slave_connection) 和 <!--MAGECLOUD-143 -->

- ![新圖示](../../assets/new.svg) **設定精靈** — 新增精靈，協助驗證靜態內容部署的設定。 另請參閱 [智慧型精靈](../deploy/smart-wizards.md).<!--MAGECLOUD-1910 -->

- ![新圖示](../../assets/new.svg) **Symfony主控台支援** — 新增支援Symfony Console 4與Adobe Commerce 2.3。<!-- MAGECLOUD-1966 -->

- ![修正圖示](../../assets/fix.svg) **Cron排程最佳化** — 改善佇列管理和增強記錄功能，協助偵錯cron相關問題。<!-- MAGECLOUD-1607 -->

- ![修正圖示](../../assets/fix.svg) 部署驗證失敗，如果 `ADMIN_EMAIL` 或 `ADMIN_USERNAME` 值與現有的管理員帳戶相同。<!-- MAGECLOUD-1221 -->

- ![修正圖示](../../assets/fix.svg) 移除2.2.x版本的SOLR支援。 2.1.x版本仍可啟用SOLR。<!-- MAGECLOUD-1282 -->

- ![修正圖示](../../assets/fix.svg) PRO專案的測試和生產環境第一次安裝時現在包含不同的Elasticsearch索引首碼，以防止在識別屬於每個環境的記錄時可能發生衝突。<!-- MAGECLOUD-1489 -->

- ![修正圖示](../../assets/fix.svg) 修正在靜態內容部署期間中斷舊版架構的建置階段的問題。<!-- MAGECLOUD-2021 -->

- ![修正圖示](../../assets/fix.svg) **Cron專屬改良功能** — 重新執行cron實作：<!-- MAGECLOUD-1607 -->

   - 修正造成cron佇列快速填滿的問題。 現在能以更可靠的方式清除過時的cron工作。

   - 重新組織cron作業順序，讓不同執行緒中的所有作業在一般群組之前啟動。

   - 改善記錄功能，以便更妥善協助偵錯cron問題。

   - **注意** — 此版本解決許多cron相關問題。 如果您目前在中使用某些cron相關修補程式 _m2-hotfix_，將其移除。

- ![修正圖示](../../assets/fix.svg) **SCD專屬改善專案**—

   - 您可以使用 `VERBOSE_COMMANDS` 和 `SCD_COMPRESSION_LEVEL` 兩者期間的環境變數 _版本編號_ 和部署階段(_P)。<!-- MAGECLOUD-1819 -->

   - 修正當遇到非預期的值時，導致部署失敗並出現隨機錯誤的問題。 `SCD_COMPRESSION_LEVEL` 環境變數。 改善設定驗證，以提供有意義的通知。 另請參閱 [`SCD_COMPRESSION_LEVEL`](../environment/variables-build.md#scd_compression_level) 以取得可接受的值。<!-- MAGECLOUD-2043 -->

   - 修正 `SCD_COMPRESSION_LEVEL` 環境變數設定流程，讓覆寫功能如預期運作。<!-- MAGECLOUD-2044 -->

   - 修正無法設定的問題 `SCD_THREADS` 中的環境變數 `.magento.env.yaml` 檔案 _部署_ 階段。<!-- MAGECLOUD-2046 -->

## v2002.0.10

- ![新圖示](../../assets/new.svg) **靜態內容部署(SCD)** — 有新的替代部署程式，可在收到請求時產生靜態內容（隨選）。 這可產生最關鍵的資產，藉此減少停機時間並改善快取處理。<!-- MAGECLOUD-1285 -->

   - **新環境變數** — 已新增 `SCD_ON_DEMAND` 全域環境變數來產生靜態內容。<!-- MAGECLOUD-1738 -->

   - **部署後勾點** — 新增 `post_deploy` 鉤點 `.magento.app.yaml` 清除快取並預先載入（加溫）快取的檔案 _晚於_ 容器開始接受連線。 它僅適用於包含中繼和生產環境的Pro專案 [!DNL Cloud Console] 和適用於入門專案。 雖然不需要，但這會與 `SCD_ON_DEMAND` 環境變數。<!-- MAGECLOUD-1788 -->

- ![新圖示](../../assets/new.svg) **最佳化** — 在部署期間最佳化移動或複製檔案，以提高部署速度並降低檔案系統的負載。<!-- MAGECLOUD-1842 -->

- ![新圖示](../../assets/new.svg) **部署記錄** — 新增啟用Syslog和Graylog Extended Log Format (GELF)處理常式的功能，以便在部署過程中輸出記錄。 另請參閱 [記錄處理常式](../environment/log-handlers.md).<!-- MAGECLOUD-1751 -->

- ![新圖示](../../assets/new.svg) 已新增下列專案 [**環境變數**](../environment/variables-intro.md)：

   - `CRYPT_KEY` — 在行動資料庫時，向另一個環境提供密碼編譯金鑰。<!-- MAGECLOUD-1556 -->

   - `SKIP_HTML_MINIFICATION`—_全域_ 跳過複製中靜態檢視檔案的環境變數 `var/view_preprocessed` 目錄，並在請求時產生縮制HTML。<!-- MAGECLOUD-1621 and MAGECLOUD-1736-->

   - `SCD_ON_DEMAND`—_全域_ 環境變數來產生靜態內容。<!-- MAGECLOUD-1738 -->

   - `WARM_UP_PAGES` — 您可以列出要用來預先載入快取的頁面。 新增 [部署後變數](../environment/variables-post-deploy.md).

- ![修正圖示](../../assets/fix.svg) 修正本機套用的修補程式中斷執行個體部署的問題。 現在，ECE-Tools可以偵測到已套用修補程式。<!-- MAGECLOUD-982 -->

- ![修正圖示](../../assets/fix.svg) 修正JavaScript套件組合與GZIP功能之間的衝突。 現在，這些功能可正確搭配使用。<!-- MAGECLOUD-1735 -->

- ![修正圖示](../../assets/fix.svg) 修正使用舊版PHP 7.0.x時，造成ECE-Tools CLI指令失敗的問題。<!-- MAGECLOUD-1744 -->

- ![修正圖示](../../assets/fix.svg) 修正無法在多個執行緒中使用壓縮策略進行靜態內容部署的問題。<!-- MAGECLOUD-1822 -->

- ![修正圖示](../../assets/fix.svg) 修正造成管理員登入延遲的Redis工作階段鎖定問題。 此外，2.1.x也提供此修正。<!-- MAGECLOUD-1853 -->

## v2002.0.9

>[!NOTE]
>
>您必須 [升級Adobe Commerce on cloud infrastructure中繼資料](../dev-tools/install-package.md#update-the-metapackage) 以取得此專案及所有未來的更新。

- ![新圖示](../../assets/new.svg) **ece-tools** — 此 `ece-tools` 套件現在支援Adobe Commerce 2.1.x。<!-- MAGECLOUD-1086 -->

- ![新圖示](../../assets/new.svg) **Redis設定** — 您現在可以 [設定Redis](../environment/variables-deploy.md#cache_configuration) 頁面和預設快取以及Redis工作階段存放區（使用環境變數）。<!-- MAGECLOUD-1552 -->

- ![新圖示](../../assets/new.svg) **搜尋、AMQP和Redis服務改善** — 我們已整合服務設定流程，讓所有服務的運作方式都相同。 手動編輯 `env.php` 不再支援設定服務的檔案。 您必須使用 `.magento.env.yaml` 檔案而非。<!-- MAGECLOUD-1437 -->

- ![修正圖示](../../assets/fix.svg) **環境變數**—

   - 使用 `env:STATIC_CONTENT_THREADS` 已過時，並將在未來版本中移除。 使用 [SCD_THREADS](../environment/variables-deploy.md#scd_threads) 而非。<!-- MAGECLOUD-1507 -->

   - 此 `STATIC_CONTENT_EXCLUDE_THEMES` 環境變數已遭取代。 您必須使用 `SCD_EXCLUDE_THEMES` 環境變數。<!-- MAGECLOUD-1640 -->

- ![修正圖示](../../assets/fix.svg) **記錄** — 我們針對內建修補作業簡化了登入作業。<!-- MAGECLOUD-1674 -->

- ![修正圖示](../../assets/fix.svg) 已移除 `developer` 模式支援和 `APPLICATION_MODE` 環境變數，因為它們已導致非預期行為。<!-- MAGECLOUD-1615 -->

- ![修正圖示](../../assets/fix.svg) 我們已修正造成與Redis相關的靜態內容部署失敗的問題。 現在，多執行緒靜態內容部署可如預期般執行。<!-- MAGECLOUD-1630 -->

- ![修正圖示](../../assets/fix.svg) 已修正導致使用者無法儲存對Admin中設定欄位的修改的問題，這些修改在執行 `app:config:dump` 命令。<!-- MAGECLOUD-1175 -->

- ![修正圖示](../../assets/fix.svg) 新增對舊版的支援 `symfony/yaml` 修正與某些套件衝突，這些套件尚未與最新版本相容。<!-- MAGECLOUD-1674 -->

## v2002.0.8

>[!NOTE]
>
>我們已合併 `vendor/magento/ece-patches` 替換為 `vendor/magento/ece-tools` 在此版本中。 您不再需要更新 `vendor/magento/ece-patches` 另外封裝。

**新功能：**

- **改善的記錄**<!-- MAGECLOUD-1253 -MAGECLOUD-1495 -->
   - 我們改良了記錄訊息功能，以便在建置或部署程式覆寫環境變數時提供更好的解釋。
   - 您現在可以即時檢視安裝和升級進度。 追蹤 `install_update.log` 檔案以檢視進度。 例如，

     ```bash
     tail -f var/log/install_upgrade.log
     ```

- **新cron命令** — 您現在可以解除鎖定特定的cron工作，而不必使用停止並重新啟動所有工作 [`cron:unlock`](https://support.magento.com/hc/en-us/articles/360033099451) 命令。 在2.1中無法使用。<!-- MAGECLOUD-1367 -->

- **統一的設定檔** — 您現在可以使用設定建置和部署階段 [`.magento.env.yaml`](https://devdocs.magento.com/cloud/project/magento-env-yaml.html) 檔案。<!-- MAGECLOUD-1369 -->

- **備份組態檔** — 部署程式現在會自動建立 `app/etc/env.php` 和 `app/etc/config.php` 配置檔案部署後。 我們也新增了 [新增CLI命令](https://support.magento.com/hc/en-us/articles/360033182871) 從備份還原這些組態檔。<!-- MAGECLOUD-1372 -->

- **疑難排解驗證錯誤** — 我們變更了您必須在下列情況下用來解決驗證錯誤的指令： `config.php` 未包含足夠的資料用於靜態內容部署。 以前，錯誤訊息會指示您執行 `bin/magento app:config:dump`. 現在，您必須執行 `php ./vendor/bin/ece-tools config:dump`.<!-- MAGECLOUD-1491 -->

- **新環境變數** — 您現在可以使用環境變數來連線自訂 [搜尋](../environment/variables-deploy.md#search_configuration) 和 [AMQP型](../environment/variables-deploy.md#queue_configuration) 服務至您的網站。<!-- MAGECLOUD-1410 -->

- 我們實作智慧型修補。 現在，套件不是根據Adobe Commerce在雲端基礎結構版本上套用修補程式，而是根據修補的套件版本套用修補程式。<!--MAGECLOUD-1090-->

**已解決問題：**

- 我們已修正導致建置錯誤的記錄問題。<!-- MAGECLOUD-1162 -->

- 我們已修正以互動模式執行部署時，造成逾時例外的問題。<!-- MAGECLOUD-1389 -->

- 我們已修正使用壓縮策略產生靜態內容時導致錯誤的問題。 在2.1中無法使用。<!-- MAGECLOUD-1446 MAGECLOUD-1485-->

- 我們修正了部署指令碼無法正確識別中繼和生產環境的問題。<!-- MAGECLOUD-1493 -->

- 我們已修正導致網路問題中斷資料庫連線，以及在安裝和升級過程中導致失敗的問題。<!-- MAGECLOUD-1520 -->

- 我們已修正您無法使用匯出設定檔案的問題 `app:config:dump` 多次。 在2.1中無法使用。<!--  MAGECLOUD-1567  -->

- 我們已修正Redis工作階段 _鎖定_ 導致下列問題的原因： _管理員_ 登入延遲。 在2.1中無法使用。<!--  MAGECLOUD-1582  -->

- 我們修正了與版本設定相關的實作問題，此問題與其他以撰寫器為基礎的修補模組發生衝突。<!-- MAGECLOUD-1450 -->

- 我們已修正匯入期間造成PHP記憶體問題的問題。<!-- MAGECLOUD-1310 -->

- 已移除修補程式；修正中的錯誤 `colinmollenhour/credis` v1.6，在雲端基礎結構2.2.1上啟用對Adobe Commerce的支援。在2.1中無法使用。<!-- MAGECLOUD-1033 -->

## v2002.0.7

**已解決問題：**

- 已移除 `var/view_preprocessed` 符號連結，修正導致JavaScript縮制衝突的問題。<!-- MAGECLOUD-1454 -->

## v2002.0.6

**已解決問題：**

- 我們已修正導致以下問題的因素： `gzip` 當檔案或目錄名稱包含空格時發生錯誤。<!-- MAGECLOUD-1413 -->

- 已修正導致部署指令碼無法正確識別和啟用模組相依性的問題。<!-- MAGECLOUD-1424 -->

## v2002.0.5

**新功能：**

- **使用環境變數設定cron消費者** — 您現在可以使用新的 `CRON_CONSUMERS_RUNNER` 環境變數。

- **設定掃描** — 現在，我們會在建置/部署過程中掃描重要元件，如果掃描失敗，便會暫停該程式，避免網站處於維護模式而造成不必要的停機時間。

- **建置/部署通知** — 我們已新增一個組態檔，您可以 [設定Slack和/或電子郵件通知](../environment/set-up-notifications.md) 用於所有環境中的建置/部署動作。

- **靜態內容壓縮** — 我們現在壓縮靜態內容，使用 [gzip](https://www.gnu.org/software/gzip/) 建置和部署階段期間。 此壓縮搭配Fastly壓縮，有助於縮小存放區大小並提高部署速度。 如有必要，您可以使用停用壓縮 [建置選項](../environment/variables-build.md) 或 [部署變數](../environment/variables-deploy.md). 如需詳細資訊，請參閱下列主題：

   - [應用程式環境變數](../application/variables-property.md)

   - [靜態內容部署效能](../deploy/static-content.md)

   - [部署流程](https://devdocs.magento.com/cloud/reference/discover-deploy.html)

- **設定管理** — 現在會自動產生 `app/etc/config.php` 在建置階段期間，將檔案存在您的Git存放庫中（如果尚未存在）。 自動產生的檔案僅包含模組和副檔名的清單。 如果檔案已經存在，則建置階段會照常繼續。 如果您關注 [設定管理](../store/store-settings.md) 稍後，這些命令會更新檔案，而不需要其他步驟。 請參閱 [部署流程](https://devdocs.magento.com/cloud/reference/discover-deploy.html) 以取得詳細資訊。

- **資料庫傾印** — 我們已新增 `magento/ece-tools` 用於在所有環境中建立資料庫傾印的CLI命令。 對於Pro計畫生產環境，這個命令只會從三個高可用性節點中的一個轉儲，因此在轉儲期間寫入不同節點的生產資料可能不會被複製。 我們建議在生產環境中執行資料庫傾印之前，將應用程式置於維護模式。 另請參閱 [備份管理](https://devdocs.magento.com/cloud/project/project-webint-snap.html#db-dump) 以取得詳細資訊。

- **已解除Cron間隔限制** — 針對us-3、eu-3和ap-3區域中布建的所有環境的預設cron間隔為1分鐘。 所有其他地區的預設cron間隔為5分鐘（適用於Pro整合環境）和1分鐘（適用於Pro測試和生產環境）。 若要修改現有的cron工作，請編輯您的設定，位置在： `.magento.app.yaml` 或建立生產/測試環境的支援票證。 請參閱 [設定cron工作](../application/crons-property.md#set-up-cron-jobs) 以取得詳細資訊。

**已解決問題：**

- 我們已修正因叫用的部署程式而導致部署時間過長的問題 `cache-clean` 靜態內容部署之前的作業。<!-- MAGECLOUD-1327 -->

- 我們修正了在生產環境中部署的靜態內容產生步驟期間導致錯誤的問題。<!-- MAGECLOUD-1322 -->

- 我們已修正部分客戶無法存取的問題 `magento/ece-tools` 將輸出記錄到的命令 `stderr`.<!-- MAGECLOUD-1264 -->

- 我們已修正中無法提供基底URL值的問題 `env.php` 分支中的更新。<!-- MAGECLOUD-1242 -->

- 我們已修正導致此問題的原因： `magento setup:install` 命令以新增不安全的首碼(`http://`)以保護基底URL。<!-- MAGECLOUD-1171 -->

- 我們已修正修補程式錯誤不會導致部署失敗的問題。<!-- MAGECLOUD-1170 -->

- 我們已修正防止的問題 `ece-tools` 如果無法套用修補程式，會停止執行並擲回例外狀況。<!-- MAGECLOUD-1152 -->

- 我們已修正在管理員中啟用HTML縮制後，載入店面時造成錯誤的問題。<!-- MAGECLOUD-1138 -->

## v2002.0.4

**已解決問題：**

- 您現在可以 [手動重設停滯的cron工作](https://support.magento.com/hc/en-us/articles/360033099451) 透過SSH存取在所有環境中使用CLI命令。 部署程式會自動重設cron作業。<!-- MAGECLOUD-1355 -->

## v2002.0.3

**已解決問題：**

- 我們已修正由於Redis讀取/寫入時間過長而導致頁面逾時的問題。 您現在可以使用 `disable_locking` Redis設定中的引數以防止此問題。<!-- MAGECLOUD-1311 -->

## v2002.0.2

**已解決問題：**

- 此 [!DNL RabbitMQ] 設定程式現在會自動取得所有必要的引數。<!-- MAGECLOUD-1246 -->

## v2002.0.1

**新功能：**

- 雲端基礎結構上的Adobe Commerce現在支援範圍和 [靜態內容部署策略](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-static-deploy-strategies.html). 我們已新增 `–s` 引數及預設值 `quick` 用於靜態內容部署策略。 您可以使用環境變數 [SCD_STRATEGY](../environment/variables-deploy.md) 以自訂這些策略並搭配您的建置和部署動作使用。 此變數支援選項 `standard`， `quick`，或 `compact`. 如果您選取 `compact`，我們會覆寫 `STATIC_CONTENT_THREADS` 值 `1`，可能會減緩部署速度，尤其是在生產環境中。 在2.1中無法使用。<!--- MAGECLOUD-1057 -->

- 我們在環境上建立了記錄檔，以擷取及編譯建置和部署動作。 此 `var/log/cloud.log` 檔案位於根應用程式目錄中。<!--- MAGECLOUD-1014 & MAGECLOUD-1023 -->

**已解決問題：**

- 已重構 `ece-tools` 套裝，使其與雲端基礎結構2.2.0和更新版本上的Adobe Commerce相容。<!-- MAGECLOUD-919 & MAGECLOUD-1030 -->

- 我們已修正導致無法 `ece-tools` 如果無法套用修補程式，會停止執行並擲回例外狀況。<!-- MAGECLOUD-1186 -->

- 我們已修正導致在建置期間略過相依性插入(di)編譯時擲回例外狀況的問題。<!-- MAGECLOUD-1047 & MAGECLOUD-1049 -->

- 我們已修正導致部署程式覆寫中自訂Redis設定的問題 `env.php` 檔案。<!-- MAGECLOUD-1019 -->

- 我們已修正由於預設的安全管理員停用而導致重新導向回圈的問題。<!-- MAGECLOUD-1020 -->

## v2002.0.0

>[!WARNING]
>
>此套件不再與雲端基礎結構上的其他Adobe Commerce版本相容，並且 **不應** 使用。

### 初始發行

的初始版本 `ece-tools` 適用於Adobe Commerce on cloud infrastructure 2.2.0。
