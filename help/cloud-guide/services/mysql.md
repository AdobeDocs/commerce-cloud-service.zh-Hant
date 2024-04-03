---
title: 設定MySQL服務
description: 瞭解如何在雲端基礎結構上使用Adobe Commerce管理用於永久資料儲存的MySQL服務。
feature: Cloud, Services, Storage
exl-id: 70820d00-8b82-4b60-87e4-ea98fd7ffcb2
source-git-commit: 9be8d1e062ab3dba86bc4d9c9ee8b8ece33d5b75
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# 設定MySQL服務

此 `mysql` 服務提供永久資料儲存，依據為 [MariaDB](https://mariadb.com/) 10.2至10.4版，支援 [XtraDB](https://docs.percona.com/percona-xtradb-cluster/8.0/index.html) 儲存引擎並重新實作MySQL 5.6和5.7的功能。

與其他MariaDB或MySQL版本相比，在MariaDB 10.4上重新索引需要更多時間。 另請參閱 [索引子](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html#indexers) 在 _效能最佳實務_ 指南。

>[!WARNING]
>
>將MariaDB從10.1版升級至10.2版時請務必小心。MariaDB 10.1是支援的最新版本 _XtraDB_ 做為儲存引擎。 MariaDB 10.2使用 _InnoDB_ 用於儲存引擎。 從10.1升級至10.2後，您無法復原變更。 Adobe Commerce同時支援兩種儲存引擎；不過，您必須檢查擴充功能及專案使用的其他系統，以確保其與MariaDB 10.2相容。另請參閱 [10.1和10.2之間的不相容變更](https://mariadb.com/kb/en/upgrading-from-mariadb-101-to-mariadb-102/#incompatible-changes-between-101-and-102).

{{service-instruction}}

**啟用MySQL**：

1. 將所需的名稱、型別和磁碟值（以MB為單位）新增至 `.magento/services.yaml` 檔案。

   ```yaml
   mysql:
       type: mysql:<version>
       disk: 5120
   ```

   >[!TIP]
   >
   >MySQL錯誤，例如 `PDO Exception: MySQL server has gone away`，可能是磁碟空間不足所造成。 確認您已為中的服務配置足夠的磁碟空間 [`.magento/services.yaml`](services-yaml.md#disk) 檔案。

1. 設定以下專案中的關係： `.magento.app.yaml` 檔案。

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

1. 新增、提交和推送您的程式碼變更。

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable mysql service" && git push origin <branch-name>
   ```

1. [驗證服務關係](services-yaml.md#service-relationships).

{{service-change-tip}}

## 設定MySQL資料庫

設定MySQL資料庫時，有以下選項：

- **`schemas`** — 綱要定義資料庫。 預設結構描述為 `main` 資料庫。
- **`endpoints`** — 每個端點代表具有特定許可權的認證。 預設端點為 `mysql`，具有 `admin` 存取 `main` 資料庫。
- **`properties`** — 屬性用於定義其他資料庫組態。

以下為中的基本設定範例 `.magento/services.yaml` 檔案：

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

此 `properties` 在上述範例中，修改預設值 `optimizer` 設定為 [效能最佳實務指南中的建議](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html#indexers).

**MariaDB設定選項**：

| 選項 | 說明 | 預設值 |
| -------------------- | --------------------------------------------------- | ------------------ |
| `default_charset` | 預設字元集。 | utf8mb4 |
| `default_collation` | 預設定序。 | utf8mb4_unicode_ci |
| `max_allowed_packet` | 封包大小上限（以MB為單位）。 Range `1` 至 `100`. | 16 |
| `optimizer_switch` | 設定查詢最佳化程式的值。 另請參閱 [MariaDB檔案](https://mariadb.com/kb/en/server-system-variables/#optimizer_switch). | |
| `optimizer_use_condition_selectivity` | 選取最佳化處理程式使用的統計資料。 Range `1` 至 `5`. 另請參閱 [MariaDB檔案](https://mariadb.com/kb/en/server-system-variables/#optimizer_use_condition_selectivity). | 10.4及更新版本為4 |

### 設定多個資料庫使用者

您可以選擇設定多個具有不同許可權的使用者來存取 `main` 資料庫。

依預設，有一個端點命名為 `mysql` 具有資料庫管理員存取權的使用者。 若要設定多個資料庫使用者，您必須在 `services.yaml` 檔案並在中宣告關係 `.magento.app.yaml` 檔案。 對於Pro測試和生產環境， [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 以請求其他使用者。

使用巢狀陣列來定義特定使用者存取的端點。 每個端點可以指定一個或多個結構描述（資料庫）的存取權，以及每個結構描述的不同許可權層級。

有效的許可權層級為：

- `ro`：僅允許SELECT查詢。
- `rw`：允許SELECT查詢和INSERT、UPDATE和DELETE查詢。
- `admin`：允許所有查詢，包括DDL查詢（CREATE TABLE、DROP TABLE等）。

例如：

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        schemas:
            - main
        endpoints:
            admin:
                default_schema: main
                privileges:
                    main: admin
            reporter:
                privileges:
                    main: ro
            importer:
                privileges:
                    main: rw
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

在上述範例中， `admin` 端點提供管理員層級的存取權， `main` 資料庫， `reporter` 端點提供唯讀存取權，以及 `importer` 端點提供讀寫存取權，這表示：

- 此 `admin` 使用者可完全控制資料庫。
- 此 `reporter` 使用者只有SELECT許可權。
- 此 `importer` 使用者具有SELECT、INSERT、UPDATE和DELETE許可權。

將上例中定義的端點新增至 `relationships` 的屬性 `.magento.app.yaml` 檔案。 例如：

```yaml
relationships:
    database: "mysql:admin"
    databasereporter: "mysql:reporter"
    databaseimporter: "mysql:importer"
```

>[!NOTE]
>
>如果您設定一個MySQL使用者，則無法使用 [`DEFINER`](https://dev.mysql.com/doc/refman/8.0/en/show-grants.html) 預存程式和檢視的存取控制機制。

## 連線到資料庫

直接存取MariaDB資料庫需要您使用SSH登入遠端雲端環境，並連線至資料庫。

1. 使用SSH登入遠端環境。

   ```bash
   magento-cloud ssh
   ```

1. 從擷取MySQL登入認證 `database` 和 `type` 中的屬性 [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) 變數中。

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   或

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   在回應中，尋找MySQL資訊。 例如：

   ```json
   "database" : [
      {
         "password" : "",
         "rel" : "mysql",
         "hostname" : "nnnnnnnn.mysql.service._.magentosite.cloud",
         "service" : "mysql",
         "host" : "database.internal",
         "ip" : "###.###.###.###",
         "port" : 3306,
         "path" : "main",
         "cluster" : "projectid-integration-id",
         "query" : {
            "is_master" : true
         },
         "type" : "mysql:10.3",
         "username" : "user",
         "scheme" : "mysql"
      }
   ],
   ```

1. 連線到資料庫。

   - 首先，使用以下命令：

     ```bash
     mysql -h database.internal -u <username>
     ```

   - 對於Pro，請使用下列指令，其中主機名稱、連線埠號碼、使用者名稱和密碼擷取自 `$MAGENTO_CLOUD_RELATIONSHIPS` 變數中。

     ```bash
     mysql -h <hostname> -P <number> -u <username> -p'<password>'
     ```

>[!TIP]
>
>您可以使用 `magento-cloud db:sql` 命令以連線到遠端資料庫並執行SQL命令。

## 連線到次要資料庫

>[!IMPORTANT]
>
>此功能僅適用於Pro Production和Staging叢集。

有時候，您必須連線到次要資料庫，以改善資料庫效能或解決資料庫鎖定問題。 如果需要此設定，請使用 `"port" : 3304` 以建立連線。 請參閱 [設定MySQL從屬連線的最佳實務](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration.html) 中的主題 _實作最佳實務_ 指南。

## 疑難排解

請參閱下列Adobe Commerce支援文章，以取得MySQL問題疑難排解的說明：

- [正在檢查緩慢的查詢和處理MySQL](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/database/checking-slow-queries-and-processes-mysql.html)
- [在雲端上建立資料庫傾印](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html)
- [資料移轉工具疑難排解](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-migration-tool-troubleshooting.html)
- [Adobe Commerce升級：壓縮至動態表格2.2.x、2.3.x至2.4.x](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/commerce-235-upgrade-prerequisites-mariadb.html)
