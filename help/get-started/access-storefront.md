---
title: 存取您的Commerce管理面板
description: 瞭解如何存取您的Commerce管理面板。
recommendations: noDisplay, catalog
exl-id: 9a8a0a49-b108-48bd-b413-ec9431370c06
source-git-commit: 3ca09243dc0a714c1d86cccf9f0620a8a39fd1e1
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 存取您的Commerce管理面板

擁有Commerce管理員面板管理存取權的使用者可以新增使用者、設定商店服務、完成商店設定和自訂工作等。

若為新專案，收到歡迎電子郵件後的第一個步驟是變更授權擁有者帳戶的密碼，以保護管理員對專案的存取權。 此帳戶的預設使用者名稱是授權擁有者的電子郵件地址。

您可以使用下列其中一種方法來提交密碼變更請求：

- 找到傳送至授權擁有者電子郵件地址的歡迎電子郵件，然後按照連結變更您的密碼。

- 複製商店URL，從 [[!DNL Cloud Console]](../cloud-guide/project/overview.md) 到瀏覽器中。 然後，附加 `/admin` 到URL的結尾以開啟登入頁面。 按一下 **忘記密碼？** 將密碼變更請求傳送到授權擁有者電子郵件地址的連結。

提交密碼變更請求後，請檢視電子郵件中的密碼重設通知。 如果您沒有收到電子郵件，請檢查您的垃圾郵件資料夾。

>[!TIP]
>
>如果密碼重設失敗或您無法登入「管理員」面板，則具有管理員存取許可權的使用者可以使用SSH連線至專案，並使用 `admin:user:create` CLI命令。 另請參閱 [建立、編輯或解除鎖定管理員帳戶](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) 在 _安裝指南_.

## 監視網站健康狀況

此 [全網站分析工具](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/intro) 是主動式自助服務工具和中央存放庫，其中包含詳細的系統分析和建議，以確保Adobe Commerce安裝的安全性和可操作性。 它提供全天候的即時效能監控、報告和建議，以找出潛在問題，並更清楚地瞭解網站健康狀況、安全性和應用程式設定。 這有助於縮短解決時間，並改善網站穩定性與效能。 您可以直接從存取「全網站分析工具」 [管理面板](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/access#option-2-logging-in-to-your-site-wide-analysis-tool-dashboard-from-your-stores-admin-panel) 或從 [專用網域](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/access#option-1-logging-in-to-your-site-wide-analysis-tool-dashboard-directly-from-the-site-wide-analysis-tool-domain-for-adobe-commerce-on-cloud-infrastructure-only) (僅限雲端基礎結構專案上的Adobe Commerce)。
