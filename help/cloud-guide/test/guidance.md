---
title: 測試指南
description: 閱讀在雲端基礎結構上啟動Adobe Commerce的測試型別和最佳實務。
exl-id: 1d7897a2-af97-46ab-89c0-2ec54284190e
source-git-commit: aae285d85188bfadd73d5b4e1fea16afa5beb117
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# 測試指南

在雲端基礎結構專案上設定並自訂Adobe Commerce後，最佳實務是在啟動商店網站之前徹底測試您的應用程式。 測試有助於正確管理對叢集規模的期望，並因應未來業務需求適度擴展。

## 功能測試

在開發期間，請務必對雲端基礎結構專案上的Adobe Commerce執行端對端功能測試。 有關在Docker環境中執行功能測試，請參閱以下指南：

- **應用程式測試** — 使用 [Magento功能測試架構(MFTF)](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/) 以在Cloud Docker環境中測試應用程式。

- **程式碼測試** — 使用 [PHP的代碼欺騙測試架構](https://developer.adobe.com/commerce/cloud-tools/docker/test/code-testing/) 用於驗證要貢獻給雲端套件存放庫的程式碼。

## 啟動前最佳實務

將下列測試型別視為在網站啟動前執行的最佳實務：

- **負載測試** — 進行負載測試，以瞭解系統在預期負載下的行為。 例如，測試應用程式上同時作用的使用者數目，讓每個使用者在設定的期間內執行特定數目的交易。 此測試會顯示重要業務關鍵交易的回應時間，例如資料庫或應用程式伺服器行為。 負載測試有助於識別瓶頸。

- **壓力測試** — 挑戰系統內的容量上限，以判斷目前負載遠超過預期最大值時，系統是否執行充分。

- **安全性掃描**—Adobe提供免費的 [安全性掃描工具](../launch/overview.md#set-up-the-security-scan-tool) 用於您的網站。

- **滲透測試** — 電腦系統上的授權模擬網路攻擊，旨在評估系統的安全性。 滲透測試有助於找出弱點或弱點，包括未經授權人士存取系統功能與資料的可能性。

>[!WARNING]
>
>客戶不得對AWS基礎結構或AWS服務本身進行任何安全性評估。 如果您在安全性評估中發現的任何AWS服務中，發現安全性問題， [聯絡AWS安全性](mailto:aws-security@amazon.com) 立即。 另請參閱 [滲透測試的AWS客戶政策](https://aws.amazon.com/security/penetration-testing/).
