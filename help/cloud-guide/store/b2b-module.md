---
title: 啟用B2B模組
description: 瞭解如何在雲端基礎結構上為Adobe Commerce啟用企業對企業的模組。
feature: Cloud, B2B
exl-id: 01d02ea0-1e7d-4608-adbf-1dad7f5e2182
source-git-commit: bb7a866b1896a8a43d01ad3f83dc655bcf383374
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 啟用B2B模組

如果您的客戶為公司，您可以安裝Adobe Commerce適用的B2B模組，將Adobe Commerce擴充至雲端基礎結構Pro專案，以符合企業對企業的模式。 雖然本主題提供在雲端基礎結構上安裝和設定適用於Adobe Commerce的B2B模組的特定資訊，但您可在以下指南中找到其他B2B資訊：

- [Adobe Commerce B2B開發人員指南](https://developer.adobe.com/commerce/webapi/rest/b2b/)
- [Adobe Commerce B2B使用手冊](https://experienceleague.adobe.com/docs/commerce-admin/b2b/guide-overview.html)

>[!TIP]
>
>由於B2B是雲端基礎結構上Adobe Commerce的模組，Adobe建議您先將Adobe Commerce應用程式部署至整合或預備環境，再開始進行。

## 安裝B2B模組

將B2B模組新增至專案時，Adobe建議在開發分支中工作。 如果您沒有分支，請參閱 [建立開發分支](../development/cli-branches.md#create-a-branch-for-development). 安裝B2B模組時， `Magento_B2b` 模組名稱會自動插入至 `app/etc/config.php` 檔案。 不需要直接編輯檔案。

**安裝B2B模組的方式**：

1. 在本機工作站上，變更至專案目錄。

1. 建立或簽出開發分支。

1. 將B2B模組新增至 `require` 的區段 `composer.json` 檔案。

   ```bash
   composer require magento/extension-b2b --no-update
   ```

1. 更新專案相依性。

   ```bash
   composer update
   ```

1. 新增、提交和推送程式碼變更。

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Install the B2B module."
   ```

   ```bash
   git push origin <branch-name>
   ```

1. 建置和部署完成後，請使用SSH登入遠端環境，並確認已安裝B2B模組。

   ```bash
   bin/magento module:status Magento_B2b
   ```

   擴充功能名稱會使用以下格式： `<VendorName>_<ComponentName>`.

   範例回應：

   ```terminal
   Magento_B2b : Module is enabled
   ```

   如果您遇到部署錯誤，請參閱 [從元件失敗復原](../deploy/recover-failed-deployment.md).

## 啟用B2B模組

當您使用Composer安裝B2B模組時，部署程式會自動啟用模組。 如果您已安裝B2B模組，則可使用CLI啟用或停用該模組

啟用B2B模組：

```bash
bin/magento module:enable Magento_B2b
```

範例回應：

```terminal
The following modules have been enabled:
- Magento_B2b

Cache cleared successfully.
Generated classes cleared successfully. Please run the 'setup:di:compile' command to generate classes.
Info: Some modules might require static view files to be cleared. To do this, run 'module:enable' with the --clear-static-content option to clear them.
```

另請參閱 [管理擴充功能](extensions.md).

## 設定B2B模組

安裝適用於Adobe Commerce模組的B2B後，您必須 [啟動訊息取用者](https://experienceleague.adobe.com/docs/commerce-admin/b2b/install.html#start-message-consumers) 以便您可以啟用 _共用目錄_ 模組，而您必須 [啟用B2B功能](https://experienceleague.adobe.com/docs/commerce-admin/b2b/enable-basic-features.html).
