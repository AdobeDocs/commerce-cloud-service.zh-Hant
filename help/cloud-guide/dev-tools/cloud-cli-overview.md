---
title: 雲端CLI
description: 瞭解magento-cloud CLI，以及它如何協助您在雲端基礎結構專案上管理Adobe Commerce的本機開發環境。
exl-id: 70dddd62-0269-4af4-bd2a-1a4fbf11a131
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---


# 雲端CLI

此 `magento-cloud` CLI工具可讓開發人員和系統管理員管理Cloud專案和環境、執行常式並執行自動化工作。 此 `magento-cloud` CLI擴充了 [[!DNL Cloud Console]](../../get-started/cloud-console.md). 安裝之後 `magento-cloud` 本機工作站上的CLI，可讓您使用它管理雲端基礎結構上的Adobe Commerce入門和專業整合環境。

**若要安裝 `magento-cloud` CLI**：

1. 在本機工作站上，變更至您要複製雲端專案的目錄，以及 [檔案系統擁有者](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) 有 _寫入_ 存取。

1. 安裝 `magento-cloud` CLI

   ```bash
   curl -sS https://accounts.magento.cloud/cli/installer | php
   ```

1. 新增 `magento-cloud` CLI至bash設定檔。

   ```bash
   export PATH=$PATH:$HOME/.magento-cloud/bin
   ```

1. 重新載入更新的bash設定檔。

   ```bash
   . ~/.bash_profile
   ```

1. 若要啟動CLI，請呼叫 `magento-cloud` 並在出現提示時輸入您的Cloud帳戶憑證。

   ```bash
   magento-cloud
   ```

   ```terminal
   Welcome to Magento Cloud!
   Please log in using your Magento Cloud account.
   Your email address or username:
   ```

1. 驗證 `magento-cloud` 命令位於您的路徑中。 下列範例列出可用的命令。

   ```bash
   magento-cloud list
   ```

## 常用命令

Adobe設計了這些命令來管理雲端整合環境，並建議您執行 `magento-cloud` 專案目錄中的CLI，讓您省略 `-p <project-ID>` 引數。

下列常用清單 `magento-cloud` CLI指令僅包含必要的選項。 您可以使用 `--help` 選項，以檢視詳細資訊。

| 命令 | 說明 |
| ------------------------------------ | -------------------------------------------------- |
| `magento-cloud login` | 登入專案。 |
| `magento-cloud list` | 列出CLI工具的可用指令。 |
| `magento-cloud environment:list` | 列出目前專案中的環境。 |
| `magento-cloud environment:checkout` | 檢視現有環境。 |
| `magento-cloud environment:merge -e` | 將此環境中的變更與其父項合併。 |
| `magento-cloud variables` | 此環境中的清單變數。 |
| `magento-cloud ssh` | 使用SSH連線到遠端環境。 |
| `magento-cloud url` | 在瀏覽器中開啟Adobe Commerce店面。 |
| `magento-cloud web` | 開啟 [!DNL Cloud Console]. |

## 環境命令

環境 _名稱_ 與環境不同 _ID_ 只有在環境名稱中使用空格或大寫字母時。 環境ID包含所有小寫字母、數字和允許的符號。 環境名稱中的大寫字母會在ID中轉換為小寫；環境名稱中的空格會轉換為破折號。

環境名稱 _無法_ 包含保留給Linux shell或規則運算式的字元。 禁用的字元包括大括弧(`{ }`)，括弧，星號(`*`)，角括弧(`< >`)，&amp;符號(`&`)，% (`%`)和其他字元。

此 `magento-cloud environment:list` 命令會顯示環境階層，而 `git branch` 不會。 如果您有任何巢狀環境，請使用下列專案：

```bash
magento-cloud environment:list
```

### 重新部署環境

不使用推播觸發重新部署。 驗證並確認要重新部署的環境。 如果有處於擱置狀態的組建，請勿使用重新部署。

```bash
magento-cloud environment:redeploy
```

範例回應：

```terminal
Are you sure you want to redeploy the environment <environment-name>? [Y/n]
```

{{redeploy-warning}}

## Git命令

您可能會注意到其中有些指令類似於Git指令。 此 `magento-cloud` 命令會直接連線至Git雲端專案，並提供其他功能。 如果您不使用建立分支 `magento-cloud` CLI，它不會「啟動」，也不會在您推送變更至遠端環境時自動建置。 此 `magento-cloud` CLI指令包含啟動。

若要建立分支，請使用 `magento-cloud` 指令，以啟動分支。

```bash
magento-cloud environment:branch <new-name> <parent-branch>
```

針對分支狀態：

- 使用 `magento-cloud env` 命令以檢視環境分支及其狀態：作用中或非作用中。
- 使用 `magento-cloud environment:activate` 啟動環境分支的指令。

推送空的Git認可以觸發部署。 例如：

```bash
git commit --allow-empty -m "redeploy" && git push <branch-name>
```

有些動作（例如新增使用者）不會進行部署。

### 建立環境分支

下列步驟會示範如何交替使用CLI和Git指令來管理您的本機環境：

1. 在本機工作站上，變更至專案目錄。

1. 切換至 [檔案系統擁有者](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html).

1. 登入您的專案。

   ```bash
   magento-cloud login
   ```

1. 列出您的專案。

   ```bash
   magento-cloud project:list
   ```

1. 列出專案中的環境。 每個環境都包含一個作用中的Git分支，其中包含您的程式碼、資料庫、環境變數、設定和服務。

   ```bash
   magento-cloud environment:list
   ```

   >[!NOTE]
   >
   >請務必使用 `magento-cloud environment:list` 命令，因為它會顯示環境階層，而 `git branch` 命令沒有。

1. 擷取來源分支以取得最新的程式碼。

   ```bash
   git fetch origin
   ```

1. 簽出或切換至特定分支和環境。

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

   Git命令只會檢查Git分支。 此 `magento-cloud checkout` 指令會出庫分支並切換至使用中環境。

   >[!TIP]
   >
   >您可以使用來建立環境分支 `magento-cloud environment:branch <environment-name> <parent-environment-ID>` 命令語法。 建立及啟用環境分支可能需要一些額外的時間。

1. 使用環境ID將任何更新的程式碼提取到您的本機。 如果環境分支是新的，則不需要這樣做。

   ```bash
   git pull origin <environment-ID>
   ```

1. (_可選_)建立 [快照](../storage/snapshots.md) 環境做為備份的ID。

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

## 更新CLI

此 `magento-cloud` 當您登入時，CLI會檢查是否有可用的更新，但您可以使用 `self:update` 命令。 如果有可用的更新，請依照指示更新CLI。

若您的 `magento-cloud` CLI為最新狀態，您會看到下列回應：

```bash
magento-cloud update
```

```terminal
Checking for Magento Cloud CLI updates (current version: X.XX.X)
No updates found
```
