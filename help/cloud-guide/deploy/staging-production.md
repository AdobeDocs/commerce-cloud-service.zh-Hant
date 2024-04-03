---
title: 部署至測試與生產
description: 瞭解如何將雲端基礎結構上的Adobe Commerce程式碼部署到中繼和生產環境，以供進一步測試。
feature: Cloud, Console, Deploy, SCD, Storage
exl-id: 4b82289f-ee04-4b14-a0ed-7a8a19fc6a6a
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 0%

---

# 部署至測試與生產

部署和上線的程式從開發開始，接著是測試，最後是在生產環境中上線。 Adobe提供端對端環境解決方案，確保設定的一致性。 每個環境都支援對店面進行直接URL存取，以及對CLI命令進行管理員和SSH存取。

當您準備好部署存放區時，必須先在中繼環境中完成部署和測試，才能部署到生產環境。 本節提供建置和部署程式、移轉資料和內容以及測試的深入指示和資訊。

>[!TIP]
>
>Adobe建議建立 [備份](../storage/snapshots.md) 部署前對環境的影響。

此外，您也可以啟用 [使用New Relic追蹤部署](../monitor/track-deployments.md) 以監控部署事件，並協助您分析部署之間的效能。

## 入門部署流程

Adobe建議建立 `staging` 分支自 `master` 分支以最好地支援您的入門計劃開發與部署。 然後，您準備好四個使用中環境中的兩個： `master` 用於生產和 `staging` 用於測試。

如需流程的詳細資訊，請參閱 [入門開發與部署工作流程](../architecture/starter-develop-deploy-workflow.md).

## 專業部署流程

Pro隨附大型整合環境，有兩個作用中的分支，一個全球 `master` 分支、中繼和生產分支。 當您建立專案時，程式碼已準備好進行分支、開發及推送，以建置和部署您的網站。 雖然整合環境可以有許多分支，但每個環境的測試與生產只有一個分支。

如需流程的詳細資訊，請參閱 [Pro開發與部署工作流程](../architecture/pro-develop-deploy-workflow.md).

## 將程式碼部署到中繼環境

中繼環境提供接近生產的環境，包括資料庫、網頁伺服器和所有服務，包括Fastly和New Relic。 您可以透過以下方式完全推送、合併及部署 [[!DNL Cloud Console]](../project/overview.md) 或 [雲端CLI命令](../dev-tools/cloud-cli-overview.md) 透過終端機應用程式。

### 使用部署程式碼 [!DNL Cloud Console]

此 [!DNL Cloud Console] 提供在整合、測試和生產環境中為入門和專業計畫建立、管理和部署程式碼的功能。

**對於Pro專案，將整合分支部署至測試環境**：

