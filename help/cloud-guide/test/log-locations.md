---
title: 檢視和管理記錄檔
description: 瞭解雲端基礎結構中可用的記錄檔型別以及在何處可以找到它們。
last-substantial-update: 2023-05-23T00:00:00Z
exl-id: d7f63dab-23bf-4b95-b58c-3ef9b46979d4
source-git-commit: 86af69eed16e8fe464de93bd0f33cfbfd4ed8f49
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# 檢視和管理記錄檔

雲端基礎結構專案上的Adobe Commerce記錄有助於疑難排解以下相關問題 [建置和部署鉤點](../application/hooks-property.md)、雲端服務和Adobe Commerce應用程式。

您可以從檔案系統 [!DNL Cloud Console]，以及 `magento-cloud` CLI

- **檔案系統** — 此 `/var/log` 系統目錄包含所有環境的記錄。 此 `var/log/` 目錄包含特定環境專屬的應用程式特定記錄。 這些目錄不會在叢集中的節點之間共用。 在Pro生產和中繼環境中，您必須檢查每個節點上的記錄。

- **[!DNL Cloud Console]** — 您可以在環境中檢視建置、部署和部署後記錄資訊 _訊息_ 清單。

- **雲端CLI** — 您可以使用 `magento-cloud log` 命令或遠端環境記錄 `magento-cloud ssh` 命令。

## 記錄位置

系統記錄檔儲存在下列位置：

- 整合： `/var/log/<log-name>.log`
- 專業測試： `/var/log/platform/<project-ID>_stg/<log-name>.log`
- Pro Production： `/var/log/platform/<project-ID>/<log-name>.log`

的值 `<project-ID>` 視專案以及環境為預備還是生產而定。 例如，專案ID為 `yw1unoukjcawe`，中繼環境使用者為 `yw1unoukjcawe_stg` 而生產環境使用者為 `yw1unoukjcawe`.

使用該範例，部署記錄為： `/var/log/platform/yw1unoukjcawe_stg/deploy.log`

### 檢視遠端環境記錄

大部分的記錄檔都包含在遠端環境中發生的事件。 對於Pro，有多個節點，每個節點都有唯一的記錄。 使用下列專案檢視所有主機的清單：

```bash
magento-cloud ssh -p <project-ID> -e <environment-ID> --all
```

範例回應：

```terminal
1.ent-project-environment-id@ssh.region.magento.cloud
2.ent-project-environment-id@ssh.region.magento.cloud
3.ent-project-environment-id@ssh.region.magento.cloud
```

**若要檢視遠端環境記錄檔的清單**：

```bash
magento-cloud ssh -e <environment-ID> "ls var/log"
```

Pro的範例：

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "ls var/log | grep error"
```

**若要檢視遠端記錄檔**：

```bash
magento-cloud ssh -e <environment-ID> "cat var/log/cron.log"
```

Pro的範例：

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "cat var/log/cron.log"
```

>[!TIP]
>
>對於Pro Staging和生產環境，會針對具有固定檔案名稱的記錄檔啟用自動記錄旋轉、壓縮和移除。 每個記錄檔型別都有旋轉模式和存留期。 入門環境沒有記錄輪換。 有關環境的記錄輪換和壓縮記錄檔有效期的完整詳細資訊，請參閱： `/etc/logrotate.conf` 和 `/etc/logrotate.d/<various>`. 無法在Pro Integration環境中設定記錄旋轉。 針對Pro整合，您必須實作自訂解決方案/指令碼並 [設定您的cron](../application/crons-property.md) 以視需要執行指令碼。

## 建置和部署記錄檔

將變更推播到您的環境後，您可以從中的每個連結檢閱記錄 `var/log/cloud.log` 檔案。 記錄檔包含每個掛接的啟動和停止訊息。 在下列範例中，訊息為「`Starting post-deploy.`「和」`Post-deploy is complete.`&quot;

檢查記錄專案的時間戳記，驗證並尋找特定部署的記錄。 以下是可用於疑難排解的記錄輸出壓縮範例：

```terminal
Re-deploying environment project-integration-ID
  Executing post deploy hook for service `mymagento`
    [2019-01-03 19:44:11] NOTICE: Starting post-deploy.
    [2019-01-03 19:44:11] INFO: Validating configuration
    [2019-01-03 19:44:11] INFO: End of validation
    [2019-01-03 19:44:11] INFO: Enable cron
    [2019-01-03 19:44:11] INFO: Create backup of important files.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/env.php.bak for /app/app/etc/env.php was created.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/config.php.bak for /app/app/etc/config.php was created.
    [2019-01-03 19:44:11] INFO: php ./bin/magento cache:flush --ansi --no-interaction
    [2019-01-03 19:44:32] INFO: Warming up failed: http://integration-id-project.us.magentosite.cloud/
    [2019-01-03 19:44:32] NOTICE: Post-deploy is complete.
```

