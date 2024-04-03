---
title: 零停機部署
description: 瞭解如何在雲端基礎結構專案上部署Adobe Commerce時減少整體停機時間。
feature: Cloud, Deploy, SCD, Themes
exl-id: ff89d2e1-dfc8-4f6d-bd98-947559af13f0
source-git-commit: 225fba1acfd8b3ce4d7ce989c7851e7b0b218680
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 零停機部署

雲端基礎結構上的Adobe Commerce會在以下位置執行應用程式： [_維護作業_ 模式](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html#production-mode) 在部署階段（讓網站離線，直到部署完成）。 您的生產網站處於維護模式的時間長度取決於網站大小、部署期間套用的變更數量，以及靜態內容部署的設定。 您可以設定專案，以便使用 **零** 停機效應。

在部署過程中，所有連線都會佇列長達5分鐘，保留任何作用中工作階段和擱置中的動作，例如加入購物車或結帳。 部署後，佇列會釋放，連線會持續進行而不會中斷。 若要使用此 _連線保留_ 以符合您的優勢，並減少部署 _零_ 停機時，您必須設定專案以使用最有效的部署策略。

使用下列步驟來減少存放區將更新部署到生產環境所需的時間：

1. [升級至 `ece-tools` 封裝](../dev-tools/install-package.md) 或 [更新 `ece-tools` 版本](../dev-tools/update-package.md)
您的雲端基礎結構專案上的Adobe Commerce必須有最新的 `ece-tools` 套裝，讓您可以利用工具來設定最佳部署。 如果您有最新的 `ece-tools`，請繼續進行下一個步驟。

   >[!NOTE]
   >
   >即使最佳實務是使用最新的 `ece-tools` 套件，零停機部署方法可搭配 `ece-tools` [2002.0.13版](../release-notes/cloud-release-archive.md#v2002013) 及更新版本。

1. [設定靜態內容部署](static-content.md)
如果靜態內容部署在部署階段失敗，您的網站會卡在維護模式。 當在建置階段期間發生失敗時，該流程會避免停機，因為它永遠不會開始部署階段。 [在建置階段期間使用最小化HTML產生靜態內容](static-content.md#setting-the-scd-on-build)理想狀態也稱為零停機部署的最佳設定，且 _防止_ 發生失敗時的停機時間。

1. [設定部署後掛接](../application/hooks-property.md)
您必須設定部署後掛接以清除並預熱快取。 根據預設，當網站關閉時，快取清理會在部署階段進行。 將快取清理移至部署後階段表示您的快取會維持作用中狀態，直到部署階段完成，然後您就可以安全地清理快取。

   自訂用來預先載入快取的頁面清單，使用 [WARMUP_PAGES環境變數](../environment/variables-post-deploy.md#warmuppages).

1. [減少佈景主題檔案](../environment/variables-deploy.md#scdmatrix)
您可以藉由設定SCD\_MATRIX環境變數來減少不必要的佈景主題檔案數目。

1. [加速靜態內容部署](../environment/variables-deploy.md#scdthreads)
您可以更新SCD\_THREADS環境變數來增加靜態內容部署的執行緒數量，以加快部署程式。

>[!NOTE]
>
>您可以透過以下方式驗證您的專案設定以獲得最佳部署 [執行理想狀態精靈](smart-wizards.md#verifying-an-ideal-configuration).
