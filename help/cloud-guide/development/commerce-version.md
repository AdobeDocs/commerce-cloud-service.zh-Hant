---
title: 升級Commerce版本
description: 瞭解如何在雲端基礎結構專案中升級Adobe Commerce版本。
feature: Cloud, Upgrade
exl-id: 87821007-4979-4a20-940b-aa3c82c192d8
source-git-commit: 745a9f08353bd5dfbb871ca88947157c145c7c70
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# 升級Commerce版本

您可以將Adobe Commerce程式碼基底升級至較新版本。 升級專案前，請先檢閱 [系統需求](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) 在 _安裝_ 最新軟體版本需求指南。

根據您的專案組態，您的升級任務可能包括以下內容：

- 更新服務(例如MariaDB (MySQL)、OpenSearch、RabbitMQ和Redis)以與新Adobe Commerce版本相容。
- 轉換較舊的組態管理檔案。
- 更新 `.magento.app.yaml` 包含鉤點和環境變數新設定的檔案。
- 將協力廠商擴充功能升級至最新支援的版本。
- 更新 `.gitignore` 檔案。

{{upgrade-tip}}

{{pro-update-service}}

## 從舊版升級

如果您正從低於2.1的Commerce版本開始升級，Adobe Commerce程式碼庫中的某些限制可能會影響您進行 _更新_ 至特定的ECE-Tools發行版本或 _升級_ 至下一個支援的Commerce版本。 請使用下表來決定最佳路徑：

