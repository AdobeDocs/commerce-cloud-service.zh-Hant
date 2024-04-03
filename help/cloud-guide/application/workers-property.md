---
title: 工作者
description: 瞭解如何在中設定worker屬性 [!DNL Commerce] 應用程式組態檔。
feature: Cloud, Configuration
exl-id: d6816925-5912-45ca-8255-6c307e58542d
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Workers屬性

您可以定義工作程式獨立於Web執行個體執行，而不需要執行中的Nginx執行個體；但是，工作程式使用的網路儲存空間與 [!DNL Commerce] 應用程式。 您不需要在背景工作執行個體上設定Web伺服器（使用Node.js或Go），因為路由器無法將公開要求導向背景工作。 這使得工作者執行個體非常適合用於背景工作或持續執行工作，這些工作可能會阻礙部署。

## 設定背景工作

背景工作僅適用於Pro預備和生產環境。 專業整合與入門環境可選擇使用 [CRON_CONSUMERS_RUNNER](../environment/variables-deploy.md#cron_consumers_runner) 變數中。

若要在Pro Staging或Production中設定背景工作， [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 並包含下列資訊：

- 專案ID
- 環境ID
- 工作者名稱
- 啟動命令

您可以為每個工作者設定一個處理序。 中的基本通用背景工作設定 `.magento.app.yaml` 檔案可能如下所示：

```yaml
workers:
    queue:
        commands:
            start: |
                php ./bin/magento queue:consumers:start commerce.eventing.event.publish
```

此範例會定義名為的單一背景工作 `queue`，具有小（大小S）的資源配置層級，並執行 `php ./bin/magento` 啟動時的命令。 工作者 `queue` 然後在每個節點上以工作者處理序的方式執行。 如果命令結束，就會自動重新啟動。

## 命令和覆寫

此 `commands.start` 需要使用金鑰才能啟動背景工作應用程式的命令。 您可以使用任何有效的shell命令，不過最好使用應用程式的語言。 如果指定的指令 `start` 索引鍵終止，它會自動重新啟動。

>[!IMPORTANT]
>
>此 `deploy` 和 `post_deploy` 勾點和 `crons` 命令只會在Web容器上執行，而不會在Worker執行個體中執行。

### 繼承

的定義 `size`， `relationships`， `access`， `disk` 和 `mount`、和 `variables` 屬性會由背景工作繼承，除非明確覆寫。

以下屬性最常用於覆寫 [頂層設定](properties.md)：

- `size` — 為單一背景程式分配較少的資源
- `variables` — 指示應用程式以不同方式執行

### 時間與佇列

雖然每個工作者佇列在彼此後面，但以下設定會在中產生一致的兩秒時間戳記 `var/time.txt` 檔案，不論PHP程式碼內是否8秒休眠：

```yaml
workers:
    time1:
        commands:
            start: 'php -r "sleep(8); echo time() . PHP_EOL;" >> var/time.txt& sleep 2'
```
