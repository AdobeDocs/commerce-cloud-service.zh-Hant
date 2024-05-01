---
title: Pro架構
description: 瞭解Pro架構支援的環境。
feature: Cloud, Auto Scaling, Iaas, Paas, Storage
topic: Architecture
exl-id: d10d5760-44da-4ffe-b4b7-093406d8b702
source-git-commit: 95b033ba430cb5dc74fa654b9d519dfcd5b6d319
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 0%

---

# Pro架構

雲端基礎結構上的Adobe Commerce Pro架構支援多種環境，可用於開發、測試和啟動您的商店。

- **主版** — 提供 `master` 分支已部署至Platform as a Service (PaaS)容器。
- **整合** — 提供單一 `integration` 分支以進行開發，但您可以建立一個額外的分支。 這最多允許兩個 _主要_ 分支已部署至Platform as a Service (PaaS)容器。
- **分段** — 提供單一 `staging` 分支部署到專用基礎架構即服務(IaaS)容器。
- **生產** — 提供單一 `production` 分支部署到專用基礎架構即服務(IaaS)容器。

下表總結了環境之間的差異：

|                                        | 整合 | 分段 | 生產 |
| -------------------------------------- | ----------- | ----------------- | -------------------- |
| 支援中的設定管理 [!DNL Cloud Console] | 是 | 有限 | 有限 |
| 支援多個分支 | 是 | 否（僅限分段） | 否（僅限生產） |
| 使用YAML檔案進行設定 | 是 | 否 | 否 |
| 在專用的IaaS硬體上執行 | 否 | 是 | 是 |
| 包含Fastly CDN | 否 | 是 | 是 |
| 包含New Relic服務 | 否 | APM | APM + NRI |
| 自動備份 | 否 | 是 | 是 |

>[!NOTE]
>
>Adobe提供用於部署到本機Cloud Docker環境的Cloud Docker for Commerce工具，以便您可以開發和測試Adobe Commerce專案。 另請參閱 [Docker開發](../dev-tools/cloud-docker.md).

## 環境架構

您的專案是單一Git存放庫，具有三個主要環境分支： `integration`， `staging`、和 `production`. 下圖顯示Pro環境的階層式關係：

![Pro環境架構概觀](../../assets/pro-branch-architecture.png)

### 主要環境

在Pro專案上， `master` branch會提供使用中的PaaS環境與您的生產環境。 一律將生產計畫碼的副本推送到 `master` 環境，您便可在不中斷服務的情況下對生產環境進行偵錯。

**警告：**

- 執行 **非** 根據以下專案建立分支： `master` 分支。 使用整合環境建立用於開發的有效分支。

- 請勿使用 `master` 用於開發、UAT或效能測試的環境

### 整合環境

整合環境會在名為PaaS的伺服器網格上的Linux容器(LXC)中執行。 每個環境都包含網站伺服器和資料庫，用以測試您的網站。 另請參閱 [地區IP位址](../project/regional-ip-addresses.md) 以取得AWS和Azure IP位址的清單。

**建議的使用案例：**

整合環境是專為有限的測試和開發而設計，以便將變更移至中繼和生產環境。 例如，您可以使用整合環境來完成下列工作：

- 確保對持續整合(CI)流程的變更與雲端相容

- 在關鍵頁面上測試關鍵工作流程，例如首頁、類別、產品詳細資料頁面(PDP)、結帳和管理員

若要在整合環境中取得最佳效能，請遵循下列最佳實務：

- 限制目錄大小

- 限制使用一或兩名同時使用者

- 停用cron工作並根據需要手動執行

**警告：**

- 無法在整合環境中存取Fastly CDN和New Relic服務

- 整合環境架構不符合測試和生產架構

- 請勿使用 `integration` 用於開發測試、效能測試或使用者驗收測試(UAT)的環境

- 請勿使用 `integration` 測試B2B以瞭解Adobe Commerce功能的環境

- 您無法從資料庫生產或中繼還原整合環境中的資料庫

{{enhanced-integration-envs}}

### 中繼環境

中繼環境提供測試網站的近乎生產環境。 此環境由專屬的IaaS硬體託管，並包含所有服務，例如Fastly CDN、New Relic APM和搜尋。

**建議的使用案例：**

此環境符合生產架構，且專為UAT、內容測試和最終稽核設計，然後再將功能推送至 `production` 環境。 例如，您可以使用 `staging` 完成下列工作的環境：

- 針對生產資料進行回歸測試

- 啟用Fastly快取的效能測試

- 測試新組建，而非在生產環境中修補

- 新組建的UAT測試

- 測試Adobe Commerce的B2B

- 自訂cron設定和測試cron工作

