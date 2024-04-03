---
title: 「登入 [!DNL Cloud Console]"
description: 瞭解 [!DNL Cloud Console] 適用於Adobe Commerce的雲端基礎結構。
recommendations: noDisplay, catalog
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: c19a36b6-e5e8-461c-a82c-68b7bf121999
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# 登入 [!DNL Cloud Console]

此 [!DNL Cloud Console] 提供互動式方法來建置、管理和部署Commerce程式碼。 此 [!DNL Cloud Console] 是更現代、更方便使用的體驗，並為未來介面增強功能奠定了基礎。

[登入 [!DNL Cloud Console]](https://console.adobecommerce.com) 以檢視您的專案清單。

![專案清單](../assets/ui-allprojects-list.png)

## 功能

新增或改善的功能包括：

- 清楚概述專案和環境特性
- 具有可排序歷史記錄的活動資料流
- 入門專案的手動備份管理和記錄
- 增強的記錄檢視
- 可排序清單
- 新增整合的簡單表單和指南
- 網頁內容可及性指引(WCAG)法規遵循

![[!DNL Cloud Console]](../assets/CloudConsole.svg)

新增或改良的功能如下：

| 功能 | 功能改善 |
| -------------- | ----------------------------------- |
| [活動資料流](../cloud-guide/project/activity-stream.md) | 與執行、擱置或歷史動作的可排序清單互動。 選取活動並檢視記錄，或取消執行中的組建。 |
| [專案和環境概觀](../cloud-guide/project/overview.md#project-overview) | 開啟您的專案，並檢視專案詳細資訊和環境清單的概觀。 環境概觀提供有關環境狀態、應用程式存取和最近活動的更多詳細資訊。 |
| [整合表單](../cloud-guide/integrations/overview.md) | 使用簡單的表單和指引來新增整合，例如位元貯體或Slack通知。 |
| [專案清單](../cloud-guide/project/overview.md#cloud-console) | 此 _所有專案_ 檢視會列出您有權存取的所有專案。 您可以按一下 **[!UICONTROL Show filters]** 並依型別、地區或計畫篩選您的專案清單。 |
| [變數可見度選項](../cloud-guide/environment/variable-levels.md) | 在建置或執行階段限制專案層級或環境層級變數的可見度。 |

<!-- The following are features yet to be activated:
| **Apps and services topology** | The Apps & Services topology is visible on Project and Environment views. This interactive diagram allows you to select a service and view the relationship details, such as name, type, version, port, and more. Click **[!UICONTROL View details]** to access the overview and configuration panel for each service. | -->

## 主控台問題

**_我可以在哪裡找到快照功能_**？

的 [!DNL Starter] 專案，現在稱為快照功能 _備份_. 您可以建立 [!DNL Starter] 來自的環境 [!DNL Cloud Console] 或從Cloud CLI建立快照。 您必須擁有環境的管理員角色。

從專案導覽列選取環境。 環境必須為作用中。 選取 **[!UICONTROL Backups]** 標籤。 目前，此選項不適用於Pro環境。

**_其中是環境的已設定路由清單_**？

您可在以下網址找到已設定路由的清單： _服務_ 索引標籤進行標籤。

從專案導覽列選取環境。 選取 **[!UICONTROL Services]** 標籤。 此 **路由器** 概述會顯示已設定的路由。 目前，您無法從新增路由 [!DNL Cloud Console].

## 帳戶功能表

右上角是您的帳戶功能表。 按一下功能表的向下箭頭，然後選取 **[!UICONTROL My Profile]**. 在 _我的設定檔_ 檢視，您可以控制您的使用者詳細資料和顯示設定，管理 [安全性驗證](../cloud-guide/project/user-access.md#user-authentication-requirements)， [API權杖](../cloud-guide/project/user-access.md#create-an-api-token)、和 [ssh金鑰](../cloud-guide/development/secure-connections.md).
