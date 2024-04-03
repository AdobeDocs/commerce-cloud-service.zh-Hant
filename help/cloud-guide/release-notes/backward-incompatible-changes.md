---
title: 與舊版不相容的變更
description: 瞭解在升級現有Cloud專案時的回溯相容性。
feature: Cloud, Release Notes
recommendations: noDisplay, catalog
exl-id: 9847c565-6d59-429a-9593-c2eba5cf2da4
source-git-commit: f9edcc85c14354a2eddacbc5219557e107a367cb
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---

# 與舊版不相容的變更

升級到最新版本時，與回溯不相容的變更可能會要求您調整現有雲端專案的雲端設定和流程。 `ece-tools` 封裝或其他Commerce雲端工具套裝。

## 變更為 `ece-tools` 封裝

先前包含在 `ece-tools` 套件現在以個別套件提供。 這些套件是Composer相依性 `ece-tools`，會在您安裝或更新ece-tools時自動安裝和更新。

新架構不應影響您的安裝或更新流程。 不過，在雲端基礎結構專案上使用Adobe Commerce時，您可能需要變更一些命令語法和程式。 如需詳細資訊，請檢閱下列與舊版不相容的變更資訊，以及 [Cloud Tools Suite發行說明](cloud-tools-suite.md).

### 服務版本需求變更

我們將使用的雲端專案的最低PHP版本要求從7.0.x變更為7.1.x `ece-tools` v2002.1.0及更高版本。 如果您的環境組態指定了PHP 7.0，請更新 [php設定](../application/php-settings.md) 在 `.magento.app.yaml` 檔案。

>[!WARNING]
>
>由於PHP版本要求變更， `ece-tools` 2002.1.0僅支援在執行Adobe Commerce 2.1.15或更新版本的雲端基礎結構專案上使用Adobe Commerce。 如果您的專案使用舊版，您必須 [升級](../development/commerce-version.md) 在您更新到 `ece-tools` 2002.1.0。

### 環境設定變更

下表提供有關中已移除或已棄用的環境變數和其他環境設定檔案的資訊。 `ece-tools` v2002.1.0。

