---
title: 將請求重新路由到CMS後端
description: 瞭解如何使用Fastly邊緣模組將來自Adobe Commerce商店的傳入請求重新路由到單獨的WordPress網站。
feature: Cloud, Configuration, Routes
exl-id: 5bd9c56f-4412-4643-89b6-590a8ec65ac0
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# 將請求重新路由到CMS後端

使用Fastly Edge模組將來自Adobe Commerce商店的傳入請求重新路由到單獨的WordPress網站 _其他CMS/後端整合_ 搭配邊緣字典。 您可以依照類似的程式，將請求重新路由到其他CMS後端。

使用Fastly Edge模組從管理員建立及上傳自訂VCL程式碼，而非手動撰寫VCL程式碼並使用Fastly API上傳。

>[!NOTE]
>
>我們建議您將自訂VCL設定新增到測試環境，您可以在其中測試它們，然後在生產環境中更新Fastly服務設定。

**必要條件**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**將請求從Adobe Commerce重新路由至WordPress**：

1. 在中繼或生產環境中啟用Fastly邊緣模組。

   - 登入管理員。

   - 瀏覽至 **商店** >設定> **設定** > **進階** > **系統** > **完整頁面快取** > **Fastly設定** > **進階設定**.

   - 設定值 **Fastly Edge模組** 至 **是**.

   - 儲存設定。

1. 識別要重新路由至WordPress後端的URL路徑。

1. 完成下列工作以設定Fastly服務並建立自訂VCL程式碼，將要求重新路由至WordPress後端。

   - 建立邊緣字典，指定要從Adobe Commerce存放區重新路由傳送到後端的路徑。

   - 將WordPress後端新增至Fastly服務設定，並附加URL重寫的要求條件。

   - 設定 _其他CMS/後端整合_ Edge模組，可處理從Adobe Commerce到WordPress後端的URL重寫。

     如需詳細指示，請參閱 [Fastly Edge模組 — 其他CMS/後端整合](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) 在 _Magento2的Fastly CDN模組_ 檔案。

1. 更新Fastly服務設定後，請測試您的Adobe Commerce存放區，以確保WordPress的指定URL請求已正確重新路由。