| 目前版本 | 升級路徑 |
| ----------------- | ------------ |
| 2.1.3和較舊版本 | 在繼續之前，請將Adobe Commerce升級至2.1.4版或更新版本。 然後執行 [一次性升級以安裝ECE-Tools](../dev-tools/install-package.md). |
| 2.1.4 - 2.1.14 | [更新ECE-Tools](../dev-tools/update-package.md) 封裝。<br>請參閱版本注意事項，以瞭解 [2002.0.9](../release-notes/cloud-release-archive.md#v200209) 以及2002.0.x更新版本。 |
| 2.1.15 - 2.1.16 | [更新ECE-Tools](../dev-tools/update-package.md) 封裝。<br>請參閱版本注意事項，以瞭解[2002.0.9](../release-notes/cloud-release-archive.md#v200209) 及更新版本。 |
| 2.2.x和更新版本 | [更新ECE-Tools](../dev-tools/update-package.md) 封裝。<br>請參閱版本注意事項，以瞭解[2002.0.8](../release-notes/cloud-release-archive.md#v200208) 及更新版本。 |

{style="table-layout:auto"}

{{ece-tools-package}}

## 設定管理

舊版Adobe Commerce （例如2.1.4或更新版本至2.2.x或更新版本）使用 `config.local.php` 檔案進行組態管理。 Adobe Commerce 2.2.0版和更新版本使用 `config.php` 檔案，其運作方式與 `config.local.php` 但檔案的組態設定不同，其中包含已啟用模組的清單和其他組態選項。

從舊版升級時，您必須移轉 `config.local.php` 使用較新版本的檔案 `config.php` 檔案。 使用下列步驟來備份設定檔並建立設定檔。

**若要建立暫存 `config.php` 檔案**：

1. 建立以下專案的副本： `config.local.php` 檔案並命名它 `config.php`.

1. 將此檔案新增至 `app/etc` 資料夾。

1. 新增檔案並將其提交到您的分支。

1. 將檔案推送至整合分支。

1. 繼續進行升級程式。

>[!WARNING]
>
>升級之後，您可以移除 `config.php` 並產生新的完整檔案。 您只能刪除這個檔案來取代它一次。 產生新之後，完成 `config.php` 檔案，您無法刪除檔案以產生新檔案。 另請參閱 [設定管理和管道部署](../store/store-settings.md).

### 驗證Zend Framework撰寫器相依性

當升級至 **2.2.x的2.3.x或更新版本**，確認Zend架構相依性已新增至 `autoload` 的屬性 `composer.json` 檔案以支援Laminas。 此外掛程式支援Zend Framework的新需求，此架構已移轉至Laminas專案。 另請參閱 [Zend架構移轉至Laminas專案](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) 於 _MagentoDevBlog_.

**若要檢查 `auto-load:psr-4` 設定**：

1. 在本機工作站上，變更至專案目錄。

1. 請檢視您的整合分支。

1. 開啟 `composer.json` 文字編輯器中的檔案。

1. 檢查 `autoload:psr-4` 區段來取得控制器相依性的Zend外掛程式管理員實作。

   ```json
    "autoload": {
       "psr-4": {
          "Magento\\Framework\\": "lib/internal/Magento/Framework/",
          "Magento\\Setup\\": "setup/src/Magento/Setup/",
          "Magento\\": "app/code/Magento/",
          "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
       },
   }
   ```

1. 如果缺少Zend相依性，請更新 `composer.json` 檔案：

   - 將下列行新增至 `autoload:psr-4` 區段。

     ```json
     "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
     ```

   - 更新專案相依性。

     ```bash
     composer update
     ```

   - 新增、提交和推送程式碼變更。

     ```bash
     git add -A
     ```

     ```bash
     git commit -m "Add Zend plugin manager implementation for controllers dependency for Laminas support"
     ```

     ```bash
     git push origin <branch-name>
     ```

   - 先將變更合併到測試環境，然後再合併到生產環境。

## 組態檔

在升級應用程式之前，您必須更新專案設定檔，以考慮雲端基礎結構或應用程式上Adobe Commerce預設設定值的變更。 最新的預設值可在以下連結中找到： [magento-cloud GitHub存放庫](https://github.com/magento/magento-cloud).

### .magento.app.yaml

一律檢閱 [.magento.app.yaml](../application/configure-app-yaml.md) 已安裝版本的檔案，因為它可控制應用程式建置和部署到雲端基礎結構的方式。 以下範例適用於版本2.4.6，並使用撰寫器2.2.21。此 `build: flavor:` 屬性不用於Composer 2.x；請參閱 [安裝和使用Composer 2](../application/properties.md#installing-and-using-composer-2).

**若要更新 `.magento.app.yaml` 檔案**：

1. 在本機工作站上，變更至專案目錄。

1. 開啟並編輯 `magento.app.yaml` 檔案。

1. 更新PHP選項。

   ```yaml
   type: php:8.2
   
   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.2.21'
   ```

1. 修改 `hooks` 屬性 `build` 和 `deploy` 命令。

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           composer install
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. 將下列環境變數新增至檔案結尾。

   適用於Adobe Commerce 2.2.x至2.3.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

   適用於Adobe Commerce 2.4.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

1. 儲存檔案。 請勿認可或推送變更至遠端環境。

1. 繼續進行升級程式。

### composer.json

升級之前，請務必檢查 `composer.json` 檔案與Adobe Commerce版本相容。

**若要更新 `composer.json` Adobe Commerce 2.4.4版和更新版本的檔案**：

1. 新增下列專案 `allow-plugins` 至 `config` 區段：

   ```json
   "config": {
      "allow-plugins": {
         "dealerdirect/phpcodesniffer-composer-installer": true,
         "laminas/laminas-dependency-plugin": true,
         "magento/*": true
      }
   },
   ```

1. 將下列外掛程式新增至 `require` 區段：

   ```json
   "require": {
       "magento/composer-root-update-plugin": "^2.0.3"
   },
   ```

1. 將下列元件新增至 `extra:component_paths` 區段：

   ```json
   "extra": {
      "component_paths": {
         "tinymce/tinymce": "lib/web/tiny_mce_5"
      },
   },
   ```

1. 儲存檔案。 尚未認可或推送變更至您的分支。

1. 繼續進行升級程式。

## 專案備份

建議您先建立專案的備份，再進行升級。 使用下列步驟來備份您的整合、測試和生產環境。

**備份整合環境資料庫和程式碼**：

1. 建立遠端資料庫的本機備份。

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >此 `magento-cloud db:dump` 命令執行 [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) 命令與 `--single-transaction` 標幟，可讓您備份資料庫而不鎖定表格。

1. 備份程式碼和媒體。

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   或者，您可以省略 `[--media]` 如果您有大量靜態檔案已經在原始檔控制中。

**在部署之前備份您的測試或生產環境資料庫**：

1. 使用SSH登入遠端環境。

1. 建立 [資料庫傾印](../storage/database-dump.md). 若要選擇資料庫傾印的目標目錄，請使用 `--dump-directory` 選項。

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   傾印作業會建立 `dump-<timestamp>.sql.gz` 封存檔案到您的遠端專案目錄中。 另請參閱 [備份資料庫](../storage/database-dump.md).

## 應用程式升級

檢閱 [服務版本](../services/services-yaml.md#service-versions) 升級應用程式前，最新軟體版本需求的資訊。

**升級應用程式版本的方式**：

1. 在本機工作站上，變更至專案目錄。

1. 使用設定升級版本 [版本限制語法](overview.md#cloud-metapackage).

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >您必須使用版本限制語法才能成功更新 `ece-tools` 封裝。 您可以在下列位置找到版本限制： `composer.json` 的版本檔案 [應用程式範本](https://github.com/magento/magento-cloud/blob/master/composer.json) 您正在使用進行升級。

1. 更新專案。

   ```bash
   composer update
   ```

1. 新增、提交和推送程式碼變更。

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Upgrade"
   ```

   ```bash
   git push origin <branch-name>
   ```

   `git add -A` 由於Composer封送基礎套件的方式，需要將所有變更的檔案新增到原始檔控制中。 兩者 `composer install` 和 `composer update` 從基礎封裝封送檔案(`magento/magento2-base` 和 `magento/magento2-ee-base`)至封裝根目錄。

   Composer封送處理的檔案屬於新版Adobe Commerce，以便覆寫這些相同檔案的過時版本。 目前，Adobe Commerce中已停用封送處理，因此您必須將封送處理檔案新增至原始檔控制。

1. 等待部署完成。

1. 使用SSH登入並檢查版本，在整合、測試或生產環境中驗證升級。

   ```bash
   php bin/magento --version
   ```

### 建立config.php檔案

如中所述 [設定管理](#configuration-management)，升級後，您必須建立更新的 `config.php` 檔案。 透過您整合環境中的「管理員」完成任何其他設定變更。

**建立系統特定的組態檔**：

1. 從終端機，使用SSH命令來產生 `/app/etc/config.php` 檔案來建立環境。

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   例如，對於Pro，要執行 `scd-dump` 於 `integration` 分支：

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. 轉移 `config.php` 檔案至您的本機工作站，使用 `rsync` 或 `scp`. 您只能將此檔案新增至本機分支。

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. 新增、提交和推送程式碼變更。

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   這會產生一個更新的 `/app/etc/config.php` 包含模組清單和組態設定的檔案。

>[!WARNING]
>
>若為升級，您會刪除 `config.php` 檔案。 將此檔案新增到您的程式碼後，您應該 **非** 刪除它。 如果您必須移除或編輯設定，請手動編輯檔案。

### 升級擴充功能

檢閱Marketplace或其他公司網站中的協力廠商擴充功能和模組頁面，並確認對雲端基礎結構上的Adobe Commerce和Adobe Commerce的支援。 如果您必須升級任何協力廠商擴充功能和模組，Adobe建議您在停用擴充功能的情況下，使用新的整合分支。

**驗證及升級擴充功能的方式**：

1. 在您的本機工作站上建立分支。

1. 視需要停用您的擴充功能。

1. 可用時，下載擴充功能升級。

1. 安裝第三方檔案記錄的升級。

1. 啟用並測試擴充功能。

1. 新增、提交程式碼變更，並將其推播至遠端。

1. 推送至並在您的整合環境中測試。

1. 推送至測試環境，以便在預先生產環境中測試。

Adobe強烈建議升級您的生產環境 _早於_ 將升級的擴充功能納入您的網站啟動程式。

>[!NOTE]
>
>當您升級應用程式版本時，升級程式會更新至最新版本的 [Fastly CDN模組](../cdn/fastly.md#fastly-cdn-module-for-magento-2) 自動。

## 疑難排解升級

如果升級失敗，您會在瀏覽器中收到一則錯誤訊息，指出您無法存取店面或管理面板：

```terminal
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**解決錯誤的方式**：

1. 在本機工作站上，變更至專案目錄。

1. 使用SSH登入遠端環境。

   ```bash
   magento-cloud ssh
   ```

1. 開啟 `./app/var/report/<error number>` 檔案。

1. [檢查記錄](../test/log-locations.md) 和決定問題的來源。

1. 新增、提交和推送程式碼變更。

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