>[!TIP]
>
>當您設定雲端環境時，可以設定 [記錄檔Slack和電子郵件通知](../environment/set-up-notifications.md) 用於建置和部署動作。

以下記錄檔擁有所有雲端專案的共同位置：

- **部署記錄**： `var/log/cloud.log`
- **上次部署錯誤記錄**： `var/log/cloud.error.log`
- **偵錯記錄**： `var/log/debug.log`
- **例外狀況記錄**： `var/log/exception.log`
- **系統記錄**： `var/log/system.log`
- **支援記錄**： `var/log/support_report.log`
- **報表**： `var/report/`

透過 `cloud.log` 檔案包含來自部署流程每個階段的回饋，部署勾點建立的記錄對每個環境都是獨一無二的。 環境特定的部署記錄位於以下目錄中：

- **Starter and Pro整合**： `/var/log/deploy.log`
- **Pro Staging**： `/var/log/platform/<project-ID>_stg/deploy.log`
- **Pro Production**： `/var/log/platform/<project-ID>/deploy.log`

### 部署記錄

每個部署的記錄會串連至特定的 `deploy.log` 檔案。 以下範例會列印終端機中目前環境的部署記錄：

```bash
magento-cloud log -e <environment-ID> deploy
```

範例回應：

```terminal
Reading log file projectID-branchname-ID--mymagento@ssh.zone.magento.cloud:/var/log/'deploy.log'

[2023-04-24 18:58:03.080678] Launching command 'b'php ./vendor/bin/ece-tools run scenario/deploy.xml\n''.

[2023-04-24T18:58:04.129888+00:00] INFO: Starting scenario(s): scenario/deploy.xml (magento/ece-tools version: 2002.1.14, magento/magento2-base version: 2.4.6)
[2023-04-24T18:58:04.364714+00:00] NOTICE: Starting pre-deploy.
...
```

{{scd-timing-warning}}

### 錯誤記錄

在部署過程中產生的錯誤和警告訊息會同時寫入 `var/log/cloud.log` 和 `var/log/cloud.error.log` 檔案。 雲端錯誤記錄檔僅包含來自最新部署的錯誤和警告。 空白檔案表示部署成功且沒有錯誤。

