---
title: 管理磁碟空間
description: 瞭解如何使用命令列介面管理磁碟空間。
feature: Cloud, Storage
exl-id: 480cb33b-ac83-441d-946e-5b4de09ad84e
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 0%

---

# 管理磁碟空間

您可以在雲端基礎結構合約和的Adobe Commerce中找到雲端專案的總儲存容量 [帳戶頁面](https://accounts.magento.cloud/user). 您帳戶中的每張專案卡片都會顯示 _環境_，則 _儲存_ 容量，以及 _使用者_. 或者，您可以使用以下雲端命令：

```bash
magento-cloud subscription:info | grep storage
```

範例回應：

```terminal
| storage              | 51200
```

當Pro生產或中繼環境達到或超過儲存容量的95%時，雲端基礎結構監控工具會觸發支援警報，通知您儲存容量會自動增加。

通知範例：

>[!BEGINSHADEBOX]

_「我們的監視偵測到叢集(project-id-environment)上的檔案儲存空間已接近滿載。 磁碟使用率目前處於關鍵使用率等級，剩餘不到1 GiB。 共用儲存磁碟區目前正在從60 GiB升級至70 GiB，以維持您的服務正常運作。 請檢視生產和中繼檔案的使用情況，以瞭解是否可以清除一些空間。」_

>[!ENDSHADEBOX]

>[!TIP]
>
>建議您定期監控儲存容量，並將其維持在90%以下，以避免自動增加。 配置完畢後，就無法還原Pro測試和生產的儲存空間增加。

## 檢查整合環境

您可以使用來檢查整合環境的磁碟空間使用量 `magento-cloud` CLI

**檢查約略的磁碟空間使用量**：

```bash
magento-cloud db:size
```

範例回應：

```terminal
Checking database service mysql...

+----------------+-----------------+--------+
| Allocated disk | Estimated usage | % used |
+----------------+-----------------+--------+
| 2.0 GiB        | 193.3 MiB       | ~ 9%   |
+----------------+-----------------+--------+
```

所有掛載都共用一個磁碟。 您可以使用來檢查裝載的磁碟空間使用量 `magento-cloud` CLI

**若要檢查掛載的約略磁碟空間使用量**：

```bash
magento-cloud mount:size
```

範例回應：

```terminal
Checking disk usage for all mounts on <project>-<environment>-mymagento@ssh.us.magento.cloud...

+------------+-----------+---------+-----------+-----------+--------+
| Mount(s)   | Size(s)   | Disk    | Used      | Available | % Used |
+------------+-----------+---------+-----------+-----------+--------+
| app/etc    | 184 KiB   | 1.9 GiB | 481.3 MiB | 1.4 GiB   | 24.7%  |
| pub/media  | 128 KiB   |         |           |           |        |
| pub/static | 158.2 MiB |         |           |           |        |
| var        | 316.7 MiB |         |           |           |        |
+------------+-----------+---------+-----------+-----------+--------+
```

## 檢查專用叢集

對於Pro測試環境和生產環境，您可以使用 `disk free` 指令，報告檔案系統使用的磁碟空間量。 您必須使用SSH登入遠端環境。

```bash
df -h
```

此 `-h` 選項會以人類看得懂的格式（KB、MB或GB）顯示報表。

在下列範例回應中， `/mnt/shared` 掛載顯示媒體與磁碟空間 `/data/mysql/` 掛載顯示資料庫的磁碟空間：

```terminal
Filesystem                                    Size  Used Avail Use% Mounted on
udev                                           16G     0   16G   0% /dev
tmpfs                                         3.2G  9.1M  3.2G   1% /run
/dev/xvda1                                     59G  8.9G   48G  16% /
tmpfs                                          16G   36K   16G   1% /dev/shm
tmpfs                                         5.0M     0  5.0M   0% /run/lock
tmpfs                                          16G     0   16G   0% /sys/fs/cgroup
/dev/xvdj                                     9.8G  2.3G  7.6G  23% /data/mysql
/dev/xvdi                                     9.8G  491M  9.3G   5% /data/exports
192.168.5.5:/shared                           9.8G  591M  9.3G   6% /mnt/shared
/dev/loop0                                     91M   91M     0 100% /app/project
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
192.168.5.5:/shared/project/app/etc     9.8G  591M  9.3G   6% /app/project/app/etc
192.168.5.5:/shared/project/pub/media   9.8G  591M  9.3G   6% /app/project/pub/media
192.168.5.5:/shared/project/pub/static  9.8G  591M  9.3G   6% /app/project/pub/static
```

您可以指定目錄來限制回應。 例如：

```bash
df -h var/
```

範例回應：

```terminal
Filesystem                                    Size  Used Avail Use% Mounted on
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
```

## 配置磁碟空間

兩個 [組態檔](../environment/overview.md) 控制雲端環境中的磁碟空間配置： `.magento.app.yaml` 檔案與 `.magento/services.yaml` 檔案。 每個檔案都包含 `disk` 屬性，定義個別設定的磁碟大小值（以MB為單位）。 您只能在Pro整合和Starter環境中變更磁碟空間配置。

>[!IMPORTANT]
>
>針對Pro生產和中繼環境，您必須 [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 以變更磁碟空間配置。 Pro生產與測試環境的大小增加只能在特定的間隔進行，因此，根據您目前的磁碟空間使用量，支援服務可能會建議將磁碟空間配置增加至少10 GB。 配置完畢後，就無法還原Pro測試和生產的儲存空間增加。

### 應用程式磁碟空間

此 `.magento.app.yaml` 檔案控制 [永久磁碟空間](../application/properties.md#disk) 可供應用程式使用。

**增加應用程式的磁碟空間**：

1. 在本機開發環境中，開啟 `.magento.app.yaml` 組態檔。

1. 為設定新值 `disk` 屬性（以MB為單位）。

   ```yaml
   disk: <value-mb>
   ```

1. 將變更儲存在檔案中。

1. 新增、提交和推送您的程式碼變更。

   ```bash
   git add .magento.app.yaml && git commit -m "Increase disk space for application" && git push origin <branch-name>
   ```

   將更新的YAML檔案推送到遠端環境後，變更就會生效。

### 服務磁碟空間

此 `.magento/services.yaml` 檔案控制每個服務可用的磁碟空間，例如MySQL和Redis。

**增加服務的磁碟空間**：

1. 在本機開發環境中，開啟 `.magento/services.yaml` 組態檔。

1. 在檔案中新增或尋找服務。 另請參閱 [進一步瞭解設定服務](../services/services-yaml.md).

1. 設定磁碟屬性的新值（以MB為單位）。

   ```yaml
   <name>:
       type: <service-name>:<service-version>
       disk: <value-mb>
   ```

1. 將變更儲存在檔案中。

1. 新增、提交和推送您的程式碼變更。

   ```bash
   git add .magento/services.yaml && git commit -m "Increase disk space for service" && git push origin <branch-name>
   ```

   將更新的YAML檔案推送到遠端環境後，變更就會生效。

## 監視磁碟空間

在Pro Production環境中，您可以使用New Relic的Adobe Commerce警示管理原則來監視磁碟空間和其他效能指標。 如需詳細資訊，請參閱 [使用受管理警示監控效能](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts). 如需進一步的指引，請參閱 [解決資料庫效能問題的最佳實務](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html).

## 無剩餘空間

組建快取會隨著時間而成長。 如果您收到警告指出 `No space left on device`，請嘗試清除組建快取並重新部署：

```bash
magento-cloud project:clear-build-cache
```
