---
title: 備份管理
description: 瞭解如何在雲端基礎結構專案上手動建立和還原Adobe Commerce的備份。
feature: Cloud, Paas, Snapshots, Storage
exl-id: 1cb00db7-2375-4761-9c07-1e20a74859e0
source-git-commit: 4c3f3f2775e8327476233520e52b589f7264786f
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 0%

---

# 備份管理

您可以隨時使用手動備份使用中的入門環境 **[!UICONTROL Backup]** 中的按鈕 [!DNL Cloud Console] 或使用 `magento-cloud snapshot:create` 命令。

備份或 _快照_ 是環境資料的完整備份，包含執行中服務（MySQL資料庫）的所有持續性資料，以及任何儲存在掛載磁碟區(var、pub/media、app/etc)上的檔案。 快照可以 _非_ 包含程式碼，因為程式碼已儲存在Git型存放庫中。 您無法下載快照的復本。

備份/快照功能可以 **非** 適用於Pro預備和生產環境，依預設會接收定期備份以用於災難回覆。 請參閱 [專業備份與災難回覆](../architecture/pro-architecture.md#backup-and-disaster-recovery) 以取得詳細資訊。 與Pro測試環境和生產環境上的自動即時備份不同，備份是 **非** 自動。 它是 _您的_ 負責手動建立備份或設定cron工作，以定期建立Starter或Pro整合環境的備份。

## 建立手動備份

您可以從以下位置建立任何使用中Starter環境和整合Pro環境的手動備份： [!DNL Cloud Console] 或從Cloud CLI建立快照。 您必須擁有 [管理員角色](../project/user-access.md) 適用於環境。

**若要建立任何Starter環境的備份，請使用[!DNL Cloud Console]**：

1. 登入 [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. 從專案導覽列選取環境。 環境必須為作用中。
1. 在 _備份_ 檢視，按一下 **[!UICONTROL Backup]**. 此選項不適用於Pro環境。

   ![備份](../../assets/button-backup.png){width="150"}

**若要使用建立整合環境的備份[!DNL Cloud Console]**：

1. 登入 [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. 從專案導覽列選取整合/開發環境。 環境必須為作用中。
1. 選取 **[!UICONTROL Backup]** 選項。 此選項適用於Starter和Pro環境。
1. 按一下 **[!UICONTROL Yes]** 按鈕。

**若要使用建立快照 `magento-cloud` CLI**：

1. 在本機工作站上，變更至專案目錄。
1. 簽出要建立快照的環境分支。
1. 建立快照。

   ```bash
   magento-cloud snapshot:create --live
   ```

   或者，您可以使用 `magento-cloud backup` 簡短命令。 此 `--live` 選項讓環境得以執行以避免停機時間。 如需完整的選項清單，請輸入 `magento-cloud snapshot:create --help`.

   範例回應：

   ```terminal
   Creating a snapshot of develop-branch
   Waiting for the activity ID (User created a backup of develop-branch):
   
   Creating backup of develop-branch
   Created backup my-snapshot
   [============================] 45 secs (complete)
   Activity ID succeeded
   Snapshot name: my-snapshot
   ```

1. 驗證最新的快照。

   ```bash
   magento-cloud snapshot:list
   ```

   此清單會傳回有關快照狀態的資訊：

   ```terminal
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

## 還原手動備份

您必須擁有 [管理員存取權](../project/user-access.md) 至環境。 您最多可 **七天** 至 _還原_ 手動備份。 還原備份不會變更目前Git分支的程式碼。 以這種方式還原備份不適用於Pro中繼和生產環境；請參閱 [專業備份與災難回覆](../architecture/pro-architecture.md#backup-and-disaster-recovery).

還原時間會依資料庫的大小而有所不同：

- 大型資料庫(200+ GB)可能需要5小時
- 中型資料庫(150 GB)可能需要2.5小時
- 小型資料庫(60 GB)可能需要1小時

>[!TIP]
>
>不使用備份還原：
>
>- 若要回覆至先前的程式碼，或移除環境中新增的擴充功能，請參閱 [回覆代碼](#roll-back-code).
>- 還原不穩定環境，此環境會 _非_ 有備份，請參閱 [還原環境](../development/restore-environment.md).

**若要使用還原備份[!DNL Cloud Console]**：

1. 登入 [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. 從專案導覽列選取環境。
1. 在 _備份_ 檢視，從中選擇備份 _已儲存_ 清單。 備份功能可以 **非** 適用於Pro環境。
1. 在 ![更多](../../assets/icon-more.png){width="32"} (_更多_)功能表，按一下 **還原**.
1. 檢閱「從備份還原」資訊，然後按一下 **是，還原**.

**若要使用Cloud CLI還原快照**：

1. 在本機工作站上，變更至專案目錄。
1. 檢視要還原的環境分支。
1. 列出所有可用的快照。

   ```bash
   magento-cloud snapshot:list
   ```

   清單會傳回可用快照的相關資訊：

   ```terminal
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

1. 使用清單中的快照ID還原快照。

   ```bash
   magento-cloud snapshot:restore <snapshot-id>
   ```

## 還原災難回覆快照

若要在Pro中繼和生產環境中還原災難回覆快照， [直接從伺服器匯入資料庫傾印](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production#meth3).

## 回覆代碼

備份和快照可以 _非_ 包含程式碼的副本。 您的程式碼已儲存在Git型存放庫中，因此您可以使用Git型命令來回覆（或還原）程式碼。 例如，使用 `git log --oneline` 捲動先前的認可，然後使用 [`git revert`](https://git-scm.com/docs/git-revert) 從特定認可還原程式碼。

此外，您也可以選擇將程式碼儲存在 _非使用中_ 分支。 使用Git命令來建立分支，而非使用 `magento-cloud` 命令。 請參閱關於 [Git命令](../dev-tools/cloud-cli-overview.md#git-commands) （在Cloud CLI主題中）。
