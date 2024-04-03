---
source-git-commit: b08443d937dfc18120daa0d6a1277b9c7bca67aa
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---
# 雲端代碼片段

## Elasticsearch警告 {#elasticsearch-support}

>[!WARNING]
>
>雲端基礎結構上的Adobe Commerce不支援Elasticsearch7.11和更新版本。 Adobe Commerce版本2.3.7-p3、2.4.3-p2以及2.4.4和更新版本支援OpenSearch服務。 內部部署安裝仍支援Elasticsearch。

## 增強型整合 {#enhanced-integration-envs}

>[!NOTE]
>
>在2020年6月5日之前布建的專案具有多個較小的整合環境。 如果您需要更大的整合環境以進行測試和開發，請要求升級至增強型整合環境。 請參閱 [整合環境請求](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/announcements/commerce-announcements/integration-environment-enhancement-request-pro-and-starter.html) 中的文章 _Adobe Commerce說明中心_ 以取得詳細資訊。

## 合併選項 {#merge-options}

依預設，部署程式會覆寫 `env.php` 檔案；不過，您可以選擇合併服務組態的一或多個值，而不覆寫所有值。

設定 `_merge` 選項轉換為下列其中一項：

- `true`—**合併** 使用環境變數值設定的服務值。
- `false`—**覆寫** 使用環境變數值設定的服務值。

## 私人存放庫 {#private-repository}

>[!NOTE]
>
>Adobe強烈建議您在雲端基礎結構專案上為Adobe Commerce使用私人存放庫，以保護任何專屬資訊或開發工作，例如擴充功能和敏感設定。

## 專業自助服務警告 {#pro-self-service-warning}

>[!WARNING]
>
>部分 **Pro專案** 需要支援票證，才能更新以下專案的路由設定： `routes.yaml` 檔案和cron設定 `.magento.app.yaml` 檔案。 Adobe建議您在整合環境中更新及測試YAML設定檔，然後將變更部署至測試環境。 如果您在重新部署後未將變更套用至測試網站，且記錄檔中沒有相關的錯誤訊息，則您可以 **必須** [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 說明嘗試的組態變更。 在票證中包含任何更新的YAML設定檔案。

## Pro服務支援 {#pro-update-service}

>[!TIP]
>若為Pro專案，您必須 [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 安裝或更新 [服務](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) 在 `Staging` 和 `Production` 僅限環境。
>
>指出所需的服務變更，包括您更新的 `.magento.app.yaml` 和 `services.yaml` 檔案，並在票證中說明PHP版本。 如需對PHP版本、擴充功能或環境設定的自助變更，請參閱 [PHP設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/php-settings.html) 在 _應用程式設定_.
>
>若變更了 _即時_ 生產環境(**僅限Pro**)，您必須提供最少48小時的通知，好讓雲端基礎結構團隊有充足的時間調配資源及進行安全升級。

## 專業備份 {#pro-backups}

>[!TIP]
>
>在Pro測試和生產環境中，您必須 [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 擷取特定的備份，並在票證中註明日期、時間和時區。
>
>Adobe會 **非** 從自動備份還原任何環境。 另請參閱 [從中繼或生產還原資料庫快照](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production.html) 以取得選擇方法來還原測試或生產快照的協助。

## 重新部署警告 {#redeploy-warning}

>[!WARNING]
>
>當您執行環境的合併、推播或同步化時，或當您觸發手動重新部署時，部署程式就會開始，在此期間會 [!DNL Commerce] 應用程式處於維護模式。 在生產環境中，Adobe建議您在離峰時間完成這項工作，以避免服務中斷。

## 路由預留位置 {#route-placeholder}

>[!NOTE]
>
>下列路由組態範例使用帶有預留位置的路由範本。 此 `{default}` 預留位置代表為網站設定的預設網域。 如果您的專案有多個網域，請使用 `{all}` 用來設定預設網域及所有別名的製程的預留位置。 另請參閱 [設定路由](/help/cloud-guide/routes/routes-yaml.md).

## SCD時間 {#scd-timing-warning}

>[!WARNING]
>
>如果您在部署後應用程式中的靜態內容檔案出現問題（例如遺失自訂主題檔案），請將最大預期執行時間增加至900秒或以上。

## 以案例為基礎的部署 {#scenarios}

>[!NOTE]
>
>替換為 [!DNL ECE-Tools] 2002.1.0和更新版本，您可以使用情境式部署功能，在雲端基礎結構專案上自訂Adobe Commerce的建置、部署和部署後程式。 另請參閱 [以案例為基礎的部署](/help/cloud-guide/deploy/scenario-based.md).

## 服務指示 {#service-instruction}

在專業整合環境和入門環境上使用下列服務設定說明，包括 `master` 分支。

>[!NOTE]
>
>[提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 以變更Pro生產和中繼環境上的服務組態。

## 服務變更 {#service-change-tip}

>[!TIP]
>
>在初始服務設定之後，您可以更新已安裝服務的軟體版本 `services.yaml` 和 `.magento.app.yaml` 組態檔。 另請參閱 [變更服務版本](/help/cloud-guide/services/services-yaml.md#change-service-version) 以取得升級或降級服務的指引。

## 停滯的部署提示 {#stuck-deployment-tip}

>[!TIP]
>
>如需有關停滯部署的協助，請使用 [Adobe Commerce部署疑難排解員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html) 在 _Commerce說明中心_.

## ECE-Tools更新 {#ece-tools-package}

>[!NOTE]
>
>如果您在雲端基礎結構上使用的Adobe Commerce版本不包含 `ece-tools` 封裝，則您必須執行 [一次性升級](/help/cloud-guide/dev-tools/install-package.md) 至您的雲端專案，以移除已棄用的套件。 如果您目前使用 `ece-tools` 套件而且您必須更新它，請參閱 [更新ECE工具套件](/help/cloud-guide/dev-tools/update-package.md).

## 升級秘訣 {#upgrade-tip}

>[!TIP]
>
>在開始升級或修補程式之前，請從整合環境建立使用中分支，並將新分支簽出至您的本機工作站。 將分支專用於升級或修補程式，有助於避免干擾您正在進行的工作。

<!-- Fastly-related snippets begin -->

## 管理員登入 {#admin-login-step}

1. [登入](/help/get-started/onboarding.md#access-your-admin-panel) 傳送給管理員。

## 自動部署自訂VCL程式碼片段 {#automate-vcl-snippet-deployment}

>[!NOTE]
>
>您可以將自訂VCL代碼片段新增至 `$MAGENTO_CLOUD_APP_DIR/var/vcl_snippets_custom` 目錄。 當您按一下時，此目錄中的程式碼片段會自動上傳 _將VCL上傳到Fastly_ 在Commerce Admin中。 另請參閱 [自動自訂VCL程式碼片段部署](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md#automated-custom-vcl-snippets-deployment) Magento2檔案的Fastly CDN模組中。

<!-- Fastly-related snippets end -->
