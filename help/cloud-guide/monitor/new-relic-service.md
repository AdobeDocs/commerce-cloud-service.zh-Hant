---
title: New Relic服務
description: 瞭解您的Adobe Commerce在雲端基礎結構專案中可用的New Relic服務。
feature: Cloud, Observability
last-substantial-update: 2023-09-06T00:00:00Z
exl-id: 613f0694-5338-4037-8ee4-ac5eca376159
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# New Relic服務總覽

雲端基礎結構上的所有Adobe Commerce專案都包含對New Relic服務的存取，以協助監控效能和調查 [!DNL Commerce] 應用程式和雲端基礎結構。

以下New Relic功能可用於生產和測試環境：

- [NEW RELIC APM](#new-relic-apm) （Pro與Starter）
- [New Relic基礎結構](#new-relic-infrastructure) （僅限Pro）
- [New Relic記錄管理](#new-relic-logs) （僅限Pro）

>[!INFO]
>
>Adobe Commerce專案沒有其他New Relic功能。

## NEW RELIC APM

[適用於應用程式效能管理(APM)的New Relic](https://docs.newrelic.com/introduction-apm/) 是軟體分析產品，可協助您分析和改善應用程式互動。 New Relic APM適用於雲端基礎結構專案的所有Adobe Commerce，並提供下列功能：

- **著重於特定交易** — 主動標籤並監控網站上的關鍵客戶動作，例如新增至購物車、結帳或處理付款。
- **資料庫查詢監視** — 尋找並監視影響效能的資料庫查詢。
- **應用程式地圖** — 檢視您網站、擴充功能及外部服務中的所有應用程式相依性。
- **[!DNL Apdex]分數** — 評估效能並建立警示，找出問題並在發生時通知您，例如受快速銷售或網路事件影響的網站效能。 另請參閱 [Apdex分數](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction/).
- **Adobe Commerce的管理警報** — 使用此New Relic警示政策，根據業界最佳實務來監控應用程式和基礎建設效能。 另請參閱 [使用Adobe Commerce警示原則的「受管理」警示來監控效能](investigate-performance.md/#monitor-performance-with-managed-alerts).
- **追蹤部署** — 監控部署事件並分析部署對整體效能的影響。 另請參閱 [追蹤部署](track-deployments.md).

您的雲端基礎結構專案上的Adobe Commerce包含New Relic APM服務的軟體以及授權金鑰。 您不需要購買或安裝任何其他軟體。

## New Relic基礎結構

Pro專案包括 [New Relic基礎結構(NRI)](https://docs.newrelic.com/docs/infrastructure/infrastructure-monitoring/get-started/get-started-infrastructure-monitoring/) 此服務會自動連線至應用程式資料與效能分析，以提供動態伺服器監控。 此服務適用於Pro生產和中繼環境。

## New Relic記錄管理

所有雲端基礎結構專案包括 [New Relic記錄管理](log-management.md). 此服務已預先設定為彙總測試和生產環境的所有記錄資料，並在集中式記錄管理儀表板中顯示。
