---
title: 『[!DNL ECE-Tools] 封裝
description: 瞭解 [!DNL ECE-Tools] 套件以及這對於管理和部署Adobe Commerce的協助方式。
exl-id: 5583a685-29c5-4de5-8d2e-94cff5ff37ab
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# ECE-Tools套件

此 [!DNL ECE-Tools] package是一組指令碼和工具，用來管理和部署 [!DNL Commerce] 應用程式。 此 `ece-tools` 套件簡化了許多流程，例如管理cron工作、驗證專案設定以及套用Adobe修補程式和修補程式。 您可以檢視並貢獻 [開放原始碼 [!DNL ECE-Tools] GitHub上的程式碼存放庫][ece-repo].

{{ece-tools-package}}

此 `ece-tools` 套件與Adobe Commerce相容（從2.1.4版開始），並包含雲端基礎結構命令上的指令碼和Adobe Commerce，旨在協助管理您的程式碼並自動建置和部署您的專案。

以下列出可用的 `ece-tools` 命令：

```bash
php ./vendor/bin/ece-tools list
```

## 建置和部署

此 `ece-tools` 此套件包含一些命令，用於在雲端基礎結構應用程式上執行建置、部署和部署後階段的Adobe Commerce啟動作業。 例如， `php ./vendor/bin/ece-tools build` 命令會開始應用程式建置流程。

依預設，這些 `ece-tools` 命令位於 [勾點屬性](../application/hooks-property.md) 的 `.magento.app.yaml` 組態檔。

## Docker配置生成器

此 `ece-tools` 套件包含下列專案的相依性 [magento/magento-cloud-docker] 套件，為Docker影像提供功能和設定檔案，以在雲端基礎結構上為Adobe Commerce啟動Docker開發環境。 您也可以以獨立套件的形式執行Cloud Docker for Commerce。 另請參閱 [Docker開發](../dev-tools/cloud-docker.md).

## 服務、路由和變數

您可以使用 `ece-tools` 套件，可顯示有關Base64編碼的詳細資訊 [雲端變數](../environment/variables-cloud.md) 用於任何雲端環境。 下列指令顯示所有服務、路由和變數。

```bash
php ./vendor/bin/ece-tools env:config:show
```

若要顯示特定資訊集，請使用下列格式：

```bash
php ./vendor/bin/ece-tools env:config:show <option>
```

- `services` — 顯示關係資料，來自 `MAGENTO_CLOUD_RELATIONSHIPS` 環境變數，定義於 `services.yaml` 檔案。
- `routes` — 顯示專案的已配置路由，使用 `MAGENTO_CLOUD_ROUTES` 環境變數。
- `variables` — 顯示專案的已設定變數，使用 `MAGENTO_CLOUD_VARIABLES` 環境變數。

的輸出範例 `services` 選項：

```terminal
Magento Cloud Services:
+-----------------------------------+----------------------------------+
| Service Configuration             | Value                            |
+-----------------------------------+----------------------------------+
| database:                                                            |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| password                          | <password>                       |
| port                              | 3306                             |
+-----------------------------------+----------------------------------+
| opensearch:                                                          |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| port                              | 9200                             |
...
```

## 驗證環境設定

有一組驗證指令可用來協助評估專案的組態。 另請參閱 [智慧型精靈](../deploy/smart-wizards.md) 在 _最佳化部署_ 區段，以瞭解每個精靈指令的詳細說明。 此 `wizard:ideal-state` 命令會在建置階段自動執行。 若要確認專案的理想狀態：

```bash
php ./vendor/bin/ece-tools wizard:ideal-state
```

>[!NOTE]
>
>您必須執行 `wizard:ideal-state` 命令來識別遠端雲端環境中的虛擬報表套裝。 命令一律會傳回 `The configured state is not ideal` 在本機開發環境中執行時發生錯誤。

範例輸出：

```terminal
Ideal state is configured
```

另請參閱 [ece-tools發行說明](../release-notes/cloud-tools-suite.md).

## Adobe修補程式和自訂修補程式

此 `ece-tools` 套件包含下列專案的相依性 [magento/magento-cloud-patches] 此套件提供Adobe修補程式和熱修正，可改善所有Adobe Commerce版本與雲端環境的整合，並支援快速傳送關鍵修正。 「 」也會提供您新增至雲端基礎結構專案Adobe Commerce的自訂修補程式。 另請參閱 [套用修補程式](../development/apply-patches.md).

<!-- link definitions -->

[ece-repo]: https://github.com/magento/ece-tools
[magento/magento-cloud-docker]: https://github.com/magento/magento-cloud-docker
[magento/magento-cloud-patches]: https://github.com/magento/magento-cloud-patches
