---
title: 驗證金鑰
description: 瞭解如何在雲端基礎結構上將驗證金鑰套用至Adobe Commerce中的開發專案。
feature: Cloud, Security
topic: Security
exl-id: b05cd4c2-0804-49c8-980a-4c7b6932082b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 驗證金鑰

您必須擁有驗證金鑰才能存取Adobe Commerce存放庫，並在雲端基礎結構專案上為Adobe Commerce啟用安裝和更新命令。 指定Composer授權認證有兩個方法。

- **驗證檔案** — 包含您的Adobe Commerce的檔案 [授權認證](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) 位於雲端基礎結構根目錄的Adobe Commerce中。
- **環境變數** — 一個環境變數，可在Adobe Commerce的雲端基礎結構專案中設定驗證金鑰，以防止意外曝光。

>[!BEGINSHADEBOX]

**安全性注意事項**

Adobe建議使用 [環境變數](#composer-auth-environment-variable) 雲端專案用來防止意外洩露您的授權憑證的方法。

使用Cloud Docker for Commerce作為本機開發工具時，驗證檔案方法非常理想，但請注意，不要上傳 `auth.json` 檔案至公用的Git存放庫。 您可以新增 `auth.json` 檔案到 [`.gitignore` 檔案](../project/file-structure.md#ignoring-files).

>[!ENDSHADEBOX]

## 驗證檔案

**若要建立 `auth.json` 檔案**：

1. 如果您沒有 `auth.json` 檔案建立您的專案根目錄中。

   - 使用文字編輯器建立 `auth.json` 檔案的根目錄。
   - 複製 [範例 `auth.json`](https://github.com/magento/magento2/blob/2.3/auth.json.sample) 至新的 `auth.json` 檔案。

1. 取代 `<public-key>` 和 `<private-key>` 連同您的Adobe Commerce驗證認證。

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. 儲存變更並退出文字編輯器。

## Composer驗證環境變數

以下方法是防止在公開Git型存放庫中意外暴露敏感憑證的最佳方法。

**使用環境變數新增驗證金鑰的方式**：

1. 在 _[!DNL Cloud Console]_，按一下專案導覽右側的設定圖示。

   ![設定專案](../../assets/icon-configure.png){width="36"}

1. 在 _專案設定_ 清單，按一下 **[!UICONTROL Variables]**.

1. 按一下 **[!UICONTROL Create variable]**.

1. 在 **[!UICONTROL Variable name]** 欄位，輸入 `env:COMPOSER_AUTH`.

1. 在 _值_ 欄位，新增以下內容並取代 `<public-key>` 和 `<private-key>` 連同您的Adobe Commerce驗證認證：

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. 選取 **[!UICONTROL Available during buildtime]** 並取消選取 **[!UICONTROL Available during runtime]**.

1. 按一下 **[!UICONTROL Create variable]**.

1. 移除 `auth.json` 來自每個環境的檔案。
