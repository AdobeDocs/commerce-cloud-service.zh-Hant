---
title: 設定靜態檔案的快取
description: 瞭解如何在中設定快取儲存選項 [!DNL Commerce] 應用程式組態檔。
feature: Cloud, Configuration, Cache, SCD
exl-id: ca6db004-47fc-45ea-b8db-c0ecc3c2136b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# 設定靜態檔案的快取

您媒體和靜態檔案的快取TTL （存留時間）設定在 `.magento.app.yaml` 組態檔使用 `expires` 機碼。

>[!NOTE]
>
>在更新生產環境之前，請務必在中繼環境中測試變更。 [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 以取得更新這些環境上設定的協助。

1. 在「 」中指定TTL時間（以秒為單位） [`web` 屬性](web-property.md) 的 `.magento.app.yaml` 檔案。 您可以新增 `expires` 鍵在 `locations` 或在 `"/media"` 和 `"/static"`.

   若要防止快取過期，請使用 `expires: -1` 機碼值組。 請參閱下列範例：

   ```yaml
   # The configuration of app when it is exposed to the web.
   web:
     locations:
       "/media":
         ...
         expires: -1
   
       "/static":
         ...
         expires: -1
   ```

1. 新增、提交和推送您的程式碼變更。

   ```bash
   git add -A && git commit -m "Set cache TTL for static files" && git push origin <branch-name>
   ```