另請參閱 [部署工作流程](pro-develop-deploy-workflow.md#deployment-workflow) 和 [測試部署](../test/staging-and-production.md).

**警告：**

- 啟動生產網站後，請先使用預備環境測試修補程式，以進行生產關鍵性錯誤修正。

- 您無法從建立分支 `staging` 分支。 您會改為從推送程式碼變更 `integration` 分支至 `staging` 分支。

### 生產環境

生產環境會執行您的公開單一和多網站店面。 此環境在專用的IaaS硬體上執行，具備備援的高可用性節點，可為您的客戶提供持續存取和容錯移轉保護。 生產環境包含中繼環境中的所有服務，以及 [New Relic基礎結構(NRI)](../monitor/new-relic-service.md#new-relic-infrastructure) 此服務會自動連線至應用程式資料與效能分析，以提供動態伺服器監控。

**警告：**

您無法從建立分支 `production` 分支。 您會改為從推送程式碼變更 `staging` 分支至 `production` 分支。

### 生產技術棧疊

生產環境有三個虛擬機器器(VM)，位於由每個VM的HAProxy管理的Elastic Load Balancer後面。 每台VM都包含下列技術：

- **Fastly CDN**—HTTP快取和CDN

- **NGINX** — 使用PHP-FPM的Web伺服器，一個執行個體具有多個背景工作

- **GlusterFS** — 檔案伺服器，用於管理所有靜態檔案部署以及四個目錄掛載的同步化：

   - `var`
   - `pub/media`
   - `pub/static`
   - `app/etc`

- **Redis** — 每部虛擬機器器有一部伺服器，只有一部作用中，另外兩部做為復本

- **Elasticsearch** — 在雲端基礎結構2.2到2.4.3-p2上搜尋Adobe Commerce

- **OpenSearch** — 在雲端基礎結構上搜尋Adobe Commerce 2.3.7-p3、2.4.3-p2、2.4.4和更新版本

- **加萊拉** — 資料庫叢集，每個節點有一個MariaDB MySQL資料庫，每個資料庫的唯一識別碼的自動增加設定為三

下圖顯示生產環境中使用的技術：

![生產技術棧疊](../../assets/az-stack-diagram.png)

## 備援硬體

而不是執行傳統的主動式 — 被動式 `master` 或是主要次要設定，雲端基礎結構上的Adobe Commerce會執行 _備援架構_ 其中所有三個執行個體都接受讀取和寫入。 此架構在擴充時可提供零停機時間，並確保交易完整性。

由於獨特的備援硬體，Adobe可提供三部閘道伺服器。 大部分的外部服務可讓您將多個IP位址新增至允許清單，因此擁有多個固定IP位址不成問題。 三個閘道對應至生產環境叢集中的三個伺服器，並保留靜態IP位址。 它完全備援，而且每個層級都具備高可用性：

- DNS
- 內容傳遞網路(CDN)
- 彈性負載平衡器(ELB)
- 包含所有Adobe Commerce服務（包括資料庫和網頁伺服器）的三伺服器叢集

## 備份與災難回覆

雲端基礎結構上的Adobe Commerce使用高可用性架構，該架構會複製三個獨立AWS或Azure可用性區上的每個Pro專案，每個區有一個獨立的資料中心。 除了此備援功能外，Pro預備和生產環境也會獲得定期的即時備份，專門針對下列情況而設計： _災難性失敗_.

**自動備份** 包括來自所有執行中服務的持續資料，例如MySQL資料庫和儲存在掛載磁碟區上的檔案。 備份會儲存至與生產環境位於相同區域的加密彈性區塊儲存(EBS)。 無法公開存取自動備份，因為它們儲存在不同的系統中。

{{pro-backups}}

您可以建立 **手動備份** 使用CLI命令用於測試和生產環境的資料庫。 另請參閱 [備份資料庫](../storage/database-dump.md). 的 `integration` Adobe建議您在雲端基礎結構專案上存取Adobe Commerce後，在應用任何重大變更之前，先建立備份，作為第一步。 另請參閱 [備份管理](../storage/snapshots.md).

### 復原點目標

RPO為上次備份的最長六小時時間（例如06:00、12:00、18:00）。 備份的頻率取決於您計畫的備份排程，以及寫入儲存服務的變更量。

### 保留原則

Adobe會根據下列資料保留原則保留自動備份：

| 時段 | 備份保留原則 |
| ------------------ | ----------------------- |
| 第1天至第3天 | 每小時一次備份 |
| 第4天至第7天 | 每天一次備份 |
| 第2週至第6週 | 每週一次備份 |
| 第8週至第12週 | 每兩週備份一次 |
| 第3個月到第5個月 | 每月一次備份 |

此政策可能會因您的雲端基礎結構計畫而異。

### 復原時間目標

RTO取決於儲存的大小。 大型EBS磁碟區需要更多時間來還原。 還原時間可能會因資料庫大小而異：

- 大型資料庫(200+ GB)可能需要5個小時
- 中型資料庫(150 GB)可能需要2.5小時
- 小型資料庫(60 GB)可能需要1小時的時間

## Pro叢集縮放

Pro群集大小調整與 _計算_ 設定依選擇的雲端提供者(AWS、Azure)、地區和服務相依性而有所不同。 Adobe雲端基礎結構可以擴展Pro叢集，以因應流量期望和服務需求變化。

備援架構可讓Adobe雲端基礎建設得以升級，無需停機。 升級時，這三個執行個體都會輪換以升級容量，而不會影響網站作業。 例如，如果限制在PHP層級，而不是資料庫層級，則可以將額外的Web伺服器新增到現有的叢集。 這提供 _水平縮放_ 以補充資料庫層級的額外CPU所提供的垂直縮放功能。 另請參閱 [擴充架構](scaled-architecture.md).

如果您預期因事件或其他原因而導致流量大幅增加，可請求暫時增加容量。 另請參閱 [如何請求臨時放大](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html) 在 _Commerce說明中心_.
