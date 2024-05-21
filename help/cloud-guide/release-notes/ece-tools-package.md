---
title: ECE-Tools發行說明
description: 請參閱ECE-Tools套件的最新改良清單。
recommendations: noDisplay, catalog
last-substantial-update: 2024-05-21T00:00:00Z
exl-id: a464b940-c56e-4a7c-9948-559539e25361
source-git-commit: 923e2114270df22e134e0676ac97f84d770bb226
workflow-type: tm+mt
source-wordcount: '2929'
ht-degree: 0%

---

# ECE-Tools發行說明

此 [ece-tools](https://github.com/magento/ece-tools) package是一組指令碼和工具，用來管理和部署雲端專案。 此發行說明說明說明說明此套件的最新改善，此套件隸屬於 [適用於Commerce的Cloud Tools Suite](cloud-tools-suite.md).

>[!NOTE]
>
>另請參閱 [升級ECE-Tools](../dev-tools/update-package.md) 有關更新至最新版本的資訊 `ece-tools` 封裝。

此 `ece-tools` 套件會使用以下發行版本設定順序： `200<major>.<minor>.<patch>`

發行說明包括：

- ![新圖示](../../assets/new.svg) 新功能
- ![修正圖示](../../assets/fix.svg) 修正和改良

<!--Add release notes below-->

## v2002.1.19 {#latest}

發行日期： 2024年5月21日

- ![新圖示](../../assets/new.svg) **Lua** — 為CACHE_CONFIGURATION新增選項useLua。
- ![修正圖示](../../assets/fix.svg) **驗證器** — 更新新版Redis和RabbitMQ的驗證器。

## v2002.1.18

發行日期： 2024年4月8日

- ![新圖示](../../assets/new.svg) **PHP**  — 新增對PHP 8.3的支援。
- ![修正圖示](../../assets/fix.svg) 驗證器 — 已更新EOL驗證器。

## v2002.1.17

發行日期： 2024年1月16日

- ![修正圖示](../../assets/fix.svg) **Elasticsearch和OpenSearch的驗證器** — 修正啟用LiveSearch時，驗證器安裝搜尋服務時產生誤導性訊息的問題。<!-- MCLOUD-10167 -->
- ![修正圖示](../../assets/fix.svg) **部署警告** — 修正導致非空白資料夾出現部署警告的問題。<!-- MCLOUD-8958 -->

## v2002.1.16

發行日期： 2023年10月16日

- ![新圖示](../../assets/new.svg) **ENABLE_WEBHOOKS全域環境變數** — 已新增 [ENABLE_WEBHOOKS](../environment/variables-global.md#enable_webhooks) 與Commerce webhook搭配使用以連線至外部端點的全域變數，例如App Builder執行階段動作或協力廠商詳細目錄管理系統。

## v2002.1.15

發行日期： 2023年7月31日

- ![修正圖示](../../assets/fix.svg) **錯誤代碼** — 更新錯誤代碼結構描述和錯誤代碼檔案產生器。
- ![修正圖示](../../assets/fix.svg) **自訂Redis模型的驗證器** — 更新自訂Redis後端模型的驗證器。 [請參閱快取設定的範例](../environment/variables-deploy.md#cache_configuration).
- ![修正圖示](../../assets/fix.svg) **RabbitMQ的驗證器** — 新增RabbitMQ 3.11支援
- ![修正圖示](../../assets/fix.svg) **修正了錯誤的連結** — 修正歡迎電子郵件範本中入門檔案的錯誤連結。

## v2002.1.14

發行日期： 2023年3月10日

- ![新圖示](../../assets/new.svg) **PHP** — 新增對PHP 8.2的支援。
- ![新圖示](../../assets/new.svg) **服務的驗證器** — 更新Commerce 2.4.6必要服務的驗證器：MariaDB 10.6、Redis 7.0、PHP 8.2、OpenSearch 2.x和RabbitMQ 3.9。
- ![修正圖示](../../assets/fix.svg) **ece-tools db-dump** — 修正導致 `db-dump` 提前停止的作業。

## v2002.1.13

發行日期： 2022年10月27日

- ![新圖示](../../assets/new.svg) **新增對Adobe CommerceAdobe I/O事件的支援**. 擴充功能開發人員現在可以使用 [Adobe I/O事件](https://developer.adobe.com/events/docs/) 框架，可將雲端例項的Commerce事件資訊傳送至其為編寫的應用程式 [AdobeApp Builder](https://developer.adobe.com/app-builder/docs/overview/). Adobe Commerce的Adobe I/O事件位於「合作夥伴預覽」中。<!-- CEXT-932 -->
- ![新圖示](../../assets/new.svg) **OPcache設定的驗證器** — 新增驗證器，以檢查排除路徑的OPcache設定。<!-- MCLOUD-9485 -->
- ![修正圖示](../../assets/fix.svg) **修正GraphQL快取設定的問題** — 現在ECE-Tools保留了GraphQL `id_salt` 中的值 `cache` 中的設定 `app/etc/env.php` 檔案。<!-- MCLOUD-9486 -->

## v2002.1.12

發行日期： 2022年9月13日

- ![新圖示](../../assets/new.svg) **啟用`synchronous_replication`**—ECE-Tools集 `synchronous_replication=>true` 在 `app/etc/env.php` 檔案時間 `MYSQL_USE_SLAVE_CONNECTION` 已啟用。 此設定僅影響Commerce 2.4.6+。 請參閱 `MYSQL_USE_SLAVE_CONNECTION` 中的變數說明 [部署變數](../environment/variables-deploy.md#mysql_use_slave_connection).<!-- MCLOUD-9142 -->
- ![新圖示](../../assets/new.svg) **OpenSearch** — 新增配置和設定 `opensearch` 下一版Adobe Commerce 2.4.6的引擎。另請參閱 [設定OpenSearch服務](../services/opensearch.md).<!-- MCLOUD-9236 -->

## v2002.1.11

發行日期： 2022年8月4日

- ![修正圖示](../../assets/fix.svg) **ElasticSuite Validator和OpenSearch** — 修正安裝OpenSearch時的ElasticSuite完整性檢查驗證器問題。<!-- MCLOUD-8767 -->
- ![修正圖示](../../assets/fix.svg) **部署命令的傳回型別** — 修正部署命令的傳回型別。<!-- AC-3208 -->
- ![修正圖示](../../assets/fix.svg) **[!DNL RabbitMQ]全新Commerce 2.4.5安裝的問題** — 固定 [!DNL RabbitMQ] 安裝新Commerce 2.4.5時發生當機問題。<!-- MCLOUD-9059 -->

## v2002.1.10

發行日期： 2022年3月31日

- ![修正圖示](../../assets/fix.svg) **Elasticsearch7.10** — 更新驗證器以支援7.10版的Elasticsearch。<!-- MCLOUD-8548 -->

## v2002.1.9

發行日期： 2022年3月10日

- ![新圖示](../../assets/new.svg) **OpenSearch** — 新增對Adobe Commerce版本2.4.4、2.4.3-p2和2.3.7-p3的OpenSearch支援。<!-- MCLOUD-8296 -->
- ![新圖示](../../assets/new.svg) **PHP** — 新增對PHP 8.1的支援。
- ![修正圖示](../../assets/fix.svg) **symfony/process** — 新增與Symfony/處理序^5.3的相容性。<!-- MCLOUD-8283 -->

- ![新圖示](../../assets/new.svg) **取用者多重流程** — 新增 `multiple_processes` 選項，讓您能夠指定每個取用者要衍生的處理作業數目。 請參閱 `CRON_CONSUMERS_RUNNER` 中的變數說明 [部署變數](../environment/variables-deploy.md#cron_consumers_runner).<!-- MCLOUD-8295 -->
- ![新圖示](../../assets/new.svg) **OpenSearch配置和完整主機路徑** — 新增設定Elasticsearch配置和完整主機路徑的功能。
- ![修正圖示](../../assets/fix.svg) **AWS S3** — 變更啟用AWS S3的方法。
- ![修正圖示](../../assets/fix.svg) **修正driver_options讀取器** — 新增從資料庫連線讀取driver_options組態 `env.php` 檔案者 `ece-tools` 用於驗證器。<!-- MCLOUD-8420 -->

## v2002.1.8

發行日期： 2021年10月25日

- ![新圖示](../../assets/new.svg) **替代傾印位置** — 已新增 `--dump-directory` 選項，以便您為DB傾印選擇目標目錄。 現在 `/app/var/dump-main` 是資料庫傾印的預設目標目錄。 另請參閱 [備份管理：傾印您的資料庫](../storage/database-dump.md)<!-- MCLOUD-8063 -->
- ![修正圖示](../../assets/fix.svg) **更新獨白** — 更新 `monolog` 封裝到 `^2.3`.<!-- ACMP-1263 -->
- ![修正圖示](../../assets/fix.svg) **更新Symfony** — 更新Symfony相依性以與Adobe Commerce 2.4.4相容。<!-- ACMP-1533 -->
- ![修正圖示](../../assets/fix.svg) **功能/解決自動載入** — 修正部署至整合環境並看到 `CRITICAL: [9] Required configuration is missed in autoload section of composer.json file.` 錯誤。<!-- https://github.com/magento/ece-tools/pull/799 -->

## v2002.1.7

發行日期： 2021年7月29日

**設定更新**—

- ![新圖示](../../assets/new.svg) 新增對Composer 2.0的支援。<!--MCLOUD-8003-->

- ![修正圖示](../../assets/fix.svg) **更新下列專案的撰寫器需求`symphony/console`** — 更新ECE-Tools `composer.json` 的版本需求 `symphony/console` 修正導致此問題的套件 `di:compile` 命令失敗並出現以下錯誤： `Incompatible argument type: Required type: int. Actual type: string`<!--MC-42919-->

- ![修正圖示](../../assets/fix.svg) 更新軟體生命週期結束檢查(`eol.yaml`)以包含Elasticsearch7.9.x。<!--MCLOUD-7938-->

## v2002.1.6

發行日期： 2021年4月20日

- ![新圖示](../../assets/new.svg) **Redis驗證認證** — 新增從讀取Redis授權認證的功能 `relationships` 屬性。<!--MCLOUD-7694-->

- ![新圖示](../../assets/new.svg) **Elasticsearch授權認證** — 新增從以下位置讀取Elasticsearch授權認證的功能： `relationships` 屬性。<!--MCLOUD-7695-->

- ![新圖示](../../assets/new.svg) **專用工作階段儲存服務** — 已新增 `redis-session` 作為工作階段儲存的第二個選項。 您可以使用 `redis-session` 服務以儲存工作階段資訊並使用 `redis` 快取服務，以提供更優異的效能。<!--MCLOUD-7698-->

- ![新圖示](../../assets/new.svg) **已棄用的SPLIT_DB訊息** — 新增已棄用的驗證器警告和嚴重訊息 `SPLIT_DB` Adobe Commerce 2.4.2的選項及其在Adobe Commerce 2.5.0中的移除。<!--MCLOUD-7806-->

- ![修正圖示](../../assets/fix.svg) **從關係Elasticsearch版本** — 修正服務驗證器，以從擷取正確版本的Elasticsearch `relationships` Cloud Docker和整合環境中的屬性。<!--MCLOUD-7572-->

- ![修正圖示](../../assets/fix.svg) **彈性的Redis連線埠驗證**—Redis現在可以從驗證自訂快取連線中的連線埠， `server` URL。 例如，您可以將連線埠號碼新增至伺服器URL，如下所示： `server: 'tcp://rfs-store-simple-page-cache:26379'`. 這有助於防止出現下列驗證錯誤： `port` 選項遺失或不正確。<!--MCLOUD-7722-->

- ![修正圖示](../../assets/fix.svg) **升級至Adobe Commerce 2.4.2** — 修正使用者必須手動執行的問題 `bin/magento setup:upgrade` 在升級至Adobe Commerce 2.4.2後，讓網站可正常運作。<!--MCLOUD-7776-->

## v2002.1.5

發行日期： 2021年2月1日

- ![新圖示](../../assets/new.svg) **遠端儲存裝置** — 已新增 `REMOTE_STORAGE` 環境變數，可啟用雲端專案以使用儲存服務(例如AWS S3)遠端儲存媒體檔案。 此設定選項是ECE-Tools套件的一部分，但在雲端基礎結構上的Adobe Commerce上不受支援。<!--MCLOUD-7153-->

- ![新圖示](../../assets/new.svg) **新增 `cloud:config:validate` 命令** — 新增指令 `php vendor/bin/ece-tools cloud:config:validate` 驗證 `.magento.env.yaml` 將變更推送至遠端雲端環境前的設定。<!--MCLOUD-7120-->

- ![新圖示](../../assets/new.svg) **排清opcache** — 新增對 `opcache.enable_cli` PHP選項，可在執行部署掛接之前排清OPcache。 此組態會重設快取組態，以確保目前的組態設定會套用至每個部署。<!--MCLOUD-7015-->

- ![新圖示](../../assets/new.svg) **驗證Aurora DB** — 更新資料庫服務驗證，使其與Aurora資料庫相容。<!--MCLOUD-7269-->

- ![新圖示](../../assets/new.svg) **新增SCD_NO_PARENT環境變數** — 已新增 `SCD_NO_PARENT` 環境變數(適用於Adobe Commerce >=2.4.2)，以管理父系主題的靜態內容產生。<!--MCLOUD-7284-->

- ![修正圖示](../../assets/fix.svg) **記憶體限制和指令** — 修正以下問題 `php vendor/bin/ece-tools` 如果命令的大小為 `cloud.log` 檔案超出PHP memory_limit。 取代讀取整個 `cloud.log` 將檔案放入記憶體，我們現在只能從記錄檔讀取較小的資料子集。<!--MCLOUD-7275--><!--MCLOUD-7400-->

- ![修正圖示](../../assets/fix.svg) **自訂資料庫連線** — 修正 `.magento.env.yaml` 為定義自訂資料庫連線的設定問題 `DATABASE_CONFIGURATION` 未使用。 未將連線設定新增到 `app/etc/env.php`.<!--MCLOUD-7426-->

- ![修正圖示](../../assets/fix.svg) **空白的錯誤記錄檔** — 修正下列情況下導致部署失敗的問題： `cloud.error.log` 空白。<!--MCLOUD-7296-->

- ![修正圖示](../../assets/fix.svg) **MariaDB 10.3驗證** — 修正適用於Adobe Commerce 2.3.6-p1的MariaDB 10.3驗證。<!--MCLOUD-7416-->

- ![修正圖示](../../assets/fix.svg) **快取：排清記錄** — 改善記錄專案，以指示 `cache:flush` 步驟。<!--MCLOUD-7503-->

## v2002.1.4

發行日期： 2020年11月19日

- ![修正圖示](../../assets/fix.svg) 修正中指定搜尋引擎導致部署失敗的問題。 `SEARCH_CONFIGURATION` 環境變數是以外的值 `elasticsearch`.<!--MCLOUD-7283-->

## v2002.1.3

發行日期： 2020年11月9日

**基礎架構更新**—

- ![新圖示](../../assets/new.svg) 新增唯讀的ECE-Tools支援 `pub/static` 目錄（當靜態內容設定為在建置階段中部署時）。<!--MC-37699-->

- ![新圖示](../../assets/new.svg) 新增對Elasticsearch7.9和Redis 6的支援，以與即將發行的Adobe Commerce版本相容。<!--MCLOUD-7191-->

- ![修正圖示](../../assets/fix.svg) 更新ECE-Tools `composer.json` 為「品質修補工具」新增必要的相依性。 這修正了ECE-Tools和magento-cloud-patches套件之間存在的循環相依性。<!--MCLOUD-6910-->

**驗證和記錄改善**—

- ![新圖示](../../assets/new.svg) 新增搜尋引擎驗證，以確保 `elasticsearch` 設定用於Adobe Commerce on cloud infrastructure 2.4和更新版本。 如果驗證失敗，部署將停止，並顯示嚴重錯誤訊息，建議修正問題。 另請參閱 [嚴重錯誤，部署階段](../dev-tools/error-reference.md#deploy-stage).<!--MCLOUD-6937-->

- ![新圖示](../../assets/new.svg) 新增Elasticsearch驗證，以檢查Elasticsearch服務版本與Adobe Commerce版本之間的相容性。<!--MCLOUD-7193-->

- ![新圖示](../../assets/new.svg) 更新Elasticsearch相容性錯誤訊息，以顯示與Adobe CommerceElasticsearch模組相容的Elasticsearch版本。 錯誤訊息現在會提供要在您的雲端基礎結構中安裝的特定Elasticsearch版本，以便與您的Adobe Commerce版本使用的Elasticsearch模組相容。 另請參閱 [警告錯誤，部署階段](../dev-tools/error-reference.md#deploy-stage-1).<!--MCLOUD-6698-->

- ![新圖示](../../assets/new.svg) 已新增警告錯誤 `2026` 和 `2027` 無效 `MAGE_MODE` 環境變數設定。 唯一有效值為 `production`. 進行此修正之前， `MAGE_MODE` 可設為 `developer` 沒有部署錯誤，只會在稍後嘗試寫入唯讀檔案時造成錯誤。 另請參閱 [警告錯誤](../dev-tools/error-reference.md#warning-errors).<!--MCLOUD-6708-->

- ![修正圖示](../../assets/fix.svg) 修正Redis、RabbitMQ和MySQL服務的驗證，以確保這些版本與Adobe Commerce版本相容。 這些服務的有效版本現在會寫入 `cloud.log`.<!--MCLOUD-7098-->

- ![修正圖示](../../assets/fix.svg) 已更新 `cloud.log` 以納入快取熱身期間傳送要求的並行要求限制。 此值設定在 [WARMUP_CONCURRENCY](../environment/variables-post-deploy.md#warm_up_concurrency) 部署後變數。<!--MCLOUD-5563-->

**CLI命令更新**—

- ![新圖示](../../assets/new.svg) 新增CLI命令(`cloud:config:create` 和 `cloud:config:update`)以建立和更新 `.magento.env.yaml` 檔案的設定可包含一或多個建置、部署和部署後變數。 另請參閱 [從CLI建立組態檔](../environment/configure-env-yaml.md#create-configuration-file-from-cli).<!--MCLOUD-7072-->

**環境變數更新**—

- ![新圖示](../../assets/new.svg) 已新增 [SKIP_COMPOSER_DUMP_AUTOLOAD](../environment/variables-build.md#skip_composer_dump_autoload) 組建變數。 將變數設為 `true` 停止應用程式執行 `composer dump-autoload` 適用於Commerce安裝的Cloud Docker期間的命令。 變數僅與具有可寫入檔案系統（使用為測試和開發而建立的）的Commerce容器的Cloud Docker相關 `./vendor/bin/ece-docker build:compose --with-test`)。 使用這類安裝，略過 `composer dump-autoload` command可防止執行其他命令時發生錯誤，這些命令會嘗試從已刪除的檔案存取檔案 `generated` 目錄。<!--MCLOUD-6939-->

## v2002.1.2

發行日期： 2020年8月5日

**驗證和記錄改善**—

- ![新圖示](../../assets/new.svg) 已新增 `schema.error.yaml` 此檔案包含在建置、部署和部署後程式中可能發生的所有錯誤和警告通知，以及解決錯誤的建議。 此檔案中的資訊也可在 _Commerce雲端指南_. 另請參閱 [ece-tools的錯誤訊息參考](../dev-tools/error-reference.md).<!--MCLOUD-5878-->

- ![新圖示](../../assets/new.svg) 已變更雲端錯誤記錄(`/var/log/cloud.error.log`)專案，讓記錄檔更容易以程式設計方式剖析。<!--MCLOUD-5879-->

- ![新圖示](../../assets/new.svg) 新增其他錯誤檢查以建置、部署和部署後處理，並改善現有檢查：

   - 錯誤碼2026 — 無法將在建置階段產生的一些資料還原到掛載的目錄

   - 錯誤碼3004 — 無法建立備份檔案

   - 錯誤碼102 — 新增額外檢查，以找出在 `env.php` 檔案不可寫入 <!--MCLOUD-6221-->

- ![新圖示](../../assets/new.svg) 已新增 **品質PATCH** 環境變數，用來指定一或多個在建置過程中要套用的品質修補程式。 另請參閱 [建立變數](../environment/variables-build.md#quality_patches).<!--MCLOUD-6375-->

## v2002.1.1

發行日期： 2020年6月25日

- ![新圖示](../../assets/new.svg) **基礎架構更新**—

   - ![新圖示](../../assets/new.svg) **記錄功能改善** — 將退出代碼指派給嚴重的部署錯誤，並在錯誤訊息通知和記錄事件中公開退出代碼，藉此改善記錄追蹤功能。 另請參閱 [ece-tools的錯誤訊息參考](../dev-tools/error-reference.md).<!-- MCLOUD-5637, 5531-->

   - ![新圖示](../../assets/new.svg) 改善資料庫傾印程式(`vendor/bin/ece-tools db-dump`)並更新記錄訊息，以釐清資料庫傾印作業會將應用程式切換到維護模式、停止使用者佇列處理程式，以及在傾印開始之前停用cron作業。<!--MCLOUD-5324, MCLOUD-2062-->

   - ![修正圖示](../../assets/fix.svg) 已修正問題，以確保在部署到中繼和生產環境時，專案URL會正確更新。 現在， `ece-tools` 使用URL作為路由，並 `primary:true` 在專案路由設定中設定的屬性。 另請參閱 [部署變數](../environment/variables-deploy.md#update_urls).<!--MCLOUD-5883-->

   - ![修正圖示](../../assets/fix.svg) 已更新 `generate.xml` 建立套用修補程式的案例工作流程。 修補程式必須先套用，才能更新Adobe Commerce，修正可能導致 `di:compile` 和 `module:refresh` 失敗的步驟。<!--MCLOUD-5941-->

   - ![修正圖示](../../assets/fix.svg) 修正安裝程式中傳回 `Crypt key missing` 錯誤。 此 `crypt/key` 值會在安裝期間自動產生。<!--MCLOUD-6120-->

- ![新圖示](../../assets/new.svg) **服務更新**—

   - ![新圖示](../../assets/new.svg) 新增對PHP 7.4和MariaDB 10.4的支援。<!--MAGECLOUD-2957, MCLOUD-4144-->

- ![新圖示](../../assets/new.svg) **環境變數更新**—

   - ![新圖示](../../assets/new.svg) 已新增 **SCD_USE_BALER** 變數，以在Adobe Commerce雲端基礎結構建置程式中啟用JavaScript套裝的Baler模組。 請參閱中的變數說明 [建立變數](../environment/variables-build.md#scd_use_baler).<!-- MCLOUD-3456, MCLOUD-3457-->

   - ![新圖示](../../assets/new.svg) 已新增 **REDIS_BACKEND** 環境變數，可為Adobe Commerce 2.3.5或更新版本的Redis快取設定Redis後端模型。 請參閱中的變數說明 [部署變數](../environment/variables-deploy.md#redis_backend).<!--MCLOUD-5721, MCLOUD-5865-->

- ![新圖示](../../assets/new.svg) **CLI命令更新**—

   - ![新圖示](../../assets/new.svg) 更新下列CLI命令，並附上選項，以取得更詳細的記錄：

      - `app:config:dump`
      - `app:config:import`
      - `module:enable`

     每個呼叫的記錄層級由 [`VERBOSE_COMMANDS`](../environment/variables-build.md#verbose_commands) 中的變數 `.magento.env.yaml` 檔案。<!--MCLOUD-3503-->

- ![新圖示](../../assets/new.svg) **驗證改善**—

   - ![新圖示](../../assets/new.svg) **Elasticsearch 7.x相容性檢查** — 更新Elasticsearch7.x軟體相容性檢查的Elasticsearch驗證。<!--MCLOUD-5542-->

   - ![新圖示](../../assets/new.svg) **更新服務版本和EOL驗證檢查** — 更新驗證，以根據Adobe Commerce 2.4需求檢查已安裝的服務版本。<!--MCLOUD-6144-->

   - ![修正圖示](../../assets/fix.svg) 修正驗證問題，讓下列部署後警告訊息只有在 `post-deploy` 連結設定遺失 `.magento.app.yaml` 檔案：

     ```text
     Your application does not have the "post_deploy" hook enabled.
     ```

     <!--MCLOUD-4077-->

   - ![新圖示](../../assets/new.svg) **新增Zend Framework相依性的驗證** — 新增已移轉至Laminas專案的Zend架構的撰寫器相依性驗證。 如果缺少必要的相依性，則在建置過程中會顯示以下錯誤訊息。

     ```text
     Required configuration is missing from the autoload section of the composer.json file.
     Add ("Laminas\Mvc\Controller\Zend\": "setupsrc/ Zend/Mvc/Controller/") to
     the `autoload -> psr-4` section. Then, re-run the "composer update" command locally, and
     commit the updated composer.json and composer.lock files.
     ```

     另請參閱 [驗證Zend Framework相依性](../development/commerce-version.md#verify-zend-framework-composer-dependencies).<!--MCLOUD-4094-->

   - ![新圖示](../../assets/new.svg) **已新增的驗證 `env.php` 檔案和資料** — 新增檢查 `env.php` 在安裝和升級過程中產生的檔案和資料。<!--MCLOUD-5991-->

      - 如果 `env.php` 安裝遺失檔案，而且 `crypt/key` 值並未在 `.magento.app.yaml` 檔案時，部署會失敗，並出現以下通知：

        ```text
        The crypt/key key value does not exist in the ./app/etc/env.php file or the CRYPT_KEY cloud environment variable``Missing crypt key for upgrading Magento`.
        ```

      - 如果安裝不包含 `env.php` 檔案，或設定僅包含一個快取型別，則 `cron:enable` 命令會在升級過程中執行，以還原檔案 `cache_types`. 下列通知已新增至記錄檔：

        ```text
        Magento state indicated as installed but configuration file app/etc/env.php was empty or did not exist.
        Required data will be restored from environment configurations and from the .magento.env.yaml file.
        ```

## v2002.1.0

發行日期： 2020年2月6日

- ![新圖示](../../assets/new.svg) **基礎架構更新**—

   - ![新圖示](../../assets/new.svg) **為Commerce的Cloud Docker新增了單獨的包** — 將Docker封裝與分離 `ece-tools` 套件以維護程式碼品質並提供獨立的發行版本。 相關更新與修正 `ece-tools` 管理自 [magento-cloud-docker](https://github.com/magento/magento-cloud-docker) GitHub存放庫。<!--MAGECLOUD-2927-->

   - ![新圖示](../../assets/new.svg) **更新的修補功能** — 將修補功能從ECE-Tools套件移至另一個套件 [magento-cloud-patches](https://github.com/magento/magento-cloud-patches) 封裝。 部署期間， `ece-tools` 使用新套件套用修補程式。 另請參閱 [雲端修補程式發行說明](cloud-patches.md).<!--MAGECLOUD-4567-->

   - ![新圖示](../../assets/new.svg) **更新的Composer相依性** — 已更新 `composer.json` 雲端基礎結構上Adobe Commerce的檔案，其相依性為 `magento/magento-cloud-docker` 封裝。 現在， `ece-tools` 包含中所有套件的相依性 [`Cloud Tools Suite for Commerce`](cloud-tools-suite.md). 當您安裝或更新時，會自動安裝及更新這些套件 `ece-tools`.

- ![新圖示](../../assets/new.svg) **支援情境部署**—<!--MAGECLOUD-4101-->

   - ![新圖示](../../assets/new.svg) 現在您可以使用XML組態檔來自訂建置、部署和部署後程式，以覆寫或自訂預設組態。

   - ![新圖示](../../assets/new.svg) **已變更 `hooks` 中的設定`.magento.app.yaml`** — 我們已更新 `hooks` 設定格式以支援情境式部署。 舊版ECE-Tools 2002.0.x仍受支援。 不過，您必須更新為新格式，才能使用以案例為基礎的部署功能。 另請參閱 [以案例為基礎的部署](../deploy/scenario-based.md#add-scenarios-using-build-and-deploy-hooks).

>[!NOTE]
>
>在更新至ECE-Tools 2002.1.0版之前，請檢閱 [與舊版不相容的變更](backward-incompatible-changes.md) 瞭解可能需要您更新雲端基礎結構專案設定或流程上的Adobe Commerce的變更。

- ![新圖示](../../assets/new.svg) **服務更新**—

   - ![新圖示](../../assets/new.svg) 新增對PHP 7.3的支援。<!--MAGECLOUD-4022-->

   - ![新圖示](../../assets/new.svg) 新增對RabbitMQ 3.8的支援。<!--MAGECLOUD-4674-->

   - ![新圖示](../../assets/new.svg) 新增驗證，以對照每項服務的EOL日期檢查已安裝的服務版本。 現在，如果服務版本在EOL日期後的三個月內，客戶將會收到通知，如果EOL日期是過去，客戶將會收到警告。<!--MAGECLOUD-4076-->

   - ![修正圖示](../../assets/fix.svg) 修正Elasticsearch設定問題，以確保在所有環境中都設定了正確的Elasticsearch設定。<!--MAGECLOUD-4474-->

>[!NOTE]
>
>另請參閱 [服務版本](../services/services-yaml.md#service-versions) 如需雲端基礎結構上Adobe Commerce中所使用的服務清單，及其版本與雲端範本的相容性。

- ![新圖示](../../assets/new.svg) **環境變數更新**—

   - ![新圖示](../../assets/new.svg) 擴充的功能 `WARM_UP_PAGES` 環境變數，可支援特定產品頁面的快取預先載入。 請參閱中的展開定義 [部署後變數](../environment/variables-post-deploy.md#warm_up_pages) 主題。<!--MAGECLOUD-4444-->

   - ![新圖示](../../assets/new.svg) 已新增 `ERROR_REPORT_DIR_NESTING_LEVEL` 環境變數簡化中的錯誤報表資料管理 `<magento_root>/var/report/` 目錄。 請參閱中的變數說明 [建立變數](../environment/variables-build.md#error_report_dir_nesting_level) 主題。

   - ![修正圖示](../../assets/fix.svg) 已移除 `SCD_EXCLUDE_THEMES`， `STATIC_CONTENT_THREADS`，`DO_DEPLOY_STATIC_CONTENT`、和 `STATIC_CONTENT_SYMLINK` 環境變數。 另請參閱 [與舊版不相容的變更](backward-incompatible-changes.md#environment-configuration-changes).<!--MAGECLOUD-4407, MAGECLOUD-3873-->

   - ![修正圖示](../../assets/fix.svg) 修正彈性套裝設定程式的問題，以便在設定 `ELASTICSUITE_CONFIGURATION` 部署變數而不使用 `_merge` 選項。<!--MAGECLOUD-4388-->

- ![新圖示](../../assets/new.svg) **CLI命令更新**—

   - ![新圖示](../../assets/new.svg) **新cron命令** — 您現在可以在雲端基礎結構環境中，使用手動管理Adobe Commerce中的cron處理 `cron:disable` 和 `cron:enable` 命令。 使用disable命令可停止所有作用中的cron處理序，並停用所有cron工作。 使用enable指令可在準備就緒時重新啟用cron作業。 另請參閱 [停用cron工作](../application/crons-property.md#disable-cron-jobs).

   - ![新圖示](../../assets/new.svg) **改善錯誤報告** — 針對ECE-Tools處理期間發生的CLI命令失敗，新增更佳的記錄功能。<!--MAGECLOUD-4849-->

   - ![新圖示](../../assets/new.svg) **移除已棄用的組建命令** — 移除下列建置命令： `m2-ece-build`， `m2-ece-deploy`， `m2-ece-scd-dump`，並重新命名 `ece-tools docker` 命令 `ece-docker`. 另請參閱 [與舊版不相容的變更](backward-incompatible-changes.md)<!--MAGECLOUD-4392-->

- ![新圖示](../../assets/new.svg) 移除已棄用的 `build_options.ini` 並新增驗證，如果檔案存在，則建置會失敗。 使用 [.magento.env.yaml](../environment/configure-env-yaml.md) 檔案以設定建置選項。

- ![修正圖示](../../assets/fix.svg) 已修正導致建置流程失敗的問題，當 `config.php` 檔案是空的。<!--MAGECLOUD-4127-->

## 2002.0.23

發行日期： 2020年2月27日

- ![修正圖示](../../assets/fix.svg) 修正的相容性問題 `ece-tools` 2002.0.x版無法在生產模式中成功完成隨選靜態內容產生。

## 較舊的版本

請參閱 [發行說明封存](cloud-release-archive.md) 適用於2002.0.22版和更早版本。
