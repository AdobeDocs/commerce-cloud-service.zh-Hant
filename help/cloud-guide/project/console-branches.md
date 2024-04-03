---
title: "使用管理分支 [!DNL Cloud Console]"
description: 瞭解如何使用管理雲端基礎結構上Adobe Commerce的環境分支 [!DNL Cloud Console].
role: Developer
feature: Cloud, Install
exl-id: 2c4ef149-fdb9-473f-91fd-5e6421ac5a43
source-git-commit: a5af3cc6e174a731a8f2ff198acd794384ef4585
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 0%

---

# 使用管理分支 [!DNL Cloud Console]

您可以使用以下其中一種管理環境： [!DNL Cloud Console] 或 `magento-cloud` CLI 您的專案檔案儲存在Git存放庫中。 您可以使用Git命令來管理您的程式碼，但 `magento-cloud` CLI的設計用途是與平台功能互動，而Git指令則否。 另請參閱 [Git命令](../dev-tools/cloud-cli-overview.md#git-commands) （在雲端CLI主題中）。

本主題說明如何使用 [!DNL Cloud Console] 至：

- 新增或刪除環境
- 同步(`git pull`)從父環境
- 合併(`git push`)至上層環境

>[!TIP]
>
>您無法從Pro測試和生產環境建立分支。 您可以從以下位置分支： `master` 分支。

## 建立環境

分支策略會使用常見的Git工作流程，您可在其中開發程式碼並在開發分支中新增擴充功能。 另請參閱 [入門者](../architecture/starter-architecture.md) 和 [Pro](../architecture/starter-develop-deploy-workflow.md) 架構概述。

- 首先，建立 `staging` 分支自 `master` 分支，然後從中分支 `staging` 用於開發。
- 對於Pro，請從以下位置建立開發分支： `Integration` 環境。

您的帳戶支援的有限數量 ![作用中分支](../../assets/icon-active.png){width="32"} (active) and an unlimited number of ![inactive branch](../../assets/icon-inactive.png){width="32"} （非使用中）開發分支。 僅使用「 」新增或刪除分支，以管理作用中和非作用中分支 [!DNL Cloud Console] 或Cloud CLI。 刪除分支之前，必須先停用分支，該分支會保留在 _環境_ 清單為 _非使用中_. 您可以稍後重新啟用分支，也可以 [刪除分支](../dev-tools/cloud-cli-overview.md#) 在環境設定中或使用Cloud CLI。

如果您需要其他使用中的環境進行開發，請提交 [支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

**新增分支的方式**：

1. 登入 [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. 從中選擇專案 _所有專案_ 清單。

1. 選取環境。

   >[!TIP]
   >
   >您的新分支是從此環境複製。 選擇與您要建立之環境類似的父環境。

1. 按一下 **[!UICONTROL Branch]**.

   ![建立分支](../../assets/button-branch.png){width="150"}

1. 在 _正在從分支……_ 表單，輸入分支名稱。

   環境 _名稱_ 與環境不同 _ID_ 只有在環境名稱中使用空格或大寫字母時。 環境ID包含所有小寫字母、數字和允許的符號。 環境名稱中的大寫字母會在ID中轉換為小寫；環境名稱中的空格會轉換為破折號。

   環境名稱 **無法** 包含保留給Linux shell或規則運算式的字元。 禁用的字元包括大括弧(`{ }`)，括弧，星號(`*`)，角括弧(`>`)，&amp;符號(`&`)，% (<code>%</code>)和其他字元。

1. 選取 **[!UICONTROL Environment type]**.

1. 按一下 **[!UICONTROL Create Branch]**.

1. 環境正在部署，請稍候。

   在部署期間，環境狀態為  **處理中**. 成功部署後，的狀態會變更為綠色勾號 **成功**.

## 建立非使用中分支

您無法從Adobe Commerce Cloud主控台或CLI建立非使用中分支。 如果您想建立非作用中分支，請在Git存放庫上建立它，然後使用 `environment.Parent` 選項。

```bash
git push -o "environment.Parent=<parent branch>" <origin> <branch>
```

## 刪除環境

您必須先停用環境，才能刪除環境。 一旦環境處於非使用中狀態，您就可以將其刪除。

**停用環境**：

1. 登入 [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. 從中選擇專案 _所有專案_ 清單。

1. 從導覽列選取環境 _環境_ 清單。

1. 按一下頂端導覽列右側的設定圖示，開啟環境設定。

1. 在 _[!UICONTROL General]_標籤，向下捲動至_[!UICONTROL Deactivate environment]_ 區段並按一下 **[!UICONTROL Deactivate environment and delete data]** 並依照指示操作。

## 同步環境

同步環境（或分支）的方式與 `git pull origin <parent>`. 您可以從上層環境同步更新的程式碼。 您可透過 [!DNL Cloud Console] 適用於所有入門和專業環境。

對於Pro計畫，您可以從測試和生產同步到您的 `master` 分支。 此同步僅提取和推送程式碼，不會提取資料。 若要同步資料，請傾印資料庫資料並將其推送到另一個環境的資料庫。 另請參閱 [移轉及部署靜態檔案和資料](/help/cloud-guide/deploy/staging-production.md#migrate-static-files).

**同步環境**：

1. 登入 [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. 從中選擇專案 _所有專案_ 清單。

1. 在環境清單中，按一下要同步的分支名稱。

1. 按一下（同步）。

   ![同步環境](../../assets/button-sync.png){width="150"}

1. 選取要同步的專案。

   - 取代資料 — （資料與檔案）同步來自父分支的資料庫與內容檔案中的變更。
   - 合併(Merge) - （程式碼）從父分支同步更新的程式碼。

   這樣也會建置CLI指令供您複製和使用。

1. 按一下 **同步**.

## 與上層環境合併

合併環境（或分支）等同於 `git push origin`. 您可以合併以將更新後的程式碼從環境推送至其父環境。 您可以將此程式碼合併至 `master`. 您可以使用部署到測試和生產 `merge` 命令。

**要與父環境合併**：

1. 登入 [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. 從中選擇專案 _所有專案_ 清單。

1. 在環境清單中，按一下要合併的分支名稱。

1. 按一下（合併）。

   ![合併環境](../../assets/button-merge.png){width="150"}

1. 按一下 **合併** 並確認動作。

## 檢視記錄

透過 [!DNL Cloud Console]，您可以檢閱環境的各種記錄，包括建置、部署和部署歷史記錄。

的 **入門者**，即可檢閱建置和部署記錄檔以及部署歷史記錄。 這些環境包括 `master` （生產）分支以及從中建立的所有分支。

的 **Pro**&#x200B;中，您可以檢閱每個環境中的下列記錄：

- 整合 — 建置、部署和部署歷史記錄
- 測試 — 建置記錄檔和部署歷史記錄。 使用SSH登入伺服器以檢視部署記錄。
- 生產 — 建置記錄檔和部署歷史記錄。 使用SSH登入伺服器以檢視部署記錄。

**若要在中檢視記錄[!DNL Cloud Console]**：

1. 登入 [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. 從中選擇專案 _所有專案_ 清單。

1. 選取環境。

   環境檢視提供 [活動清單](activity-stream.md) 顯示 _最近_ 事件，每個嘗試的動作會有一個專案，包括同步、合併、分支、備份等。 按一下 **全部** 以取得完整的部署歷史記錄。

1. 若要檢視建置記錄，請選取帳戶上每個部署記錄的「成功」或「失敗」連結。

>[!TIP]
>
>按一下 **篩選依據** 圖示以取得下拉式清單，並選取要檢視的訊息型別。

## 從私人Git存放庫提取程式碼

您在雲端基礎結構專案上的Adobe Commerce可包含來自私人Git存放庫的程式碼。 例如，您可能在私人存放庫中擁有自訂模組或主題的程式碼。 若要這麼做，您必須將專案的公開SSH金鑰新增至您的私人Git存放庫，並更新您的專案 `composer.json` 檔案。

若要將部署金鑰新增至您的私人GitHub存放庫，您必須是該存放庫的管理員。 GitHub允許您僅對一個存放庫使用部署金鑰。

如果您偏好讓專案存取多個存放庫，您可以將SSH金鑰附加至自動使用者帳戶。 由於此帳戶不是由人類使用，因此稱為 [電腦使用者](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys). 將電腦帳戶新增為共同作業人員，或將電腦使用者新增至具有存放庫存取權的團隊。

>[!INFO]
>
>Adobe建議將此程式碼新增並合併至專案Git存放庫。 如果您未設定連線，則可能會遇到建置問題。

**尋找您的SSH公開金鑰**：

1. 登入 [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. 從中選擇專案 _所有專案_ 清單。

1. 按一下上方導覽列右側的設定圖示。

1. 在 _專案設定_，按一下 **[!UICONTROL Deploy Key]**.

1. 將部署金鑰複製到剪貼簿，以便用於下列其中一個Git型方法：

>[!BEGINTABS]

>[!TAB GitHub]

### 輸入您的GitHub部署金鑰

在GitHub上，部署金鑰預設為唯讀。

**若要輸入您的專案公開金鑰作為GitHub部署金鑰**：

1. 以管理員身分登入您的GitHub存放庫。
1. 按一下存放庫 **[!UICONTROL Settings]** 標籤。

   >[!NOTE]
   >
   >如果沒有看到此選項，表示您不是以存放庫管理員的身分登入，且無法完成此工作。 請要求您的GitHub存放庫管理員執行此操作。

1. 在 _設定_ 索引標籤在左側導覽中，按一下 **[!UICONTROL Deploy Keys]**.
1. 按一下 **[!UICONTROL Add deploy key]**.
1. 按照提示操作。

在 `composer.json`，使用 `<user>@<host>:<.git</code>` 格式，或 `ssh://<user>@<host>:<port>/<path>.git` 若使用非標準連線埠。

>[!TAB 位元貯體]

### 輸入您的Bitbucket部署金鑰

**若要輸入您的專案公開金鑰做為Bitbucket部署金鑰**：

1. 以管理員身分登入您的Bitbucket存放庫。
1. 在左側導覽列中，按一下 **[!UICONTROL Settings]**.
1. 按一下「一般」 > **[!UICONTROL Deployment Keys]**.
1. 按一下 **[!UICONTROL Add Key]**.
1. 按照提示操作。

>[!TAB GitLab]

### 輸入您的GitLab部署金鑰

**新增專案的公開SSH金鑰做為GitLab部署金鑰**：

1. 以擁有者身分登入您的GitLab存放庫。
1. 確認 _管道_ 已為您的專案啟用選項：

   1. 在專案設定中，展開 **[!UICONTROL Visibility, project, features, permissions]** 區段。
   1. 如有必要，請按一下 **[!UICONTROL Pipelines]** 以啟用選項。

1. 將您的公開SSH金鑰新增至CI/CD設定。

   1. 在左側導覽區域中，按一下「設定> **[!UICONTROL CI / CD]**.
   1. 按一下「部署金鑰」 **展開** 以設定金鑰。
   1. 在 _部署金鑰_ 表單，將部署金鑰名稱新增至 **[!UICONTROL Title]** 並將您的公開SSH金鑰貼到 **[!UICONTROL Key]** 欄位。
   1. 按一下 **[!UICONTROL Add Key]** 以儲存組態。

>[!ENDTABS]

## 保護環境和分支的安全

您可以從任何位置透過網頁瀏覽器使用存取您的專案和環境 [!DNL Cloud Console]. 您可以為生產環境、商店和網站設定安全性。 本節可協助您確保嚴格針對開發人員、DBA等的整合與測試環境的安全性。

>[!WARNING]
>
>**不要** 使用下列方法來保護Pro測試和生產環境的安全。 這會中斷Fastly快取。 使用 [封鎖](../cdn/fastly-vcl-blocking.md) Adobe Commerce的Fastly CDN中可用的功能。

**保護環境**：

1. 登入 [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. 從中選擇專案 _所有專案_ 清單。

1. 選取環境並按一下導覽列上的設定圖示。

1. 在環境設定上 _一般_ 標籤，按一下 **開啟** 的 **[!UICONTROL HTTP access control enabled]** 以啟用安全存取。 您可以在認證或IP位址之間選擇，以篩選存取許可權。

1. 若要依認證篩選，請按一下 **[!UICONTROL Add Login]**，輸入使用者名稱和密碼，然後按一下 **[!UICONTROL Add Login]** 以新增。

1. 若要依IP位址篩選，請在清單中輸入IP位址，並附上 `deny` 或 `allow`. 例如：

   ```text
   123.456.789.111/29 allow
   123.456.789.112/29 allow
   234.123.567.111/29 allow
   0.0.0.0/0 deny
   ```

1. 按一下 **[!UICONTROL Save]**. 這會重新部署環境以更新安全性和設定。 Adobe建議在完成安全性設定後測試環境。
