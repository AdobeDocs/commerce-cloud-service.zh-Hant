---
title: 管理擴充功能
description: 瞭解如何在雲端基礎結構上的Adobe Commerce中安裝和管理擴充功能。
feature: Cloud, Extensions, Upgrade
exl-id: 9c6e98ca-85da-4342-8402-d576eb382ba2
source-git-commit: bb7a866b1896a8a43d01ad3f83dc655bcf383374
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# 管理擴充功能

您可以透過以下方式新增擴充功能，以擴充您的Adobe Commerce應用程式功能： [Commerce Marketplace](https://marketplace.magento.com). 例如，您可以新增佈景主題來變更店面的外觀和風格，或新增語言套件來本地化您的店面和管理員。

## 副檔名的撰寫器名稱

雖然本節會討論如何從Commerce Marketplace取得擴充功能的撰寫器名稱和版本，但您可以找到 _任何_ 模組。 開啟 `composer.json` 文字編輯器中的檔案並記下 `"name"` 和 `"version"` 值。

**若要從Commerce Marketplace取得模組的撰寫器名稱**：

1. 登入 [Commerce Marketplace](https://marketplace.magento.com) 使用您購買元件的使用者名稱和密碼。

1. 在右上角，按一下您的使用者名稱並選取 **我的設定檔**.

   ![存取您的Marketplace帳戶](../../assets/marketplace/my-profile.png)

1. 在 _我的帳戶_ 頁面，按一下 **我的購買**.

   ![Marketplace購買記錄](../../assets/marketplace/my-purchases.png)

1. 在 _我的購買_ 頁面上，選取您購買的模組，然後按一下 **技術細節**.

1. 按一下 **複製** 複製 [!UICONTROL Component name] 到剪貼簿。

1. 開啟文字編輯器，貼上元件名稱並附加冒號字元(`:`)。

1. 在 **技術細節**，按一下 **複製** 複製 [!UICONTROL Component version] 到剪貼簿。

1. 在文字編輯器中，將版本編號附加至冒號後的元件名稱。 例如：

   ```text
   extension-name/magento2:1.0.1
   ```

## 安裝擴充功能

當您將擴充功能新增至實作時，Adobe建議在開發分支中工作。 安裝擴充功能時，擴充功能名稱為(`<VendorName>_<ComponentName>`)會自動插入 [`app/etc/config.php`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/deployment-files.html) 檔案。 不需要直接編輯檔案。

**若要安裝擴充功能**：

1. 在本機工作站上，變更至專案目錄。

1. 建立或簽出開發分支。 另請參閱 [分支](../development/cli-branches.md).

1. 使用撰寫器名稱和版本，將擴充功能新增至 `require` 的區段 `composer.json` 檔案。

   ```bash
   composer require <extension-name>:<version> --no-update
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
   git commit -m "Install <extension-name>"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!WARNING]
   >
   >安裝擴充功能時，您必須包含 `composer.lock` 檔案。 此 `composer install` 命令會讀取 `composer.lock` 檔案啟用遠端環境中定義的相依性。

1. 建置和部署完成後，請使用SSH登入遠端環境並確認已安裝擴充功能。

   ```bash
   bin/magento module:status <extension-name>
   ```

   擴充功能名稱會使用以下格式： `<VendorName>_<ComponentName>`.

   範例回應：

   ```terminal
   Module is enabled
   ```

   如果您遇到部署錯誤，請參閱 [擴充功能部署失敗](../deploy/recover-failed-deployment.md).

## 管理擴充功能

當您使用Composer新增擴充功能時，部署程式會自動啟用擴充功能。 如果您已安裝擴充功能，可以使用CLI啟用或停用擴充功能。 管理擴充功能時，請使用格式： `<VendorName>_<ComponentName>`

登入遠端環境時，切勿啟用或停用擴充功能。

**啟用或停用擴充功能的方式**：

1. 在本機工作站上，變更至專案目錄。

1. 啟用或停用模組。 此 `module` 指令會更新 `config.php` 具有模組請求狀態的檔案。

   >啟用模組。

   ```bash
   bin/magento module:enable <module-name>
   ```

   >停用模組。

   ```bash
   bin/magento module:disable <module-name>
   ```

1. 如果您已啟用模組，請使用 `ece-tools` 以重新整理組態。

   ```bash
   ./vendor/bin/ece-tools module:refresh
   ```

1. 驗證模組的狀態。

   ```bash
   bin/magento module:status <module-name>
   ```

1. 新增、提交和推送程式碼變更。

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Disable <extension-name>"
   ```

   ```bash
   git push origin <branch-names>
   ```

## 升級擴充功能

繼續進行之前，您需要該擴充功能的撰寫器名稱和版本。 此外，請確認擴充功能與您的專案和Adobe Commerce版本相容。 尤其是， [檢查所需的PHP版本](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) 開始之前。

**更新擴充功能的方式**：

1. 在本機工作站上，變更至專案目錄。

1. 建立或簽出開發分支。 另請參閱 [分支](../development/cli-branches.md).

1. 開啟 `composer.json` 文字編輯器中的檔案。

1. 找到您的擴充功能並更新版本。

1. 儲存變更並退出文字編輯器。

1. 更新專案相依性。

   ```bash
   composer update
   ```

1. 新增、提交和推送您的程式碼變更。

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update <extension-name>"
   ```

   ```bash
   git push origin <branch-names>
   ```

如果發生錯誤，請參閱 [從元件失敗復原](../deploy/recover-failed-deployment.md). 若要進一步瞭解如何搭配Adobe Commerce使用擴充功能，請參閱 [擴充功能](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/extensions.html) 在 _管理指南_.
