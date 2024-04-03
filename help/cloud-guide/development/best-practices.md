---
title: 升級專案的最佳實務
description: 檢視升級專案檔案的最佳實務清單。
feature: Cloud, Best Practices, Upgrade
exl-id: 7d0a2627-e4c5-46b4-9e6c-24d20fa4f92f
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# 升級專案的最佳實務

遵循建置和部署的最佳實務，並使用 [升級與修補程式](../development/commerce-version.md) 升級應用程式的工作流程。 請使用下列准則來規劃您的升級與升級後的工作：

- **備份您的專案** — 在升級Adobe Commerce和任何第三方或自訂擴充功能之前，請先在整合、測試和生產環境中備份資料庫。 另請參閱 [備份資料庫](../development/commerce-version.md#project-backup).

- **檢查相容性問題**-

   - 確認所有自訂主題都與新的Adobe Commerce版本相容

   - 升級協力廠商和自訂擴充功能後，請使用 `magento-cloud local:build` 在部署之前驗證撰寫器相依性的命令。

   - 請檢閱Adobe Commerce發行說明和擴充功能檔案，以確保您已實作任何必要的因應措施或設定變更，以解決與升級Adobe Commerce版本和擴充功能相關的已知功能問題和錯誤。

   - 請確認已安裝的服務版本與新的Adobe Commerce版本相容，並視需要升級服務。 另請參閱 [服務](../services/services-yaml.md).

   - 測試您的資料庫，解決Adobe Commerce版本和擴充功能更新所導致的任何問題。

   - 在部署到遠端環境之前，對環境特定的設定進行任何必要的更新。

   - 請確定搜尋服務版本與PHP使用者端版本相容。 另請參閱 [設定Elasticsearch](../services/elasticsearch.md) 或 [設定OpenSearch](../services/opensearch.md).

- **檢查遠端環境中的資料庫連線和可用儲存空間**-

   - 使用SSH登入遠端伺服器並驗證與MySQL資料庫的連線。 另請參閱 [連線到資料庫](../services/mysql.md#connect-to-the-database).

   - 驗證遠端環境中的可用儲存空間 — 使用 `disk free` 命令以檢視和管理雲端環境中的可用磁碟空間。 另請參閱 [管理磁碟空間](../storage/manage-disk-space.md).

      - 檢查已升級資料庫的大小，並確認 `services.yaml` 檔案已配置足夠的磁碟空間。

      - 釋放磁碟空間 — 清除快取，然後清除 `/log` 和 `/tmp` 目錄。

- **在部署到中繼之前，在本機和整合環境中規劃並執行成功的升級** — 升級後，測試您的部署並解決任何問題。

- **先將程式碼合併到測試環境，然後再合併到生產環境** — 在將變更推送至生產環境之前，請先測試並解決中繼環境中的任何問題。

- **完成升級後的工作**-

   - 使用SSH登入遠端伺服器並驗證下列專案：

      - 視需要檢查索引器狀態並重新索引。 另請參閱 [管理索引子](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html) 在 _設定指南_.

      - 檢查 `cron` 記錄檔和 `cron_schedule` Adobe Commerce資料表驗證cron狀態，並視需要重新執行cron工作。
另請參閱 [記錄](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html#logging) 在 _設定指南_.

   - 在中繼和生產環境中完成升級後使用者驗收測試UAT，並修正與協力廠商和自訂擴充功能升級相關的任何問題。