| 專案 | 替代方案 |
| -------- | ----------- |
| `SCD_EXCLUDE_THEMES` 變數 | [`SCD_MATRIX`](../environment/variables-build.md#scd_matrix) |
| `STATIC_CONTENT_THREADS` 變數 | [`SCD_THREADS`](../environment/variables-build.md#scd_threads) |
| `DO_DEPLOY_STATIC_CONTENT` 變數 | [`SKIP_SCD`](../environment/variables-build.md#skip_scd) |
| `STATIC_CONTENT_SYMLINK` 變數 | 無。 現在，組建一律會建立指向靜態內容目錄的符號連結 `pub/static`. |
| `build_options.ini` 檔案 | 使用 [`.magento.env.yaml`](../application/configure-app-yaml.md) 檔案來設定環境變數，以管理所有環境中的建置和部署動作。<p>如果您建置的雲端環境包含 `build_options.ini` 檔案，建置會失敗。 |

### CLI命令變更

下表總結了ECE-Tools v2002.1.0中CLI指令的變更，這些變更可能需要您更新指令或指令碼。

| 命令 | 替代方案 |
|-------- | ----------- |
| `m2-ece-build` | `vendor/bin/ece-tools build` |
| `m2-ece-deploy` | `vendor/bin/ece-tools deploy` |
| `m2-ece-scd-dump` | `vendor/bin/ece-tools config:dump` |
| `vendor/bin/ece-tools patch` | `vendor/bin/ece-patches apply` |
| `vendor/bin/ece-tools docker:build` | `vendor/bin/ece-docker build:compose` |
| `vendor/bin/ece-tools docker:config:convert` | `vendor/bin/ece-docker  image:generate:php` |

在舊版ECE-Tools中，您可以使用 `m2-ece-build` 和 `m2-ece-deploy` 用來設定部署鉤點的命令 `.magento.app.yaml` 檔案。 當您更新至v2002.1.0時，請檢查 `hooks` 中的設定 `.magento.app.yaml` 檔案，並視需要加以取代。

## 雲端修補程式變更

- **移除已下載的修補程式**-The `magento/magento-cloud-patches` 套裝軟體將所有可用的修補程式套裝在 [軟體下載](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/commerce.html) 頁面，並在您部署至雲端時自動套用這些頁面。 若要避免升級至ECE-Tools 2002.1.0或更新版本後發生修補程式衝突，請移除您手動下載並新增至專案的Adobe提供的任何修補程式。

- **更新套用修補程式指令** — 我們將套用修補程式的指令從 `vendor/bin/ece-tools` 目錄到 `vendor/bin/ece-patches` 目錄。 如果您使用此指令來手動套用修補程式，請使用新路徑。

  > 手動套用修補程式

  ```bash
  php ./vendor/bin/ece-patches apply
  ```

## Cloud Docker變更

- **PHP的最低版本要求現在是PHP 7.1** — 如果您的Cloud Docker for Commerce主機正在執行較早的版本，請升級到PHP v7.1或更高版本。

- **Commerce雲端Docker命令變更**-

   - **更新用於Docker構建操作的Commerce的Cloud Docker命令** — 我們將Cloud Docker for Commerce命令從 `vendor/bin/ece-tools` 目錄到 `vendor/bin/ece-docker` 目錄。 更新指令碼和命令以使用新路徑。

     升級至 `ece-tools` 2002.1.0，使用以下命令檢視可用的 `ece-docker` 命令。

     ```bash
     php ./vendor/bin/ece-docker list
     ```

   - **更新Cloud Docker-compose命令** — 我們將路徑重新命名為命令檔案的來源 `./bin/docker` 至 `./bin/magento-docker`. 更新指令碼和命令以使用新路徑。

   - **Cron容器不再包含在預設Docker配置中** — 現在，您必須新增 `--with-cron` 的選項 `ece-docker build:compose` 命令以在Docker環境配置中包含Cron容器。 另請參閱 [管理cron工作](https://developer.adobe.com/commerce/cloud-tools/docker/configure/manage-cron-jobs/) 在 _Cloud Docker for Commerce_ 指南。

     先前使用cron作業產生容器的指令碼現在不含cron容器。

   - **使用暫時容器** — 在舊版中，容器是由以下專案建立的： `bin/magento-docker` 並未移除命令作業，因此您可以將其用於其他作業。 現在， `magento-docker` 命令會在命令完成之後移除它們建立的任何容器。

     如果要保留由Docker撰寫操作建立的容器，請使用 `docker-compose run` 命令而非 `bin/magento-docker` 命令。

   - **執行部署後鉤點**-The `cloud-deploy` 命令不再執行部署後鉤點。 使用新的 `cloud-post-deploy` 命令以在部署後執行部署後掛接。 更新您的指令碼以新增命令以執行部署後鉤點。

     ```shell
     bin/magento-docker ece-deploy
     bin/magento-docker ece-post-deploy
     ```

     或者，如果您使用 `docker-compose` 命令直接執行 `docker-compose run deploy cloud-post-deploy` 部署命令之後的命令。

- **正在重新整理資料庫** — 資料庫容器現在儲存在 `magento-db` 永久性Docker磁碟區。 當您重新整理Docker環境時，資料庫不再自動刪除。 如有需要，請使用下列其中一個指令來手動移除它。

   - 移除 `magento-db` 容器：

     ```bash
     docker volume rm magento-db
     ```

   - 關閉Docker容器時移除所有關聯的磁碟區：

     ```bash
     docker-compose down -v
     ```

- **覆寫歸檔和備份檔案的檔案同步設定** — 使用Docker-sync或mutagen時，具有下列副檔名的封存和備份檔案不再同步：SQL、GZ、ZIP和BZ2。 您可以將檔案重新命名為以不同的副檔名結尾，以覆寫這些檔案型別的預設檔案同步化。 例如： `synchronize-me.zip-backup`
