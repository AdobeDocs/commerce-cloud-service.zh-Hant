---
title: New Relic監視
description: 瞭解如何存取您的New Relic儀表板，並分析雲端基礎結構專案中Adobe Commerce的資料。
feature: Cloud, Observability
topic: Performance
exl-id: 8d1e2ad6-14d0-4754-9703-960d93e135a9
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# New Relic監視

New Relic可連線並監控您的基礎建設，以及 [!DNL Commerce] 使用PHP代理程式的應用程式。 雲端環境連線至New Relic後，您可以登入您的New Relic帳戶，檢閱代理程式收集的資料。

在 _APM與服務_ 頁面，選取 **摘要** 以檢視應用程式的交易式資訊。 此檢視可協助您識別潛在故障，並檢查應用程式和服務的整體健康狀況。

![雲端專案New Relic概觀頁面](../../assets/new-relic/dashboard.png)

從這個檢視中，您可以追蹤發生緩慢回應或瓶頸的交易、應用程式輸送量、Web錯誤等等。

檢閱追蹤的資料：

- **最耗時** — 透過平行追蹤請求來判斷時間消耗。 例如，您的產品和類別檢視可能會有花費最多交易時間。 如果客戶帳戶頁面突然在時間消耗上排名很高，您的應用程式可能會受到呼叫或查詢拖曳效能的影響。

- **最高輸送量** — 根據傳輸位元組的大小和頻率，識別點選次數最多的頁面。

所有收集的資料都會詳細說明用於傳輸資料、查詢或 _Redis_ 資料。 如果查詢造成問題，New Relic會提供資訊以追蹤和回應這些問題。

>[!TIP]
>
>如需使用此資料來疑難排解應用程式效能問題的詳細資訊，請參閱 [使用New Relic疑難排解效能](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-performance-using-new-relic-on-magento-commerce.html) 在 _Adobe Commerce說明中心_.

## 使用受管理警示監控效能

Adobe提供 _Adobe Commerce的管理式警報_ 追蹤效能測量結果的警示原則。 此原則包含警示集合，當基礎結構或應用程式問題影響網站效能時，這些警示會設定臨界值並觸發警告和嚴重通知。 此原則會追蹤生產環境中的以下量度：

| 量度 | 資料彙集 | 可用性 |
|:-------------------|:----------------|:----------------|
| [!DNL Apdex] 分數 | APM | Pro與Starter |
| CPU使用量 | NRI | Pro |
| 磁碟空間 | NRI | Pro |
| 錯誤率 | APM | Pro與Starter |
| 記憶體使用量 | NRI | Pro |
| MariaDB查詢載入 | NRI | Pro |
| Redis記憶體 | NRI | Pro |

當網站基礎結構或應用程式條件觸發警報臨界值時，New Relic會傳送警報通知，以便您能主動解決問題。 另請參閱 [Adobe Commerce的管理式警報](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) 在 _Adobe Commerce說明中心_ 以取得警示臨界值以及解決觸發警示之問題的疑難排解步驟的詳細資訊。

>[!TIP]
>
>對於Pro測試和整合環境以及入門環境，請使用 [健康狀態通知](../integrations/health-notifications.md) 以監視磁碟空間。

>[!PREREQUISITES]
>
>- **New Relic認證** — 登入雲端專案New Relic帳戶的憑證
>- **作用中的New Relic整合** — 確認您的雲端環境已連線至New Relic
>- **工作流程通知** — 至少設定一個 [工作流程](#set-up-a-workflow-for-notifications) 以接收警示通知

**檢閱Adobe Commerce的「受管理的警示」原則**：

1. 登入您的 [New Relic帳戶](https://login.newrelic.com/login).

1. 找到 _Adobe Commerce的管理式警報_ 原則：

   - 在Explorer導覽功能表中按一下 **[!UICONTROL Alerts & AI]**.

   - 在 _偵測_，按一下 **[!UICONTROL Alert Conditions & Policies]**.

   - 確認您的帳戶已選取在 _警示條件和原則_ 檢視。

   - 在 _原則_ 清單，選取 **Adobe Commerce的管理式警報** 原則。

     ![已產生警示原則](../../assets/new-relic/managed-alerts-policy.png)

     >[!NOTE]
     >
     >如果 _Adobe Commerce的管理式警報_ 原則無法使用，請參閱 [Adobe Commerce的管理式警報](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) 在 _Adobe Commerce說明中心_.

1. 按一下 **[!UICONTROL Alert conditions]** 標籤以複查原則中定義的警示條件。

## 建立警示原則

請勿修改「Adobe Commerce的管理警示」原則中包含的任何警示。 Adobe會隨著時間更新並改善此原則中的警示條件，覆寫您新增至原則的任何自訂。

您可以建立警示原則，而不必修改現有的警示。 然後，將警示條件複製到新原則。 另請參閱 [更新原則或條件](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-policies/update-or-disable-policies-conditions/) 在 _New Relic_ 檔案。

>[!TIP]
>
>另請參閱 [警報簡介](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/learn-alerts/alerts-concepts-workflow/) 在 _New Relic_ 說明檔案，以取得警示、警示原則和工作流程的詳細資訊。

## 設定通知的工作流程

您現在可以設定 _工作流程_（先前稱為通知頻道），可接收根據篩選資料（例如警示原則）的有關您網站績效的通知。 當應用程式或基礎結構的條件觸發警示時，有關效能問題的通知會傳送至與警示原則相關的所有工作流程。 您也會在問題確認和關閉時收到通知。

New Relic提供設定不同型別的工作流程通知的範本，包括電子郵件、Slack、PagerDuty、webhook等。

**若要設定工作流程**：

1. 登入您的 [New Relic帳戶](https://login.newrelic.com/login).

1. 建立工作流程。

   - 在Explorer導覽功能表中按一下 **[!UICONTROL Alerts & AI]**.

   - 在左側導覽列中的 _豐富並通知_，按一下 **[!UICONTROL Workflows]**.

   - 按一下 **[!UICONTROL Add a workflow]** 在右側。

     ![New Relic新增工作流程](../../assets/new-relic/add-a-workflow.png)

   - 在 _設定您的工作流程_ 頁面，輸入工作流程的名稱。

   - 在 _篩選資料_ 區段，選取 **[!UICONTROL Managed Alerts for Adobe Commerce]** 從 **[!UICONTROL Policy]** 下拉式清單。

   - 在 _通知_ 區段，選取通道並依照指示進行。

   - 按一下 **[!UICONTROL Test workflow]** 以驗證您的設定。

1. 按一下 **[!UICONTROL Activate workflow]**.

請參閱New Relic檔案以瞭解 [工作流程](https://docs.newrelic.com/docs/alerts-applied-intelligence/applied-intelligence/incident-workflows/incident-workflows/).

>[!WARNING]
>
>「Adobe Commerce的管理警示」原則中的警示已將預設工作流程設定為通知雲端基礎結構客戶上支援Adobe Commerce的Adobe團隊。 請勿修改這些預設頻道的設定，也不要移除指派給這些頻道的警示原則。
