---
title: 設定Redis服務
description: 瞭解如何在雲端基礎結構上為Adobe Commerce設定及最佳化Redis做為後端快取解決方案。
feature: Cloud, Cache, Services
exl-id: d6971875-d302-495a-ad10-a81c507c2bc9
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# 設定Redis服務

[Redis](https://redis.io) 是選用的後端快取解決方案，可取代Adobe Commerce預設使用的Zend架構Zend_Cache_Backend_File。

另請參閱 [設定Redis](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/config-redis.html) 在 _設定指南_.

{{service-instruction}}

**啟用Redis**：

1. 將所需的名稱和型別新增到 `.magento/services.yaml` 檔案。

   ```yaml
   myredis:
       type: redis:<version>
   ```

   若要提供您自己的Redis設定，請新增 `core_config` 在您的網站中輸入金鑰 `.magento/services.yaml` 檔案：

   ```yaml
   cache:
       type: redis:<version>
   ```

1. 設定以下專案中的關係： `.magento.app.yaml` 檔案。

   ```yaml
   runtime:
       extensions:
           - redis
   
   relationships:
       redis: "redis:redis"
   ```

1. 新增、提交和推送您的程式碼變更。

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable redis service" && git push origin <branch-name>
   ```

1. [驗證服務關係](services-yaml.md#service-relationships).

{{service-change-tip}}

## 使用Redis CLI

假設您的Redis關係已命名 `redis`，您可使用 `redis-cli` 工具。

1. 使用SSH連線至已安裝並設定Redis的整合環境。

1. 開啟連線至主機的SSH通道。

   ```bash
   redis-cli -h redis.internal
   ```

## 取得已安裝的Redis版本

使用下列命令取得Redis版本安裝在整合環境中：

```bash
redis-cli -h redis.internal info | grep version
```

範例回應：

```terminal
redis_version:7.0.5
gcc_version:8.3.0
```

### Redis on Pro測試和生產

若要在中繼或生產環境中安裝Redis版本，請使用 `redis-server` 命令：

```bash
redis-server -v
```

```terminal
Redis server v=7.0.5 ...
```

使用下列命令取得Redis組態安裝在Pro Staging或生產環境中：

```bash
echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
```

範例回應：

```terminal
"redis" : [
    {
        "cluster" : "project-master-123abc4",
        "fragment" : null,
        "host" : "redis.internal",
        "host_mapped" : false,
        "hostname" : "oblahblahblahblahe.redis.service._.magentosite.cloud",
        "ip" : "169.254.10.10",
        "password" : null,
        "path" : null,
        "port" : 6379,
        "public" : false,
        "query" : {},
        "rel" : "redis",
        "scheme" : "redis",
        "service" : "redis",
        "type" : "redis:7.0.5",
        "username" : null
    }
]
```

## 疑難排解Redis

請參閱下列Adobe Commerce支援文章，以取得疑難排解Redis問題的說明：

- [Redis問題延遲Admin登入或結帳](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-issue-delay-magento-admin-login-or-checkout.html)
- [延伸的Redis快取實作Adobe Commerce 2.3.5+](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-service-configuration.html)
- [MDVA-30102：Redis快取已滿](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/v1-0-6/mdva-30102-magento-patch-redis-cache-getting-full.html)
- [Adobe Commerce上的受管理警報： Redis記憶體警告警報](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-warning-alert.html)
- [Adobe Commerce上的受管理警報：Redis記憶體嚴重警報](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-critical-alert.html)
- [Redis疑難排解員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-troubleshooter.html)
