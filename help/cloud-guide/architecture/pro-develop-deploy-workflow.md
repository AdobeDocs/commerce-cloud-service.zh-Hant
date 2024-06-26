---
title: Pro專案工作流程
description: 瞭解如何使用Pro開發和部署工作流程。
feature: Cloud, Iaas, Paas
exl-id: 103e90d5-2ef2-4fef-845c-439344666b00
source-git-commit: 08f43a3b0a50cdb2a5e8a45bd2e2448bc6dbca2b
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# Pro專案工作流程

Pro專案包含單一Git存放庫，其中包含全域 `master` 分支和三個主要環境：

1. **生產** 啟動及維護已上線網站的環境
1. **分段** 使用所有服務進行測試的環境
1. **整合** 開發和測試環境

![Pro環境清單](../../assets/pro-environments.png)

這些環境是 `read-only`，接受從您本機工作區推送之分支的部署程式碼變更。 另請參閱 [Pro架構](pro-architecture.md) 以取得Pro環境的完整概觀。 另請參閱 [[!DNL Cloud Console]](../project/overview.md#cloud-console) 以取得專案檢視中Pro環境清單的概觀。

下圖示範Pro開發和部署工作流程，此工作流程使用簡單的Git分支方法。 您 [開發](#development-workflow) 代碼使用根據以下原則的有效分支： `integration` 環境， _推送_ 和 _提取_ 程式碼會變更至您的遠端作用中分支，或從您遠端使用中分支變更。 部署已驗證程式碼的方法有： _合併_ 連線至基礎分支的遠端分支，這會啟用自動化 [建置和部署](#deployment-workflow) 該環境的程式。

![Pro架構開發工作流程的高層級檢視](../../assets/pro-dev-workflow.png)

## 開發工作流程

整合環境提供單一、基礎的 `integration` 在雲端基礎結構程式碼上包含您的Adobe Commerce的分支。 您可以建立一個額外的使用中環境分支。 這允許將最多兩個作用中的分支部署到Platform as a Service (PaaS)容器。 非使用中環境的數量沒有限制。

{{enhanced-integration-envs}}

專案環境支援靈活、持續的整合流程。 從複製開始 `integration` 分支至您的本機專案資料夾。 建立一個或多個分支、開發新功能、設定變更、新增擴充功能和部署更新：

- **擷取** 變更來源 `integration`

- **分支** 從 `integration`

- **開發** 本機工作站上的程式碼，包括 [!DNL Composer] 更新

- **推播** 程式碼變更至遠端並進行驗證

- **合併** 至 `integration` 和測試

有了已開發的程式碼分支和相應的設定檔案，您的程式碼變更可以合併到 `integration` 分支以進行更全面的測試。 此 `integration` 環境也最適合：

- **整合協力廠商服務** — 並非所有服務都可在PaaS環境中使用。

- **正在產生組態管理檔案** — 部分組態設定為 _唯讀_ 在已部署的環境中。

- **設定您的存放區** — 您應使用整合環境完整設定所有商店設定。 您可找到 **商店管理員URL** 於 _整合_ 中的環境檢視 _[!DNL Cloud Console]_.

## 部署工作流程

每次您將程式碼從本機工作站推播到遠端環境，或將合併程式碼推播到環境分支時，組建和部署指令碼都會產生新程式碼，並將設定的服務布建到遠端環境。

建置指令碼動作：

- 目標環境中的網站會在建置期間繼續執行

- 在雲端基礎結構修補程式和Hotfix上檢查並執行Adobe Commerce

- 使用建置和部署記錄編譯程式碼

- 檢查組態管理，靜態內容部署會在此階段發生

- 建立或使用未變更程式碼的概要，以加速處理作業

- 布建所有後端服務與應用程式

部署指令碼動作：

- 將網站放入的目標環境中 _維護_ 模式

- 如果未在建置期間完成，則部署靜態內容

- 在雲端基礎結構上安裝或更新Adobe Commerce

- 設定流量的路由

在建置和部署程式後，您的商店會透過最新程式碼變更和設定重新上線。 另請參閱 [部署流程](../deploy/process.md).

### 合併至整合

將您使用中的開發分支合併至基底中，以結合所有已驗證的程式碼變更 `integration` 分支。 您可以在 `integration` 分支。

### 合併至分段

預備是生產前的環境，可提供儘可能接近生產環境的所有服務和設定。 一律將您的程式碼變更從 `integration` 環境至 `staging` 環境，讓您可使用所有服務執行徹底的測試。 第一次使用中繼環境時，您必須設定服務，例如 [Fastly CDN](../cdn/fastly.md) 和 [New Relic](../monitor/new-relic-service.md). 使用沙箱或測試認證來設定付款閘道、運送、通知和其他重要服務。

建議您徹底測試每個服務、驗證效能測試工具，並以管理員和客戶的身分執行UAT測試，直到您認為您的商店已準備好投入生產環境為止。 另請參閱 [部署您的存放區](../deploy/staging-production.md).

### 合併至生產環境

在中繼環境中進行徹底測試後，合併至生產環境，並使用即時憑證進行徹底測試。 一旦您啟動生產網站，客戶必須能夠完成購買，管理員必須能夠管理即時商店。 請參閱下列主題，以取得部署您的存放區及上線的詳細、清楚的逐步說明：

- [部署您的存放區](../deploy/staging-production.md)
- [網站啟動](../launch/overview.md)

### 合併至全域主版

一律將生產計畫碼的副本推送至全域 `master` 萬一迫切需要在不中斷服務的情況下對生產環境進行偵錯。

執行 **非** 從全域建立分支 `master`. 使用 `integration` 分支，為開發和修正建立新的使用中分支。