您可以使用來檢視記錄檔 [雲端CLI SSH](#view-remote-environment-logs)，您也可以使用ECE工具來顯示有建議的錯誤：

```bash
magento-cloud ssh -e <environment-ID> "./vendor/bin/ece-tools error:show"
```

範例回應：

```terminal
errorCode: 1001
stage: build
step: validate-config
suggestion: Please run the following commands:
1. bin/magento module:enable --all
2. git add -f app/etc/config.php
3. git commit -m 'Adding config.php'
4. git push
title: File app/etc/config.php does not exist
type: warning
---------------

errorCode: 1006
stage: build
step: validate-config
suggestion: Your application does not have the "post_deploy" hook enabled.
  In order to minimize downtime, add the following to ".magento.app.yaml":
  hooks:
      post_deploy: |
          php ./vendor/bin/ece-tools run scenario/post-deploy.xml
title: The configured state is not ideal
type: warning
```

大多數錯誤訊息都包含說明和建議的動作。 使用 [ECE-Tools的錯誤訊息參考](../dev-tools/error-reference.md) 以查閱錯誤碼以取得進一步指引。 如需進一步的指引，請使用 [Adobe Commerce部署疑難排解員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html).

## 應用程式記錄

與部署記錄檔類似，應用程式記錄檔對每個環境都是獨一無二的：

| 記錄檔 | Starter與Pro整合 | 說明 |
| ------------------- | --------------------------- | ------------------------------------------------- |
| **部署記錄** | `/var/log/deploy.log` | 來自的活動 [部署勾點](../application/hooks-property.md). |
| **部署後記錄** | `/var/log/post_deploy.log` | 來自的活動 [部署後勾點](../application/hooks-property.md). |
| **Cron記錄** | `/var/log/cron.log` | cron作業的輸出。 |
| **Nginx存取記錄** | `/var/log/access.log` | 在Nginx啟動時，遺失目錄和排除的檔案型別會出現HTTP錯誤。 |
| **Nginx錯誤記錄** | `/var/log/error.log` | 啟動訊息有助於偵錯與Nginx相關的設定錯誤。 |
| **PHP存取記錄** | `/var/log/php.access.log` | 對PHP服務的請求。 |
| **PHP FPM記錄** | `/var/log/app.log` | |

對於Pro測試環境和生產環境，部署、部署後和Cron記錄僅可在叢集中的第一個節點上使用：

| 記錄檔 | Pro Staging | Pro Production |
| ------------------- | --------------------------------------------------- | ----------------------------------------------- |
| **部署記錄** | 僅第一個節點：<br>`/var/log/platform/<project-ID>_stg/deploy.log` | 僅第一個節點：<br>`/var/log/platform/<project-ID>/deploy.log` |
| **部署後記錄** | 僅第一個節點：<br>`/var/log/platform/<project-ID>_stg/post_deploy.log` | 僅第一個節點：<br>`/var/log/platform/<project-ID>/post_deploy.log` |
| **Cron記錄** | 僅第一個節點：<br>`/var/log/platform/<project-ID>_stg/cron.log` | 僅第一個節點：<br>`/var/log/platform/<project-ID>/cron.log` |
| **Nginx存取記錄** | `/var/log/platform/<project-ID>_stg/access.log` | `/var/log/platform/<project-ID>/access.log` |
| **Nginx錯誤記錄** | `/var/log/platform/<project-ID>_stg/error.log` | `/var/log/platform/<project-ID>/error.log` |
| **PHP存取記錄** | `/var/log/platform/<project-ID>_stg/php.access.log` | `/var/log/platform/<project-ID>/php.access.log` |
| **PHP FPM記錄** | `/var/log/platform/<project-ID>_stg/php5-fpm.log` | `/var/log/platform/<project-ID>/php5-fpm.log` |

### 存檔的記錄檔

應用程式記錄檔每天會壓縮並封存一次，並保留一年。 壓縮記錄檔的命名方式為使用唯一ID，對應至 `Number of Days Ago + 1`. 例如，在Pro生產環境中，過去21天的PHP存取記錄會儲存起來，並命名如下：

```terminal
/var/log/platform/<project-ID>/php.access.log.22.gz
```

存檔日誌檔一律儲存在壓縮前原始檔案所在的目錄中。

>[!NOTE]
>
>**部署** 和 **部署後** 記錄檔不會輪換和封存。 整個部署歷史記錄會寫入這些記錄檔中。

## 服務記錄

由於每個服務都在個別的容器中執行，因此整合環境中無法使用服務記錄檔。 雲端基礎結構上的Adobe Commerce僅提供對整合環境中Web伺服器容器的存取權。 以下服務記錄位置適用於Pro生產和中繼環境：

- **Redis記錄**： `/var/log/platform/<project-ID>_stg/redis-server-<project-ID>_stg.log`
- **Elasticsearch記錄**： `/var/log/elasticsearch/elasticsearch.log`
- **Java記憶體回收記錄**： `/var/log/elasticsearch/gc.log`
- **郵件記錄**： `/var/log/mail.log`
- **MySQL錯誤記錄**： `/var/log/mysql/mysql-error.log`
- **MySQL慢速記錄**： `/var/log/mysql/mysql-slow.log`
- **RabbitMQ記錄**： `/var/log/rabbitmq/rabbit@host1.log`

系統會根據記錄型別，將服務記錄封存及儲存不同的時段。 例如，MySQL記錄檔的存留期最短–7天後移除。

>[!TIP]
>
>縮放架構中的記錄檔位置取決於節點型別。 另請參閱 [在縮放的架構中記錄位置](../architecture/scaled-architecture.md#log-locations) 主題。

## 記錄Pro生產和測試所需的資料

在Pro生產和中繼環境中，使用 [New Relic記錄管理](../monitor/log-management.md) 與您的專案整合，以管理與雲端基礎結構專案上Adobe Commerce相關聯的所有記錄檔的彙總記錄檔資料。

New Relic記錄檔應用程式提供集中式記錄檔管理控制面板，用於疑難排解及監控雲端基礎結構生產和中繼環境上的Adobe Commerce。 控制面板還提供對Fastly CDN、影像最佳化和Web應用程式防火牆(WAF)服務的記錄資料存取。 另請參閱 [New Relic服務](../monitor/new-relic-service.md).