1. [登入](https://accounts.magento.cloud) 至您的專案。
1. 選取 `integration` 分支。
1. 選取 **合併** 部署到中繼的選項。

   ![合併](../../assets/button-merge.png){width="150"}

1. 全部完成 [測試](../test/staging-and-production.md) 在中繼環境中。
1. 當測試準備就緒時，選取 **合併** 部署到生產環境的選項。

**首先，將開發分支部署到中繼環境**：

1. [登入](https://accounts.magento.cloud) 至您的專案。
1. 選取準備的程式碼分支。
1. 選取 **合併** 部署到中繼的選項。

   ![合併](../../assets/button-merge.png){width="150"}

1. 全部完成 [測試](../test/staging-and-production.md) 在中繼環境中。
1. 當測試準備就緒時，選取 **合併** 部署到生產環境的選項(`master`)。

### 使用命令列部署程式碼

雲端CLI提供部署程式碼的命令。 您需要SSH和Git存取權才能存取專案。

#### 步驟1：部署和測試整合環境

1. 登入專案後，請檢視整合環境：

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. 將您的本機整合環境與遠端環境同步：

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. 建立環境的快照作為備份：

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. 視需要更新本機分支中的程式碼。

1. 新增、提交和推送變更至環境。

   ```bash
   git add -A && git commit -m "Commit message" && git push origin <environment-ID>
   ```

1. 完成網站測試。

#### 步驟2：合併對測試環境的變更並進行部署

1. 請檢視測試環境：

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. 將您的本機中繼環境與遠端環境同步：

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. 建立環境的快照作為備份：

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. 將整合環境合併至預備以進行部署：

   ```bash
   magento-cloud environment:merge <integration-ID>
   ```

1. 完成網站測試。

#### 步驟3：部署到生產

1. 出庫、同步處理及建立本機生產環境的快照。

1. 將中繼環境合併至生產環境以進行部署：

   ```bash
   magento-cloud environment:merge <staging-ID>
   ```

1. 完成網站測試。

## 移轉靜態檔案

[靜態檔案](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) 儲存在 `mounts`. 將檔案從來源掛載位置（例如您的本機環境）移轉至目的地掛載位置的方法有兩種。 兩種方法都使用 `rsync` 公用程式，但Adobe建議使用 `magento-cloud` 用於在本機與遠端環境之間移動檔案的CLI。 Adobe建議使用 `rsync` 將檔案從遠端來源移動到其他遠端位置時，使用的方法。

### 使用CLI移轉檔案

您可以使用 `mount:upload` 和 `mount:download` 在本機與遠端環境之間移轉檔案的CLI命令。 這兩個命令都使用 `rsync` 公用程式，但CLI命令提供根據雲端基礎結構環境上的Adobe Commerce量身打造的選項和提示。 例如，如果您使用不含選項的簡單指令，CLI會提示您選取要上載或下載的掛載或掛載。

```bash
magento-cloud mount:download
```

範例回應：

```terminal
Enter a number to choose a mount to download from:
  [0] app/etc
  [1] pub/static
  [2] var
  [3] pub/media
  [4] All mounts
 > 3

Target directory: ~/pub/media/

Downloading files from the remote mount pub/media to pub/media

Are you sure you want to continue? [Y/n] Y
```

**若要從本機上傳檔案 `pub/media/` 資料夾到遠端 `pub/media/` 目前環境的資料夾**：

```bash
magento-cloud mount:upload --source /path/to/project/pub/media/ --mount pub/media/
```

範例回應：

```terminal
Uploading files from pub/media to the remote mount pub/media

Are you sure you want to continue? [Y/n] Y

  building file list ...   done
  ./
  sample-file.jpeg

  sent 8.43K bytes  received 48 bytes  3.39K bytes/sec
  total size is 154.57K  speedup is 18.23
```

使用 `--help` 的選項 `mount:upload` 和 `mount:download` 命令以檢視更多選項。 例如，有一個 `--delete` 在移轉期間移除無關檔案的選項。

### 使用rsync移轉檔案

或者，您可以使用 `rsync` 移轉檔案的公用程式。

```bash
rsync -azvP <source> <destination>
```

這個指令使用下列選項：

- `a`-archive
- `z` — 在移轉期間壓縮檔案
- `v`-verbose
- `P` — 部分進度

另請參閱 [rsync](https://linux.die.net/man/1/rsync) 說明。

>[!NOTE]
>
>若要將媒體直接從遠端環境傳輸到遠端環境，您必須啟用SSH代理程式轉送，請參閱 [GitHub指南](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

**直接將靜態檔案從遠端環境移轉至遠端環境（快速方法）**：

1. 使用SSH登入來源環境。 請勿使用 `magento-cloud` CLI 使用 `-A` 選項很重要，因為它可啟用驗證代理程式連線的轉送。

   >[!TIP]
   >
   >若要尋找 **SSH存取** 連結至您的 [!DNL Cloud Console]，選取環境並按一下 **存取網站**.

   ```bash
   ssh -A <environment_ssh_link@ssh.region.magento.cloud>
   ```

1. 使用 `rsync` 命令以複製 `pub/media` 從您的來源環境到其他遠端環境的目錄。

   ```bash
   rsync -azvP pub/media/ <destination_environment_ssh_link@ssh.region.magento.cloud>:pub/media/
   ```

1. 登入其他遠端環境，驗證檔案是否已成功移轉。

## 移轉資料庫

>[!WARNING]
>
>資料庫匯入和匯出作業可能需要很長的時間，這會影響網站效能和可用性。 在非尖峰時間排程匯入和匯出作業，以防止生產網站上的效能緩慢或中斷。

>[!BEGINSHADEBOX]

**先決條件：** 資料庫傾印（請參閱步驟3）應包含資料庫觸發程式。 若要傾印這些檔案，請確認您擁有 [TRIGGER許可權](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_trigger).

>[!IMPORTANT]
>
>整合環境資料庫僅供開發測試使用，其中可能包含您不想移轉至中繼和生產環境的資料。

如需持續整合部署，請Adobe **不推薦** 將資料從整合移轉至測試和生產。 您可以傳遞測試資料或覆寫重要資料。 任何重要設定都會使用 [組態檔](../store/store-settings.md) 和 `setup:upgrade` 命令進行建置和部署。

>[!ENDSHADEBOX]

Adobe **建議** 將資料從生產環境移轉至測試環境，完整測試您的網站，並儲存在具有所有服務和設定的近乎生產環境中。

>[!NOTE]
>
>若要將媒體直接從遠端環境傳輸到遠端環境，您必須啟用ssh代理程式轉送，請參閱 [GitHub指南](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

### 備份資料庫

建立資料庫備份是最佳作法。 下列程式使用下列的指引 [備份資料庫](../storage/database-dump.md).

**傾印資料庫**：

1. [使用SSH登入遠端環境](../development/secure-connections.md#use-an-ssh-command) 包含要複製的資料庫。

1. 列出環境關係，並記下資料庫登入資訊。

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

   對於Pro Staging and Production，資料庫的名稱位於 `MAGENTO_CLOUD_RELATIONSHIPS` 變數（通常與應用程式名稱和使用者名稱相同）。

1. 建立資料庫的備份。 若要選擇資料庫傾印的目標目錄，請使用 `--dump-directory` 選項。

   對於入門環境和Pro整合環境，請使用 `main` 作為資料庫的名稱：

   ```bash
   php vendor/bin/ece-tools db-dump main
   ```

   傾印選項：
   - `--dump-directory=<dir>` — 選擇資料庫傾印的目標目錄
   - `--remove-definers` — 從資料庫傾印移除DEFINER陳述式

1. 雖然偏好使用ECE-Tools方法，但另一種方法是使用GZIP格式的原生MySQL建立資料庫傾印檔案。

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers <database-name> | gzip - > /tmp/database.sql.gz
   ```

   如果您已在目標環境中設定雙因素驗證，最好排除相關的2FA表格，以避免在資料庫移轉後重新設定：

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers --ignore-table=<database-name>.tfa_user_config --ignore-table=<database-name>.tfa_country_codes <database-name> | gzip - > /tmp/database.sql.gz
   ```

1. 型別 `logout` 以終止SSH連線。

### 刪除並重新建立資料庫

匯入資料時，您必須卸除並建立資料庫。

**刪除並重新建立資料庫的方式**：

1. 建立 [SSH通道](../development/secure-connections.md#ssh-tunneling) 到遠端環境。

1. 連線到資料庫服務。

   ```bash
   mysql --host=127.0.0.1 --user='<database-username>' --pass='<user-password>' --database='<name>' --port='<port>'
   ```

1. 在 `MariaDB [main]>` 提示，卸除資料庫。

   Starter and Pro整合：

   ```shell
   drop database main;
   ```

   對於生產：

   ```shell
   drop database <cluster-id>;
   ```

   對於分段：

   ```shell
   drop database <cluster-ID_stg>;
   ```

1. 重新建立資料庫。

   Starter and Pro整合：

   ```shell
   create database main;
   ```

   為生產匯入：

   ```shell
   zcat <cluster-ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```

   匯入以進行分段：

   ```shell
   zcat <cluster-ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```
