---
title: 第二個中繼環境
description: 瞭解擁有第二個中繼環境的好處和用法，以進行平行測試、問題隔離、版本控制等。
source-git-commit: 51fa75fff952e3832151d47b80baa7f532aa277f
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---


# 第二個中繼環境

在Adobe Commerce Cloud基礎架構中，中繼環境會透過可映象生產環境的設定，確保進行完整的測試和驗證。 此環境可讓您安全地識別和解決Bug，同時確保在所有新功能或變更影響您的即時網站之前無縫整合。

有些專案需要更複雜的開發工作流程。 為了滿足此需求，Adobe提供額外的中繼環境，作為雲端基礎結構的附加選項。 擁有兩個中繼環境有利於複雜專案和跨團隊同時共同作業。

擁有次要預備環境可提供下列優點：

- **平行測試**：使用兩個中繼環境，團隊可同時測試新功能和重要更新，而不會干擾彼此的開發。 例如，您可以將環境專用於功能測試，而保留其他環境用於效能和壓力測試。

- **隔離問題**：當主要測試環境中發生錯誤或問題時，您可以在次要環境中復寫和診斷它們，而不會中斷測試進度。 這可確保疑難排解不會干擾正在進行的測試。

- **版本控制**：更有效地管理您應用程式的不同版本。 主要中繼環境可執行最新穩定組建，而次要測試實驗功能。 這可協助您更好地管理發行週期，並確保實驗性變更不會破壞穩定的建置。

- **增強轉出計畫**：您可以模擬不同的部署案例。 主要預備環境可模擬目前的生產設定，而次要環境則可設定為測試即將發行的版本。

- **使用者驗收測試(UAT)**：使用主要環境進行持續開發時，您可以將次要環境專用於UAT。 這可讓使用者或使用者端在受控制的設定中測試新功能並提供意見回饋，而不會影響測試。

- **回歸測試**：您可以將一個環境用於正向測試，將另一個環境用於回歸測試，確保新的變更不會破壞現有功能。

- **訓練與示範**：使用單一環境來訓練新團隊成員，或向利害關係人展示新功能。 這可確保培訓活動不會中斷測試。

- **私人連結設定**：主要和整合環境不支援私人連結設定。 如果您的開發工作流程需要透過私人連結連結連結的其他環境，以用於開發、測試或任何其他目的，請考慮新增額外的中繼環境。

擁有兩個測試環境可以大幅改善您的工作流程效率、風險管理和應用程式的整體品質。 這些環境提供安全性和彈性，一個中繼環境無法提供。

>[!NOTE]
>
>此設定是附加元件。 需要次要環境的客戶必須聯絡其銷售代表以要求一個。 銷售代表可提供有關定價與布建流程的資訊。

如果您的專案已有其他測試環境，或您考慮升級目前的專案，請考慮下列布建時間表與責任：

- 在向Adobe銷售代表確認請求後，布建程式最多可能需要兩週的時間。

- 新的測試環境僅適用於與您目前測試環境和生產環境相同的區域。

- 您必須更新整合或主環境，並指定您的次要中繼環境將依據哪些環境。 無法從中繼或生產環境複製次要中繼環境。

- 收到新的測試環境後，您可以將其納入開發流程。 就像其他環境一樣，程式碼和資料庫更新由您負責。

## 要求環境

請依照下列步驟以利提出要求：

1. 升級您的分支。

   使用您要用於新環境的程式碼和資料庫，升級您的整合或主要分支。

1. 請聯絡您的銷售代表。

   請聯絡您的Adobe銷售代表，並提供您要作為新中繼環境（整合或主環境）基礎的特定分支。

1. 確認詳細資料。

   您向銷售代表確認詳細資料後，請等候他們確認已收到布建請求且正在處理中。 布建程式完成後，Adobe團隊會傳送確認給您。

1. 部署到您的新環境。

   依照[標準部署步驟](../deploy/staging-production.md)將您的程式碼和資料庫部署到新的中繼環境。