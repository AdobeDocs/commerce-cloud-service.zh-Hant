---
title: New Relic帳戶管理
description: 瞭解如何存取您的New Relic帳戶，並管理雲端基礎結構專案上Adobe Commerce的存取權、整合和工具使用。
feature: Cloud, Observability
role: Admin
exl-id: ee639e2e-4074-4384-8f68-152bc3bac93b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# New Relic帳戶管理

當Adobe布建您的雲端基礎結構專案時，授權擁有者會收到New Relic的電子郵件，其中包含存取New Relic帳戶的憑證和指示。 如果您沒有收到電子郵件，請使用授權擁有者電子郵件地址來重設New Relic密碼。

## 管理使用者存取權

一個New Relic帳戶只能有一個人員指派給擁有者角色。 如果您必須變更帳戶擁有者，請將管理員角色指派給目前的擁有者，然後將擁有者角色指派給其他使用者。 另請參閱 [更新帳戶擁有者](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/) 在 _New Relic檔案_ 以取得指示。

管理New Relic存取許可權的准則：

- 專案所有者和管理員使用者可以從New Relic帳戶新增和移除使用者。
- 請勿建立超過五個完整存取權 **使用者**.
- 僅授予嚴格要求存取完整功能集的使用者完整存取權。
- 目前尚無免費的特定指引 **受限制** 使用者。

>[!TIP]
>
>在將擁有者角色指派給使用者之前，請確認該使用者存在於雲端基礎結構上Adobe Commerce的New Relic帳戶中。 如果您必須將使用者新增至該帳戶，而現有的帳戶擁有者或管理員無法協助，則任何具有 [Adobe合作關係擁有者帳戶](https://account.newrelic.com/accounts/1311131/users) (適用於New Relic)可代表客戶新增使用者。

至少新增一個 **管理員** 您的New Relic帳戶的使用者，可管理所有存取權、整合和工具使用。

**若要存取New Relic中的使用者管理**：

1. 登入您的 [New Relic帳戶](https://login.newrelic.com/login).

1. 從左下方導覽中選取您的使用者名稱。

1. 按一下 **[!UICONTROL Administration]** 並從清單中選取下列其中一項：

   - **[!UICONTROL User management]** 新增使用者並管理作用中的使用者與擱置的邀請。

   - **[!UICONTROL Access management]** 以管理使用者群組、角色和帳戶。

另請參閱 [使用者管理](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-management-ui-and-tasks/) 在 _New Relic_ 檔案。

## 為入門環境設定New Relic

>[!NOTE]
>
>**Pro環境** 已預先設定為使用New Relic服務，且可略過啟用和連線指示。 如果中繼和生產環境未安裝New Relic APM，或生產環境中無法使用New Relic基礎架構， [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 以要求安裝。

對於入門環境，您必須檢查 `.magento.app.yaml` 檔案以確認 `runtime` 區段包含New Relic擴充功能。 如果尚未設定擴充功能，請新增下列專案：

> `.magento.app.yaml`

```yaml
runtime:
    extensions:
        - newrelic
```

### 套用授權金鑰

若要將雲端環境連線至New Relic，請將New Relic授權金鑰新增至環境。

- 的 **Pro專案**，Adobe會在布建程式期間將授權金鑰新增到您的生產和中繼環境。 您可以登入 [New Relic帳戶](https://login.newrelic.com/login) 驗證雲端基礎結構網站上的Adobe Commerce與New Relic之間的連線。

- 的 **入門專案**，您有New Relic授權金鑰，最多可支援 _三_ 環境。 您必須手動將金鑰新增到您的環境設定。 入門環境未預先布建為使用New Relic服務。

對於入門環境，請將New Relic授權金鑰新增至環境設定，以啟用New Relic整合。 將金鑰新增到測試和生產環境，以及您選擇的其他一個環境。 設定僅需要New Relic授權金鑰。 您可在以下連結中找到其他組態選項的相關資訊： [New Relic報告](https://experienceleague.adobe.com/docs/commerce-admin/config/general/new-relic-reporting.html) 中的主題 _Adobe Commerce使用手冊_.

{{redeploy-warning}}

>[!PREREQUISITES]
>
>- Adobe Commerce帳戶頁面或與專案相關聯的New Relic授權的登入認證
>- [管理員層級存取權](../project/user-access.md) 至入門環境進行設定
>- 要存取的認證 [管理員](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions.html) 適用於環境

**為入門環境設定New Relic**：

1. 從尋找您的New Relic授權金鑰 [!DNL Cloud Console] 或Cloud CLI。

   **[!DNL Cloud Console]方法**：

   - 開啟您的雲端專案 [帳戶頁面](https://accounts.magento.cloud/user).

   - 在 _專案_ 標籤，尋找您的專案。

   - 按一下 **檢視詳細資料** 以取得專案基礎結構資訊。

   - 展開 **New Relic服務** 區段來檢視授權金鑰。

   - 複製授權金鑰。

   **雲端CLI方法**：

   ```bash
   magento-cloud subscription:info services.newrelic
   ```

1. 使用，將New Relic授權金鑰新增至環境 `magento-cloud` CLI

   - 變更至需要授權金鑰的環境。
   - 使用以下專案更新變數值 `magento-cloud` CLI命令：

     ```bash
     magento-cloud variable:update php:newrelic.license --value <newrelic-license-key>
     ```

   您可選擇從 [商務管理員](https://experienceleague.adobe.com/docs/commerce-admin/start/reporting/new-relic-reporting.html#step-3%3A-configure-your-store).

1. 登入您的 [New Relic帳戶](https://login.newrelic.com/login) 以確認您可以從Adobe Commerce環境檢視資料。 另請參閱 [調查績效](investigate-performance.md).

### 移除授權金鑰

您只能在三個使用中環境中使用New Relic授權金鑰。 如果金鑰在三個環境中使用，您必須從其中一個環境中移除金鑰，然後才能將其新增到其他環境。

**從環境中移除授權金鑰**：

1. 列出環境變數。

   ```bash
   magento-cloud variable:list
   ```

   範例回應：

   ```terminal
    +----------------------+-------------+----------------------+---------+
    | Name                 | Level       | Value                | Enabled |
    +----------------------+-------------+----------------------+---------+
    | php:newrelic.license | environment | newrelic-license-key | true    |
    +----------------------+-------------+----------------------+---------+
   ```

   >[!WARNING]
   >
   >如果您將授權金鑰新增為 _專案_ 變數中，您必須移除該專案層級的變數。 專案變數將授權新增至 _每_ 環境分支已建立，可能會消耗或超過授許可權制。 若要列出專案變數： `magento-cloud variable:list --level project`

1. 刪除授權變數。

   ```bash
   magento-cloud variable:delete php:newrelic.license
   ```
