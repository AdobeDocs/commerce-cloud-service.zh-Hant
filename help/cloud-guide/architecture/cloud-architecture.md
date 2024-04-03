---
title: Commerce雲端架構
description: 瞭解Starter和Pro專案架構在雲端基礎結構上與Commerce的對比。
feature: Cloud, Iaas, Paas
topic: Architecture
recommendations: noDisplay
exl-id: 37cd6733-c10a-4d06-b784-171da576f9fc
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# Commerce雲端架構

雲端基礎結構上的Adobe Commerce有入門和Pro計畫。 每個計畫都有獨特的架構，可推動您的Adobe Commerce開發和部署流程。 Starter plan和Pro plan架構都會部署資料庫、Web伺服器和快取伺服器，跨多個環境進行端對端測試，同時支援持續整合。

為了進行比較，每個計畫都包含下列基礎架構功能及支援的產品。

|          | 入門者 | Pro |
| -------- | --------------------| ------------------ |
| 核心功能 | <ul><li>[所有Adobe Commerce功能](https://experienceleague.adobe.com/docs/commerce-operations/release/features.html)</li><li>PayPal入門工具</li><li>[Commerce報表](https://business.adobe.com/products/magento/business-intelligence.html?_ga=2.85288604.442698376.1665067470-1322106587.1655147209)</li></ul> | <ul><li>[所有Adobe Commerce功能](https://experienceleague.adobe.com/docs/commerce-operations/release/features.html)</li><li>PayPal入門工具</li><li>[Commerce報表](https://business.adobe.com/products/magento/business-intelligence.html?_ga=2.85288604.442698376.1665067470-1322106587.1655147209)</li><li>[B2B模組](https://business.adobe.com/products/magento/b2b-ecommerce.html?_ga=2.105948422.442698376.1665067470-1322106587.1655147209)</li></ul> |
| 基礎結構和部署 | <ul><li>持續雲端整合工具，使用者不限</li><li>Fastly Content Delivery Network (CDN)、影像最佳化(IO)，以及寬頻寬裕量的額外安全性。 Web應用程式防火牆(WAF)服務僅適用於生產環境。</li><li>[New Relic](../monitor/new-relic-service.md) APM （效能監視）在3個分支上： `master` 和2個您選擇的專案<br>針對Adobe Commerce最佳化的Platform as a service (PaaS)生產、測試和開發環境（共4個作用中環境）</li><li>輸出篩選（輸出防火牆）</li></ul> | <ul><li>持續雲端整合工具，使用者不限</li><li>Fastly Content Delivery Network (CDN)、影像最佳化(IO)，以及寬頻寬裕量的額外安全性。 Web應用程式防火牆(WAF)服務僅適用於生產環境。</li><li>[New Relic](../monitor/new-relic-service.md) 生產上的基礎結構+中繼和生產上的APM （效能監控）。 此 [受管理的警示原則](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts) 對於Adobe Commerce，原則會實作監控最佳實務，以主動通知您有關影響網站效能的應用程式和基礎結構問題。</li><li>以Platform as a Service (PaaS)為基礎 [整合開發](pro-architecture.md#integration-environment) 針對Adobe Commerce最佳化的環境（共2個作用中環境）</li><li>基礎架構即服務(IaaS)：專為中繼和生產環境提供的虛擬基礎架構</li></ul> |
| 高可用性基礎建設 | | [高可用性架構](pro-architecture.md#redundant-hardware) 基礎基礎基礎建設即服務(IaaS)中的三伺服器設定，可提供企業級可靠性和可用性 |
| 專屬硬體 | | 基礎基礎基礎建設服務(IaaS)中的獨立專用硬體，可提供更高等級的可靠性和可用性 |
| 全年無休電子郵件支援 | 核心應用程式和雲端基礎建設的全年無休監控和電子郵件支援 | 核心應用程式和雲端基礎建設的全年無休監控和電子郵件支援 |
| 專屬的客戶技術顧問(CTA) | | 初始啟動期間的專屬技術帳戶管理，從您的訂閱開始，直到您的初始網站啟動為止 |
| 附加元件\* | <ul><li>[B2B模組](https://business.adobe.com/products/magento/b2b-ecommerce.html)</li></ul> |

\* _需額外付費_

## 入門專案

此 [入門計畫架構](starter-architecture.md) 有四個環境：

- **整合** — 整合環境提供兩個可測試的環境。 每個環境都包含作用中的Git分支、資料庫、網頁伺服器、快取、部分服務、環境變數和設定。

- **分段** — 當程式碼和擴充功能通過測試時，您可以合併 `integration` 分支到預備環境，這就會變成您的預先生產測試環境。 其中包括 `staging` 作用中分支、資料庫、網頁伺服器、快取、協力廠商服務、環境變數、設定和服務，例如Fastly和New Relic。

- **生產** — 程式碼就緒並測試後，所有程式碼都會合併至 `master` 用於部署至生產即時網站。 此環境包含您的作用中 `master` 分支、資料庫、Web伺服器、快取、協力廠商服務、環境變數和設定。

- **非使用中** — 您有不限數量的非使用中分支。

## Pro專案

此 [專業計畫架構](pro-architecture.md) 具有全域 `master` 適用於三個環境：

- **整合** — 整合環境提供可測試的環境，其中包括資料庫、Web伺服器、快取、部分服務、環境變數和設定。 您可以開發、部署和測試程式碼，然後再合併至測試環境。

   - _非使用中_ — 您可以根據系統設定的 `integration` 環境，但只有一個使用中的分支(不包括 `integration` )。

- **分段** — 中繼環境是用於生產前的測試，包括資料庫、Web伺服器、快取、協力廠商服務、環境變數、設定以及服務（例如Fastly）。

- **生產** — 生產環境包括適用於資料、服務、快取和存放區的三節點高可用性架構。 生產環境是您的即時公用存放區環境，包含環境變數、設定和協力廠商服務。

## 支援的軟體與服務

雲端基礎結構上的Adobe Commerce使用：

- 作業系統：Debian GNU/Linux
- 網頁伺服器：Nginx
- 資料庫：MySQL (MariaDB)
- 內容傳遞網路(CDN)： Fastly CDN

您可以設定下列服務：

- [PHP](../application/php-settings.md)
- [MySQL](../services/mysql.md)
- [Redis](../services/redis.md)
- [RabbitMQ](../services/rabbitmq.md)
- [Elasticsearch](../services/elasticsearch.md)
- [OpenSearch](../services/opensearch.md)

{{elasticsearch-support}}

>[!NOTE]
>
>另請參閱 [系統需求](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) 在 _安裝指南_ 推薦的版本。

Fastly CDN模組用於中繼和生產環境上的CDN和快取服務。 另請參閱 [設定Fastly服務](../cdn/fastly.md).

如需設定要在實施中使用的軟體版本的相關資訊，請參閱雲端基礎結構設定檔案上的下列Adobe Commerce：

- [應用程式設定(.magento.app.yaml)](../application/configure-app-yaml.md)
- [環境設定(.magento.env.yaml)](../environment/configure-env-yaml.md)
- [路由設定(routes.yaml)](../routes/routes-yaml.md)
- [服務組態(services.yaml)](../services/services-yaml.md)
