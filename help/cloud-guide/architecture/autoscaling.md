---
title: 自動縮放
description: 瞭解雲端基礎結構上的Adobe Commerce如何擴展以滿足資源需求。
feature: Cloud, Auto Scaling
topic: Architecture
exl-id: 2ba49c55-d821-4934-965f-f35bd18ac95f
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# 自動縮放

自動縮放功能會自動新增或移除雲端基礎建設的資源，以維持最佳效能及合理成本。 目前，此功能僅適用於設定了 [擴充架構](scaled-architecture.md).

## Web伺服器節點

此 [網頁層](scaled-architecture.md#web-tier) 調整規模，以因應流程要求的增加以及更高的流量需求。 目前，自動縮放功能只能透過新增或移除Web伺服器節點來水平縮放。

當CPU使用量和流量達到預先定義的臨界值時，就會發生自動縮放事件：

- **節點已新增** — 所有使用中Web節點的CPU/核心在1分鐘內皆為75%的容量，而流量則連續5分鐘增加20%。
- **節點已移除** — 所有使用中Web節點的CPU/核心均以60%的速率載入20分鐘。 節點會依照其新增順序移除。

最小值和最大臨界值是根據每個商家的合約資源限制來決定和設定的；這降低了無限擴展的風險。

## 使用New Relic監控臨界值

您可以使用 [New Relic服務](../monitor/new-relic-service.md) 監督特定臨界值，例如主機計數和CPU使用率。 下列New Relic查詢使用變數標籤法 `cluster-id` 僅供範例使用。

>[!TIP]
>
>如需建立查詢的參考資料，請參閱 [NRQL語法、子句和函式](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/) 在 _New Relic_ 檔案。
>使用您的查詢來建置 [New Relic控制面板](https://docs.newrelic.com/docs/query-your-data/explore-query-data/dashboards/introduction-dashboards/).

### 主機計數

以下範例New Relic查詢顯示環境內的主機計數：

```sql
SELECT uniqueCount(SystemSample.entityId) AS 'Infrastructure hosts', uniqueCount(Transaction.host) AS 'APM hosts seen' FROM SystemSample, Transaction where (Transaction.appName = 'cluster-id_stg' AND Transaction.transactionType = 'Web') OR SystemSample.apmApplicationNames LIKE '%|cluster-id_stg|%' TIMESERIES SINCE 3 HOURS AGO
```

在下列熒幕擷圖中， **已看見APM主機** 是指在選取期間記錄交易的主機數目。

![New Relic主機計數](../../assets/new-relic/host-count.png)

### CPU使用量

以下範例New Relic查詢顯示網頁節點的CPU使用量：

```sql
SELECT average(cpuPercent) FROM SystemSample FACET hostname, apmApplicationNames WHERE instanceType LIKE 'c%' TIMESERIES SINCE 3 HOURS AGO
```

![New Relic Web節點CPU使用量](../../assets/new-relic/web-node-cpu-usage.png)

## 啟用自動縮放

若要在雲端基礎結構專案上啟用或停用Adobe Commerce的自動縮放， [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). 在票證中選擇以下原因：

- **聯絡原因**：基礎結構變更請求
- **Adobe Commerce基礎結構聯絡原因**：其他基礎架構變更請求

>[!IMPORTANT]
>
>自動縮放功能會擷取未預期的事件。 即使您已啟用自動縮放，Adobe仍建議您繼續 [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 如果您期待即將到來的活動。

### 載入測試

Adobe可在您的雲端專案上啟用自動縮放 _分段_ 先叢集。 在您的環境中執行並完成負載測試後，Adobe就會在您的生產叢集上啟用自動縮放。 如需負載測試的指引，請參閱 [效能測試](../launch/checklist.md#performance-testing).

### IP允許清單

啟用自動縮放後，輸出Web節點流量會源自服務節點的IP位址。 如果您使用允許清單搭配未在雲端基礎結構專案上與Adobe Commerce繫結的第三方服務，請驗證第三方服務允許清單中的IP位址。

例如：

- 如果允許清單包含服務節點（1、2和3）的IP位址，則不需要採取任何動作。
- 如果允許清單包含服務節點（1、2和3）和Web節點（4、5和6）的IP位址（在此例中是全部六個節點），則不需要採取任何動作。
- 如果允許清單包含IP位址 _僅限_ 若是您的Web節點（4、5和6），則必須更新允許清單以包含服務節點的IP位址。
