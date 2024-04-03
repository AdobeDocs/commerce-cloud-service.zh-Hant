---
title: 使用CLI管理分支
description: 瞭解如何使用Cloud CLI在雲端基礎結構上管理Adobe Commerce的環境分支。
role: Developer
feature: Cloud, Install
exl-id: a871c7e2-4506-4a05-8fc2-fc5ef2afe609
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# 使用CLI管理分支

若要安裝 `magento-cloud` CLI，請參閱 [雲端CLI參考](../dev-tools/cloud-cli-overview.md). 安裝之後 `magento-cloud` CLI和設定SSH金鑰來遠端存取您的雲端基礎結構，您可以使用 `magento-cloud` 用於管理專案環境的CLI命令。 如需有關環境架構的資訊，請參閱 [入門架構](../architecture/starter-architecture.md) 或 [Pro架構](../architecture/pro-architecture.md).

若要使用管理分支和環境 [!DNL Cloud Console]，請參閱 [使用管理分支 [!DNL Cloud Console]](../project/console-branches.md).

## 使用CLI命令

此 `magento-cloud` CLI命令與Git命令類似。 您可以使用這些專案來連線至您的專案並管理您的環境。 雖然您可以從任何目錄執行命令，但建議您從專案目錄執行這些命令。 從專案目錄執行時，您可以省略 `-p <project-ID>` 引數。 請參閱 [雲端CLI參考](../dev-tools/cloud-cli-overview.md).

## 複製專案

下列指示使用 `magento-cloud` CLI指令和Git指令可將您的專案複製到本機工作站。 若要檢視以下專案的完整清單： `magento-cloud` CLI命令，使用 `magento-cloud list` 命令。

>[!IMPORTANT]
>
>有些Git命令無法在Adobe Commerce的雲端基礎結構專案中完成動作。 例如，您可以使用Git指令建立分支，但無法建立和啟動新環境。 您必須使用建立環境 `magento-cloud environment:branch <branch-name>` 讓環境成為 _主要_. 或者，您可以使用 [!DNL Cloud Console] 以建立作用中的環境。 另請參閱 [雲端CLI參考](../dev-tools/cloud-cli-overview.md#git-commands).

**複製專案 `master` 環境**：

1. 使用登入您的本機工作站 [檔案系統擁有者](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) 帳戶。

1. 變更為Web伺服器或虛擬主機 _docroot_ 目錄。

1. 使用登入 `magento-cloud` CLI

   ```bash
   magento-cloud login
   ```

1. 列出您的專案。

   ```bash
   magento-cloud project:list
   ```

1. 複製專案。

   ```bash
   magento-cloud project:get <project-ID>
   ```

   出現提示時，請提供目錄名稱。

1. 變更為 `magento2` 目錄。

1. 列出專案的可用環境。

   ```bash
   magento-cloud environment:list
   ```

   >[!IMPORTANT]
   >
   >此 `magento-cloud environment:list` 命令會顯示環境階層，而 `git branch` 命令沒有。

1. 擷取遠端分支。

   ```bash
   git fetch origin
   ```

1. 提取更新的程式碼。

   ```bash
   git pull origin <environment-ID>
   ```

>[!TIP]
>
>另請參閱 [整合](../integrations/overview.md) 如需在雲端基礎結構上搭配Adobe Commerce使用Git型託管服務的相關資訊。

## 建立開發分支

複製專案並更新Adobe Commerce管理員帳戶設定後，您可以分支進行開發。 如前所述，您必須使用 `magento-cloud environment:branch <branch-name>` 命令或 [!DNL Cloud Console] 讓環境變成 _主要_.

- 的 [入門者](../architecture/starter-develop-deploy-workflow.md#clone-and-branch)，考慮建立分支 `staging`，然後依據以下內容建立開發分支： `staging` 分支。
- 的 [Pro](../architecture/pro-develop-deploy-workflow.md#development-workflow)，根據下列專案建立開發分支： `Integration` 分支。

**建立開發分支的方式**：

1. 在本機工作站上，變更至專案目錄。

1. 根據專案工作流程建議的分支建立環境。

   ```bash
   magento-cloud branch <new-environment-name> integration
   ```

1. 更新相依性。

   ```bash
   composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
   ```

1. [_可選_] 建立 [備份](../storage/snapshots.md) 環境的。

### 合併分支

完成開發後，將此分支合併至父級：

1. 認可和推送程式碼變更：

   ```bash
   git add -A && git commit -m "Add message here"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. 與上層環境合併：

   ```bash
   magento-cloud environment:merge <environment-ID>
   ```

### 刪除環境

只有在您確定不再需要某個環境時，才將其刪除。 刪除環境後，就無法復原環境。

>[!WARNING]
>
>您無法刪除 `master` 任何專案的分支。

您必須是專案管理員、環境管理員或帳戶擁有者才能執行此工作。 另請參閱 [管理使用者對雲端專案的存取](../project/user-access.md).

當您刪除環境時，環境會設為 _非使用中_. 程式碼仍可在Git分支中使用，但不再包含服務或資料庫。 若要完全刪除環境，您也必須刪除對應的遠端Git分支。

**刪除環境**：

1. 在本機工作站上，變更至專案目錄。

1. 從遠端伺服器擷取更新。

   ```bash
   git fetch
   ```

1. 刪除環境分支。

   ```bash
   magento-cloud environment:delete <environment-ID>
   ```

   您可以選擇將多個環境ID新增至delete命令，一次刪除多個環境。

   ```bash
   magento-cloud environment:delete <environment-1-ID> <environment-2-ID>
   ```

1. 回應刪除本機環境和對應遠端環境的提示。

   ```terminal
   The environment <environment-ID> is currently active: deleting it will delete all associated data.
   Are you sure you want to delete the environment <environment-ID>? [Y/n]
   ```

   刪除環境會將其置於 _非使用中_ 州別。

   ```terminal
   Delete the remote Git branch too? [Y/n]
   ```

   刪除遠端Git分支會從專案移除環境。

1. 等待環境刪除。

   ```terminal
   Deleting environment <environment-ID>
   Waiting for the activity...
     Deleting environment <project-id>-<environment-ID>-xxxxxx
   
     [============================]  1 min (complete)
   Activity ID succeeded
   Deleted remote Git branch <environment-ID>
   Run git fetch --prune to remove deleted branches from your local cache.
   ```

>[!TIP]
>
>若要啟用非使用中環境，請使用 `magento-cloud environment:activate` 命令。

## 與遠端環境互動

在您之後 [設定SSH金鑰](../development/secure-connections.md)，您可以 [從您的本機工作區連線到遠端環境](../development/secure-connections.md#connect-to-a-remote-environment) 與您的專案服務互動，並修改設定。
