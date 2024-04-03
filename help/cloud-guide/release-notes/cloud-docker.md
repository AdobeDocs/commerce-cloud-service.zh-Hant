---
title: Cloud Docker包
description: 請參閱Cloud Docker套件最新改良的清單。
feature: Cloud, Docker, Release Notes
recommendations: noDisplay, catalog
last-substantial-update: 2023-07-31T00:00:00Z
exl-id: 907d977f-2e9c-4553-a46b-000bc6a57b28
source-git-commit: 21754f2ee3df586cd03d57210741b36409ad2b36
workflow-type: tm+mt
source-wordcount: '3620'
ht-degree: 0%

---

# Cloud Docker包

此 [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker) 套件提供將Adobe Commerce部署到本機雲端環境的功能和Docker影像。 本發行說明說明說明說明此套件的最新改善，此套件為的元件 [Cloud Tools Suite for Commerce](cloud-tools-suite.md).

此 `magento/magento-cloud-docker` 套件會使用以下版本順序： `<major>.<minor>.<patch>`

發行說明包括：

- ![新圖示](../../assets/new.svg) 新功能
- ![修正圖示](../../assets/fix.svg) 修正和改良

<!--Add release notes below-->

## v1.3.6 {#latest}

發行日期： 2023年7月31日

- ![新圖示](../../assets/new.svg) **已新增新的服務版本**—OpenSearch 2.5。
- ![新圖示](../../assets/new.svg) **啟用撰寫器快取** — 現在您可以擴展Docker設定，以在啟動Docker容器時啟用Composer清除快取。 另請參閱 [擴展Docker配置](https://developer.adobe.com/commerce/cloud-tools/docker/configure/extend-docker-configuration/) 在 _Cloud Docker for Commerce_ 指南。

## v1.3.5

發行日期： 2023年3月10日

- ![新圖示](../../assets/new.svg) **ionCube** — 新增PHP 8.1影像的ionCube擴充功能。
- ![新圖示](../../assets/new.svg) **已新增新的服務版本**—OpenSearch 2.3和2.4、PHP 8.2、Varnish 7.1.1。
- ![新圖示](../../assets/new.svg) **PHP 8.2的增強支援** — 已修正某些PHP 8.2.x版本的相容性問題，以支援Commerce 2.4.6。
- ![修正圖示](../../assets/fix.svg) **Composer問題** — 修復在Docker容器中更新Composer版本後發生的問題。

## v1.3.4

發行日期： 2022年10月27日

- ![新圖示](../../assets/new.svg) **已新增光澤影像** — 新增Varnish 6.5、7.0和7.1的影像。<!-- MCLOUD-7879 -->

## v1.3.3

發行日期： 2022年9月13日

- ![新圖示](../../assets/new.svg) **Apple M1 (ARM64)支援** — 新增對Docker影像的變更，以啟用對Apple M1 (ARM64)架構的支援。<!-- MCLOUD-7989-2 MCLOUD-7989 -->
- ![修正圖示](../../assets/fix.svg) **Mailhog** — 修正Mailhog服務在開發人員模式中未收到電子郵件的問題。<!-- MCLOUD-8643 -->
- ![修正圖示](../../assets/fix.svg) **init-docker.sh** — 修正中的服務版本驗證器 `init-docker.sh` 指令碼。<!-- MCLOUD-8765 -->

## v1.3.2

發行日期： 2022年3月31日

- ![新圖示](../../assets/new.svg) **新增Elasticsearch7.10影像**<!-- MCLOUD-8548 -->

## v1.3.1

發行日期： 2022年3月10日

- ![新圖示](../../assets/new.svg) **支援PHP 8.1** — 新增對PHP 8.1的支援。
- ![新圖示](../../assets/new.svg) **OpenSearch** — 新增OpenSearch 1.1和1.2版的影像。
- ![新圖示](../../assets/new.svg) **Composer 2.1** — 在PHP 8.x影像中預設設定composer 2.1.x。
- ![新圖示](../../assets/new.svg) **PHP影像改善**—

   - 新增PHP 8.1影像
   - 已升級xDebug 3.1.2版
   - 已升級xmlrpc 1.0.0RC3

- ![修正圖示](../../assets/fix.svg) **Elasticsearch和OpenSearch改進** — 改善Elasticsearch和OpenSearch Dockerfiles；移除Elasticsearch5.2影像。
- ![修正圖示](../../assets/fix.svg) **鈉鹽延伸** — 啟用 `sodium` 副檔名預設為所有PHP影像。
- ![修正圖示](../../assets/fix.svg) **撰寫器快取磁碟區** — 修正Composer快取磁碟區具有快取Composer套件的路徑。
- ![修正圖示](../../assets/fix.svg) **Nginx中的記憶體限制** — 修正NGINX影像中的記憶體限制。

## v1.3.0

發行日期： 2021年10月25日

- ![修正圖示](../../assets/fix.svg) **改善開發人員模式工作流程** — 之前，您需要在建置和部署步驟中指定模式。 現在， `--mode` 中的選項 `build` 步驟會在稍後決定模式 `deploy` 步驟。 不再需要於部署後設定模式。 另請參閱 [開發人員模式](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html).<!-- ACMP-1086 -->
- ![修正圖示](../../assets/fix.svg) **改善唯讀檔案系統**—<!-- ACMP-1106 -->
   - 修正啟動郵件設定的PHP容器問題。
   - 可以在INI檔案中使用環境變數。
   - 請確定PHP進入點不需要寫入許可權。
- ![修正圖示](../../assets/fix.svg) **更新節點** — 更新隨附的Node版本；在PHP-CLI映像中安裝Node時，現在會使用目前的LTS版本。<!-- ACMP-1539 -->
- ![修正圖示](../../assets/fix.svg) **更新Symfony** — 更新Symfony設定相依性，以與Adobe Commerce 2.4.4相容。<!-- ACMP-1533 -->

## v1.2.4

發行日期： 2021年7月29日

- ![新圖示](../../assets/new.svg) **新增 `Zookeeper` 容器** — 新增 [Zookeeper容器](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#zookeeper-container) 若要管理未部署至雲端基礎結構上Adobe Commerce之專案的鎖定提供者設定。<!--MCLOUD-8000-->

- ![新圖示](../../assets/new.svg) **新增對Composer 2.0的支援。** — 將Composer 2.0版新增至Composer設定檔案，以支援即將終止的Composer 1.0升級。<!--MCLOUD-8003-->

## v1.2.3

發行日期： 2021年6月14日

- ![新圖示](../../assets/new.svg) **已新增PHP 8.0** — 將PHP更新至8.0版，讓您能夠利用PHP 8.0包含的所有新功能和最佳化。<!--MCLOUD-7941-->
- ![新圖示](../../assets/new.svg) **更新至亮漆6.6和Elasticsearch7.11.2** — 下列連結提供發行資訊： [清漆快取6.6](https://varnish-cache.org/releases/rel6.6.0.html#rel6-6-0) 和Elasticsearch7.11.2。<!--MCLOUD-7921-->
- ![新圖示](../../assets/new.svg) **已新增 `ioncube` PHP 7.4影像的擴充功能** — 此 `ioncube` 擴充功能在最初從PHP 7.3升級至PHP 7.4後被排除後，已重新新增到PHP 7.4映像中。 *[由mattskr提交](https://github.com/magento/magento-cloud-docker/pull/314).*<!--PR #314-->
- ![新圖示](../../assets/new.svg) **新增檔案同步選項：`manual-native`** — 此 `manual-native` 檔案同步選項提供手動同步控制功能，可為macOS和Windows環境提供最佳效能。 閱讀有關使用 `manual-native` 中的選項 [開發人員模式](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) 和 [在Docker開發人員環境中同步資料](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html#file-synchronization-options).<!--MCLOUD-7977-->
- ![新圖示](../../assets/new.svg) **已從移除磁碟區刪除 `up` 和 `down` 命令** — 此 `--volume` 選項已從中移除 `bin/magento-docker up` 和 `bin/magento-docker down` 命令，取代為新的 `bin/magento-docker init` 具有資料遺失警告的命令。 此變更有助於防止意外資料遺失。 *[由joeshelton-wagento提交](https://github.com/magento/magento-cloud-docker/pull/319).*<!--PR #319-->
- ![修正圖示](../../assets/fix.svg) **已更新 `CN` 所產生憑證的值** — 移除硬式編碼 `CN` Dockerfile的值。 此值已建立憑證錯誤(`NET::ERR_CERT_INVALID`)而導致 `--host` 的選項 `ece-docker build:compose` 要忽略的命令。<!--MCLOUD-7934-->

## v1.2.2

發行日期： 2021年4月20日

- ![新圖示](../../assets/new.svg) **已更新 `host.docker.internal` 獨立於平台** — 您現在可以為Ubuntu、Windows和macOS建立相同的Docker撰寫指令碼。 在Ubuntu上使用Xdebug不再需要個別的環境變數。 [由Igor Vitol提交的修正](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #298-->
- ![新圖示](../../assets/new.svg) **已更新init-docker.sh** — 已新增 `mounts` 物件至 `MAGENTO_CLOUD_APPLICATION` 環境變數。 [由Chiranjevi提交的修正](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #299-->
- ![新圖示](../../assets/new.svg) **已更新init-docker.sh** — 已更新 `init-docker.sh` PHP 7.4和Cloud Docker 1.2.1版本的指令碼。 [由Adarsh Manickam提交的修正](https://github.com/magento/magento-cloud-docker/pull/300).<!--Issue #300-->
- ![新圖示](../../assets/new.svg) **鈉預設為啟用** — 啟用 `sodium` PHP Docker映像中預設的PHP副檔名。<!--MCLOUD-7548-->
- ![新圖示](../../assets/new.svg) **`custom-registry`選項** — 新增 `--custom-registry` 選項至 `php ./vendor/bin/ece-docker build:compose` 使用您自己的影像登入的命令。<!--MCLOUD-7476-->

  ```bash
  ./vendor/bin/ece-docker build:compose --custom-registry=my-registry.example.com
  ```

- ![新圖示](../../assets/new.svg) **已移除舊Elasticsearch版本** — 從Elasticsearch影像中移除了Elasticsearch版本1.7和2.4。<!--MCLOUD-7504-->
- ![新圖示](../../assets/new.svg) **自動產生NGINX憑證** — 從NGINX影像中移除現有的憑證。 現在，每次新部署都會自動產生NGINX憑證，以提高安全性。<!--MCLOUD-7396-->
- ![修正圖示](../../assets/fix.svg) **已啟用`opcache.validate_timestamps`** — 啟用 `opcache.validate_timestamps` 開發人員模式中的PHP預設設定。 啟用此設定修復了無法在Docker中識別檔案系統變更的問題。<!--MCLOUD-7466-->
- ![修正圖示](../../assets/fix.svg) **固定`build:custom:compose`** — 已修正 `build:custom:compose` 在建置過程中無法覆寫檔案時擲回錯誤的命令。 擲回錯誤可避免以下情況 `docker-compose up` 可能使用了錯誤的檔案。<!--MCLOUD-7457-->
- ![修正圖示](../../assets/fix.svg) **固定 `--sync_engine="native"` 選項** — 修正生產模式(`--mode="production"`)， `--sync_engine="native"` 選項不會為中的本機資料夾建立任何專案 `docker.composer.yml` 檔案。<!--MCLOUD-7254-->
- ![修正圖示](../../assets/fix.svg) **修正服務版本驗證錯誤** — 新增的服務版本 [!DNL RabbitMQ]、Elasticsearch和其他服務 `type` 中的屬性 `MAGENTO_CLOUD_RELATIONSHIP` 變數中。 將這些版本新增至 `relationships` 變數修正了部署階段發生的驗證錯誤。<!--MCLOUD-7572-->

## v1.2.1

發行日期： 2020年12月21日

- ![新圖示](../../assets/new.svg) **NGINX指令選項** — 新增建置指令選項以變更NGINX的數目 `worker_processes` 和NGINX `worker_connections` 用於TLS和Web服務。 此 `worker_process` 引數會保留將值設為 `auto`. 範例： <!--MCLOUD-7259-->

  ```terminal
  ./vendor/bin/ece-docker build:compose --nginx-worker-processes=2
  ./vendor/bin/ece-docker build:compose --nginx-worker-connections=2048
  ```

- ![新圖示](../../assets/new.svg) **TLS命令選項** — 已新增建立命令選項，以建立不含TLS服務的組態。 範例： <!--MCLOUD-7259-->

  ```terminal
  ./vendor/bin/ece-docker build:compose --no-tls
  ```

- ![新圖示](../../assets/new.svg) **NGINX記憶體耗用量** — 減少NGINX流程用於TLS和Web服務的記憶體。<!--MCLOUD-7259-->

- ![新圖示](../../assets/new.svg) **Blackfire** — 在Cloud Docker映像中預設禁用BlackfirePHP擴展。

- ![修正圖示](../../assets/fix.svg) **PHP-FPM容器** — 已透過變更 `WEB_PORT` 從 `80` 至 `8080`.<!--MCLOUD-7232-->

- ![修正圖示](../../assets/fix.svg) **無效的磁碟區命名** — 修正開發人員模式中磁碟區命名無效的錯誤。<!--MCLOUD-7442-->

- ![修正圖示](../../assets/fix.svg) **NGINX上游連線埠** — 更新Docker NGINX 1.19影像以使用連線埠8080以避免無限回圈。 [由Adarsh Manickam提交的修正](https://github.com/magento/magento-cloud-docker/pull/296).<!--Issue 295-->

## v1.2.0

發行日期： 2020年11月9日

- ![新圖示](../../assets/new.svg) **容器更新 —**

   - ![新圖示](../../assets/new.svg) **PHP-FPM容器** — 新增對gnupg PHP擴充功能的支援。 [Zilker Technology的G Arvind提交的修正](https://github.com/magento/magento-cloud-docker/pull/210).<!--MCLOUD-5981-->

   - ![修正圖示](../../assets/fix.svg) **資料庫容器** — 將必要的資料庫密碼新增至健康狀態檢查命令，以修正資料庫容器健康狀態檢查。<!--MCLOUD-7122-->

   - ![新圖示](../../assets/new.svg) **Elasticsearch容器**

      - 新增對Elasticsearch7.9的支援，以與即將發行的Adobe Commerce版本相容。<!--MCLOUD-7190-->

      - **Elasticsearch外掛程式設定** — 新增支援以使用來自的Elasticsearch外掛程式設定資訊 `services.yaml` 要產生 `docker-compose.yaml` Cloud Docker for Commerce環境的檔案。 另請參閱 [Elasticsearch外掛程式](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-plugins).<!--MCLOUD-2789-->

      - **Elasticsearch外掛程式支援** — 新增對下列Elasticsearch外掛程式的支援： `analysis-icu`， `analysis-phonetic`， `analysis-stempel`、和 `analysis-nori`. 此 `analysis-icu` 和 `analysis-phonetic` 外掛程式預設會安裝。 您可以新增或移除 `analysis-stempel` 和 `analysis-nori` 外掛程式（如需要）。<!--MCLOUD-2789-->

   - ![新圖示](../../assets/new.svg) **CLI容器**

      - **在Docker PHP容器中執行命令** — 現在您可以使用Cloud Docker CLI在Docker環境中的PHP容器內執行命令，而無需在主機上安裝PHP。 例如，以下命令會建置組態：  `./bin/magento-docker php 7.3 vendor/bin/ece-docker build:compose`. 另請參閱 [Cloud Docker CLI](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli). [Zilker Technology的G Arvind提交的修正](https://github.com/magento/magento-cloud-docker/pull/209).<!--MCLOUD-5982-->

      - 將OpenSSH-client新增至PHP CLI容器。 現在，您可以在下列情況下使用Composer的ssh代理轉送： `composer.json` 檔案包含私人Git存放庫，需要ssh使用者端使用撰寫器命令。<!--MCLOUD-6008-->

   - ![修正圖示](../../assets/fix.svg) **TLS容器** — 現在， [TLS容器](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) 是根據 `https://hub.docker.com/r/magento/magento-cloud-docker-nginx` Docker影像，而不是CentOS影像。 此變更修正了在Cloud Docker環境中的容器之間傳送HTTPS請求時導致錯誤的問題。<!--MCLOUD-6469-->

   - ![新圖示](../../assets/new.svg) **測試容器** — 新增用於應用程式測試的測試容器，並新增 `--with-test` Docker的選項 `build:compose` 僅在Docker環境中測試時建立容器的命令。 另請參閱 [應用程式測試](https://devdocs.magento.com/cloud/docker/docker-test-app-mftf.html).<!--MCLOUD-6394-->

   - ![新圖示](../../assets/new.svg) **FPM-XDEBUG容器**

      - ![新圖示](../../assets/new.svg) **在Linux上設定Xdebug** — 已新增 `--set-docker-host` 的選項 `ece-docker build:compose` 命令以配置 `host.docker.internal` Xdebug容器的值。 必須在Linux系統上使用Xdebug才能使用此選項。 另請參閱 [為Docker配置Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-6430-->

      - ![修正圖示](../../assets/fix.svg) 修正Docker ENTRYPOINT要解析的Xdebug變數設定 `uninitialized "with_xdebug" variable` 記錄檔中有錯誤。 [修正由Florent Olivaud提交](https://github.com/magento/magento-cloud-docker/pull/218)<!--MCLOUD-6043-->

- ![新圖示](../../assets/new.svg) **Docker設定變更**

   - **MailHog設定** — 現在您可以使用下列 `ece-docker build:compose` 用來停用MailHog並指定連線埠的命令選項： `--no-mailhog`， `--mailhog-http-port`、和 `--mailhog-smtp-port`. 另請參閱 [設定電子郵件](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-6898, MCLOUD-6660-->

   - 對於Cloud Docker for Commerce 1.2.0和更新版本，Adobe現在為每個修補版本提供Docker影像，Docker配置生成器使用指定的修補版本建立Docker配置，而不是使用最新的修補版本。 以前，Docker配置生成器使用最新修補版本構建配置，這可能破壞使用早期版本構建的Cloud Docker for Commerce環境。<!--MCLOUD-7093-->

   - **在自訂Cloud Docker設定中指定自訂影像和版本** — 已更新 `build:custom:compose` 命令與選項，用於指定產生自訂Docker構成組態檔案時的自訂影像和版本(`docker-compose.yaml`)。 另請參閱 [構建自訂Docker撰寫配置](https://devdocs.magento.com/cloud/docker/docker-config-sources.html#build-a-custom-docker-compose-configuration). <!--MCLOUD-7089-->

   - 更新Docker主機配置以公開連線埠443以啟用Adobe Commerce存取(`https://magento2.docker`)。 您可以新增預設連線埠 `--tls-port` 選項來產生Docker設定檔案。<!--MCLOUD-6806-->

- ![修正圖示](../../assets/fix.svg) 修復了以下情況下導致Cloud Docker for Commerce構建失敗的問題： `app/etc/env.php` 檔案已存在。<!--MCLOUD-6732-->

- ![修正圖示](../../assets/fix.svg) 更新組建設定，以使用一般磁碟區取代具名磁碟區，以防止在Linux或Linux版Windows子系統(WSL2)上部署Cloud Docker for Commerce時發生問題。<!--MCLOUD-6732-->

- ![修正圖示](../../assets/fix.svg) 更新Cloud Docker for Commerce功能測試以支援Composer 2.0。<!--MCLOUD-7183-->

## v1.1.2

發行日期： 2020年9月9日

- ![新圖示](../../assets/new.svg) 新增對Elasticsearch7.7的支援<!--MCLOUD-6219-->

## v1.1.1

發行日期： 2020年8月5日

- ![修正圖示](../../assets/fix.svg) **已更新電子郵件設定** — 更新預設的Cloud Docker for Commerce設定以支援MailHog服務，而不使用SendMail。 另請參閱 [設定電子郵件](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-5624-->

- ![修正圖示](../../assets/fix.svg) 已將PS資料庫還原至Cloud Docker環境設定以進行修正 `ps:  command not found` 錯誤。<!--MCLOUD-6621-->

- ![修正圖示](../../assets/fix.svg) 更新預設的Cloud Docker for Commerce設定，移除要修正的資料庫入口點和MariaDB磁碟區的自動掛載 `Cannot create container for service db` 啟動Cloud Docker環境時可能發生的錯誤。

  現在，您可以透過將以下選項新增到 `ece-docker build:compose` 命令： `--with-entry-point` 和 `with-mariadb-conf`. 另請參閱 [服務組態選項](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-6424-->

- ![新圖示](../../assets/new.svg) **CLI命令更新**

| 動作 | 命令 |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| 將入口點新增至資料庫容器，以便從備份還原資料庫 | `./vendor/bin/ece-docker build:compose --db --with-entrypoint` |
| 新增MariaDB設定磁碟區 | `./vendor/bin/ece-docker build:compose --db --mariadb-conf` |

## v1.1.0

發行日期： 2020年6月25日

- ![新圖示](../../assets/new.svg) **新增對分割資料庫效能解決方案的支援** — 現在您可以使用Cloud Docker環境中的分割資料庫效能解決方案來設定和部署存放區。<!--MCLOUD-3740-->

- ![新圖示](../../assets/new.svg) **支援Adobe Commerce和Magento Open Source部署** — 現在，您可以使用Cloud Docker for Commerce來部署本機開發環境，用於未在雲端基礎結構上的Adobe Commerce上託管的專案。<!--MCLOUD-5667-->

- ![新圖示](../../assets/new.svg) **Blackfire.io支援** — 新增支援以使用 [Blackfire.io擴充功能](https://devdocs.magento.com/cloud/docker/docker-config-blackfire-io.html) 以進行自動化效能測試。 [Adarsh Manickam提交的修正（來自Zilker Technology）](https://github.com/magento/magento-cloud-docker/pull/202)<!--MCLOUD-5857-->

- ![新圖示](../../assets/new.svg) **容器更新**

   - **亮漆** — 現在，當您使用支援的雲端應用程式範本版本在Cloud Docker環境中部署Adobe Commerce時，Varnish是預設的快取。 另請參閱 [清漆容器](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container).<!--MCLOUD-2634-->

   - 已新增 `--no-varnish` 產生Cloud Docker設定檔案時，可略過Varnish服務安裝的選項。<!--MCLOUD-2634-->

   - ![新圖示](../../assets/new.svg) **資料庫**

      - 新增對MySQL資料庫的支援。 現在，您可以使用MariaDB或MySQL來設定Cloud Docker環境。 另請參閱 [服務組態選項](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-5691-->

      - 新增在產生Docker構成檔案時設定資料庫複製的增量與位移設定的功能。 另請參閱 [服務容器](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers).<!--MCLOUD-5735-->

   - ![新圖示](../../assets/new.svg) **PHP-FPM**

      - 新增對PHP 7.4的支援。 [Zilker Technology的Mohanela Murugan提交的修正](https://github.com/magento/magento-cloud-docker/pull/198)<!--MCLOUD-198-->

      - 新增複製 `php.ini` 將根專案目錄中的檔案套用至Cloud Docker環境，並將自訂PHP設定套用至PHP-FPM和CLI容器。 另請參閱 [自訂PHP設定](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#customize-php-settings). [Zilker Technology的Mathew Beane提交的修正](https://github.com/magento/magento-cloud-docker/pull/130).<!--MCLOUD-6012-->

      - 新增容器健康狀態檢查。 [Visanth Sampath提交的修正（來自Zilker Technology）](https://github.com/magento/magento-cloud-docker/pull/188).<!--MCLOUD-5752-->

   - ![修正圖示](../../assets/fix.svg) **Node.js** — 將預設Node.js版本從第8版更新為第10版以提高安全性。 Node.js版本8已過時，不再透過錯誤修正或安全性修補程式進行更新。 [Zilker Technology的Mohan Elamurugan提交的修正](https://github.com/magento/magento-cloud-docker/pull/183).<!--MCLOUD-5586-->

   - ![新圖示](../../assets/new.svg) **Elasticsearch**

      - 新增對Elasticsearch6.8、7.2、7.5和7.6的支援。<!--MCLOUD-4050, MCLOUD-5855,MCLOUD-5860-->

      - 新增自訂 [Elasticsearch容器設定](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) 生成Docker構成配置檔案時。<!--MCLOUD-3059-->

      - 已新增 `--no-es` 用於生成Docker構成配置檔案的服務配置選項的選項。 使用此選項可略過Elasticsearch容器安裝，並改用MySQL搜尋。 此選項僅支援Adobe Commerce 2.3.5版和更早版本。<!--MCLOUD-3766-->

   - ![新圖示](../../assets/new.svg) **FPM-XDEBUG容器** — 新增了服務配置選項，用於在Cloud Docker環境中安裝和配置Xdebug以偵錯PHP。 另請參閱 [設定Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-4098-->

- ![新圖示](../../assets/new.svg) **Docker設定變更**

   - 新增PHP-FPM、Redis、Elasticsearch和MySQL Docker服務容器的健康狀態檢查。<!--MCLOUD-3335 and MCLOUD-5856-->

   - 將預設檔案同步處理模式變更為 `native` 在開發人員模式中。<!--MCLOUD-3890 -->

   - 在產生 `docker-compose.yml` 檔案。<!--MCLOUD-3878-->

   - 透過增加以下專案改善處理來自上游PHP-FPM容器的大型回應的能力： `fastcgi_buffers` Nginx伺服器的值。<!--MCLOUD-5980-->

   - 透過新增第二個同步工作階段來同步處理中的檔案，改善突變檔案同步處理效能。 `vendor` 目錄。 此變更可防止誘變在檔案同步程式期間卡住。 [Zilker Technology的Mathew Beane提交的修正](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

   - ![新圖示](../../assets/new.svg) **CLI命令更新**

| 動作 | 命令 |
| -------- | --------------- |
| 清除Redis快取 | `bin/magento-docker flush-redis` |
| 清除清漆快取 | `bin/magento-docker flush-varnish` |
| 略過預設清漆安裝 | `.vendor/bin/ece-docker build:compose --no-varnish`<!--MCLOUD-2634--> |
| [自訂Elasticsearch選項](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --es-env-var`<!--MCLOUD-3059--> |
| [移除Elasticsearch設定](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --no-es`<!--MCLOUD-3766--> |
| 使用MySQL 5.6或5.7版設定資料庫容器 | `./vendor/bin/ece-docker build:compose --db <mysql-version-number> --db-image mysql`<!--MCLOUD-5691--> |
| 指定自訂基底URL | `./vendor/bin/ece-docker build:compose --host=<hostname> --port=<port-number>`<!--MCLOUD-3063--> |
| [新增Xdebug設定的容器](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) | `.vendor/bin/ece-docker build:compose --mode developer --sync-engine native --with-xdebug`<!--MCLOUD-4098--> |

- ![修正圖示](../../assets/fix.svg) 修正了變體檔案同步的設定，以防止變體建立陳舊的工作階段。 [Zilker Technology的Mathew Beane提交的修正](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

- ![修正圖示](../../assets/fix.svg) 修復了在啟動PHP-FPM容器時導致Docker撰寫日誌語法錯誤的一個配置問題。 [Zilker Technology的Mathew Beane提交的修正](https://github.com/magento/magento-cloud-docker/pull/129)<!--MCLOUD-3958-->

- ![修正圖示](../../assets/fix.svg) 修復了在使用多個Docker環境時有時發生的卷冊衝突錯誤。 [Zilker Technology的G Arvind提交的修正](https://github.com/magento/magento-cloud-docker/pull/168).

- ![修正圖示](../../assets/fix.svg) 已修正導致 `ece-docker build:compose` 如果組態包含Blackfire.io，命令會失敗。 [Zilker Technology的G Arvind提交的修正](https://github.com/magento/magento-cloud-docker/pull/199). <!--MCLOUD-5797-->

- ![修正圖示](../../assets/fix.svg) 更新PHP CLI影像設定，以防止使用Cloud Docker for Commerce安裝多個套件時發生記憶體不足錯誤。 [Zilker Technology的Mohan Elamurugan提交的修正](https://github.com/magento/magento-cloud-docker/pull/197).*<!--MCLOUD-5818-->

- ![修正圖示](../../assets/fix.svg) 在Cloud Docker環境中新增對多位MySQL使用者的支援。 在舊版中， `build:compose` 作業失敗，如果 `magento.app.yaml` 檔案指定了多個資料庫使用者。 [Zilker Technology的G Arvind提交的修正](https://github.com/magento/magento-cloud-docker/pull/181).<!--MCLOUD-5670-->

- ![修正圖示](../../assets/fix.svg) 已移除 `rsyslog` 從Cloud Docker for Commerce PHP容器中解決在部署期間導致警告通知的相容性問題。 Cloud Docker不使用rsyslog公用程式。<!--MCLOUD-6173-->

## v1.0.0

發行日期：2020年2月5日

- ![新圖示](../../assets/new.svg) **已建立要傳送的個別套件`Cloud Docker for Commerce`** — 將原始程式碼從「 」移至「 」，以傳送Cloud Docker for Commerce `ece-tools` 存放庫至 [新 `magento-cloud-docker` 存放庫](https://github.com/magento/magento-cloud-docker) 以維持程式碼品質並提供獨立的發行。 新套件為ECE-Tools v2002.1.0和更新版本的相依性。

  當您更新ece-tools時，也會更新 `magento/magento-cloud-docker` 封裝至1.0.0版。如果您搭配舊版使用Cloud Docker for Commerce `ece-tools` 版本(2002.0.x)，檢閱 [向後不相容性](backward-incompatible-changes.md) 並根據需要以指令碼、命令和流程更新您的專案。

- ![新圖示](../../assets/new.svg) **為Docker映像新增版本控制** — 您現在必須更新 `magento/magento-cloud-docker` 套件以取得更新的影像。<!--MAGECLOUD-4737-->

- ![新圖示](../../assets/new.svg) **容器更新**—

   - ![新圖示](../../assets/new.svg) **PHP-FPM容器**—

      - ![新圖示](../../assets/new.svg) **新增Node.js支援** — 更新PHP-FPM影像，以支援PHP容器內的節點、npm和grunt-cli功能。<!--MAGECLOUD-3953-->

      - ![新圖示](../../assets/new.svg) **新增的支援 [ionCube](https://www.ioncube.com/)** — 更新預設Docker配置以在本機Docker開發環境中支援ionCube。<!--MAGECLOUD-4354-->

   - ![新圖示](../../assets/new.svg) **Web容器**—

      - ![新圖示](../../assets/new.svg) **自訂NGINX設定** — 新增掛載自訂 `nginx.conf` 檔案到Cloud Docker for Commerce環境。 另請參閱 [Web容器](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#web-container).<!--MAGECLOUD-4204-->

      - ![新圖示](../../assets/new.svg) **自動產生的NGINX憑證**—Docker配置檔案現在包含為Web容器自動生成NGINX證書的配置。<!--MAGECLOUD-4258-->

   - ![新圖示](../../assets/new.svg) **新Selenium容器** — 新增 [Selenium容器](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#selenium-container) 以使用Magento功能測試架構(MFTF)支援Adobe Commerce應用程式測試。<!--MAGECLOUD-4040-->

   - ![新圖示](../../assets/new.svg) **[!DNL RabbitMQ]版本支援** — 已更新 [!DNL RabbitMQ] 要支援的容器設定 [!DNL RabbitMQ] 版本3.8。<!--MAGECLOUD-4674-->

   - ![修正圖示](../../assets/fix.svg) **永久資料庫容器** — 此 `magento-db: /var/lib/mysql` 當您停止並移除Docker配置並在重新啟動Docker配置時恢復後，資料庫磁碟區現在會持續存在。 現在，您必須手動刪除資料庫磁碟區。 另請參閱 [資料庫容器].<!--MAGECLOUD-3978-->

   - ![新圖示](../../assets/new.svg) **TLS容器**—

      - ![新圖示](../../assets/new.svg) **更新容器基礎影像以使用正式影像** — 此 [雲端TLS容器](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) 影像現在是以官方的 `debian:jessie` Docker影像。—<!--MAGECLOUD-4163-->

      - ![新圖示](../../assets/new.svg) **新增對 [英鎊TLS終止Proxy]** — 此 [磅組態檔](https://github.com/magento/magento-cloud-docker/blob/1.0/images/tls/) 新增以下ENV變數以自訂TLS容器的Docker設定：

         - **`TimeOut`** — 設定第一個位元組時間(TTFB)逾時值。 預設值為300秒。

         - **`RewriteLocation`** — 決定Pound Proxy是否預設將位置重寫至要求URL。 預設為 `0` 以防止重寫中斷重新導向至外部網站，例如外部SSO網站。 [Sorin Sugar提交的修正](https://github.com/magento/magento-cloud-docker/pull/37)<!--MAGECLOUD-4061-->

      - ![新圖示](../../assets/new.svg) 將TLS容器設定中的逾時值從15秒增加到300秒。 [Zilker Technology的Mathew Beane提交的修正](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

   - ![新圖示](../../assets/new.svg) **清漆容器**—

      - ![新圖示](../../assets/new.svg) **更新容器基礎影像以使用正式影像** — 此 [雲端清漆容器](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) 現在是以官方網站為基礎 `centos` Docker影像。<!--MAGECLOUD-4163-->

      - ![新圖示](../../assets/new.svg) **改善預設逾時設定** — 已新增 `.first_byte_timeout` 和 `.between_bytes_timeout` 配置到「清漆」容器。 這兩個逾時值都預設為 `300s` （5分鐘）。 [Zilker Technology的Mathew Beane提交的修正](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

      - ![修正圖示](../../assets/fix.svg) **在Xdebug工作階段期間略過清漆** — 更新要傳回的清漆容器組態 `pass` 啟用Xdebug時收到的要求時。 在舊版中，如果Docker環境包含Varnish，則無法使用Xdebug。 [Zilker Technology的Mathew Beane提交的修正](https://github.com/magento/magento-cloud-docker/pull/111).<!--MAGECLOUD-4873-->

- ![新圖示](../../assets/new.svg) **Docker設定變更**—

   - ![新圖示](../../assets/new.svg) **管理專案的掛載和磁碟區** — 新增在啟動Docker環境以進行本機開發時管理掛載和卷冊的功能。 另請參閱 [共用專案資料].<!--MAGECLOUD-3248-->

   - ![新圖示](../../assets/new.svg) **支援網路橋接器模式** — 新增網路橋接器模式的支援，以透過本機網路啟用Docker容器之間的連線。<!--MAGECLOUD-4165-->

   - ![新圖示](../../assets/new.svg) **Cron容器預設為停用** — 為了提高效能，當您構建Docker環境時，Cron容器不再預設配置。 您可以使用 `--with-cron` Docker build命令上的選項，用於將Cron容器新增到您的環境。 另請參閱 [管理cron工作](https://devdocs.magento.com/cloud/docker/docker-manage-cron-jobs.html).<!--MAGECLOUD-5181-->

   - ![新圖示](../../assets/new.svg) **停止同步處理大型備份檔案** — 將資料庫傾印和封存檔案（ZIP、SQL、GZ和BZ2）新增至 `dist/docker-sync.yml` 和 `dist/mutagen.sh` 檔案。 同步處理大型檔案(>1 GB)可能會造成一段閒置時間，而且備份檔案通常不需要同步處理，因為您可以重新產生它們。<!--MAGECLOUD-3979-->

- ![新圖示](../../assets/new.svg) **命令變更**—

   - ![修正圖示](../../assets/fix.svg) 已重新命名 `./bin/docker` 檔案到 `./bin/magento-docker` 修復由於以下原因導致某些Docker環境中斷的問題 `./bin/docker` 檔案會覆寫現有的Docker二進位檔案。 這是 [與舊版不相容的變更](backward-incompatible-changes.md) 需要更新您的指令碼和命令。<!-- MAGECLOUD-4038 -->

   - ![新圖示](../../assets/new.svg) **新增服務組態選項，以將資料庫連線埠公開至主機** — 使用 `--expose-db-port= [Fix submitted by Adarsh Manickam from Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/101).<PORT>` 用來在建置時向主機公開資料庫連線埠的選項 `docker-compose.yml` 檔案： `bin/ece-docker build:compose --expose-db-port=<PORT>`<!--MAGECLOUD-4454-->

   - ![新圖示](../../assets/new.svg) **新的部署後命令** — 之前，在中定義的部署後鉤點 `.magento.app.yaml` 在您使用將Adobe Commerce部署到Cloud Docker容器後，檔案會自動運行 `cloud-deploy` 命令。 現在，您必須發出另一個 `cloud-post-deploy` 命令在部署後執行部署後掛接。 請參閱更新的啟動指示 [開發人員](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) 和 [生產](https://devdocs.magento.com/cloud/docker/docker-mode-production.html) 模式。<!--MAGECLOUD-3996-->

   - ![新圖示](../../assets/new.svg) 已新增 `--rm` 選項至 `./bin/magento-docker` 組建和部署容器的命令。 這會在工作完成後移除容器。<!--MAGECLOUD-4205-->

   - ![新圖示](../../assets/new.svg) **更新 `build:compose` 命令**—

      - ![新圖示](../../assets/new.svg) 已新增 `--sync-engine="native"` 的選項 `docker-build` 命令以在開發人員模式下生成Docker撰寫配置檔案時停用檔案同步。 在Linux系統上開發時，使用此選項，這些系統不需要本機Docker開發的檔案同步。 另請參閱 [在Docker環境中同步資料](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html).<!--MCLOUD-3231, MCLOUD-3890-->

   - ![新圖示](../../assets/new.svg) 已將預設檔案同步處理設定從 `docker-sync` 至 `native`. [Zilker Technology的Mathew Beane提交的修正](https://github.com/magento/magento-cloud-docker/pull/124).<!--MAGECLOUD-5066-->

- ![新圖示](../../assets/new.svg) **驗證改善**—

   - ![新圖示](../../assets/new.svg) 對本機Docker開發環境的部署流程新增驗證，以驗證雲端環境設定是否包含解密資料庫所需的加密金鑰。 現在，如果環境設定未指定加密金鑰的值，記錄中會顯示錯誤訊息。<!--MAGECLOUD-4423-->

   - ![新圖示](../../assets/new.svg) 已將容器健康情況檢查新增到Elasticsearch服務，以確保服務在繼續建置和部署處理之前已準備就緒。 如果健康情況檢查傳回錯誤，容器會自動重新啟動。<!--MAGECLOUD-4456-->
