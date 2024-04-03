---
title: 環境變數
description: 請參閱雲端基礎結構上Adobe Commerce專屬的環境變數清單。
feature: Cloud, Build, Configuration, Deploy
exl-id: bfee2f69-93a6-4d26-bb9e-be8acc5673c3
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 環境變數

雲端基礎結構上的Adobe Commerce可讓您指派環境變數來覆寫設定選項。 此 `ece-tools` 套件會在 `env.php` 根據下列專案的值的檔案： [雲端變數](variables-cloud.md)，在中設定的變數 [!DNL Cloud Console]，以及 `.magento.env.yaml` 組態檔。

中的環境變數 `.magento.env.yaml` 檔案透過覆寫您現有的Commerce設定來自訂雲端環境。 若預設值為 `Not Set`，然後 `ece-tools` 封裝取用 **否** 動作並使用 [!DNL Commerce] 預設值或以下變數的值： `MAGENTO_CLOUD_RELATIONSHIPS` 設定。 若已設定預設值，則 `ece-tools` 封裝會設定該預設值。

環境變數的型別包括：

- [管理員](variables-admin.md) — 變數覆寫專案管理員變數
- [Magento_CLOUD](variables-cloud.md) — 雲端基礎結構的特定變數
- 中使用的變數 `.magento.env.yaml` 檔案：
   - [全域](variables-global.md) — 變數會影響建置、部署和部署後階段
   - [建置](variables-build.md) — 變數控制建置動作
   - [部署](variables-deploy.md) — 變數控制部署動作
   - [部署後](variables-post-deploy.md) — 變數控制部署後的動作

變數為 _階層式_，這表示如果變數未被覆寫，則會繼承自父環境。

您可以設定 [管理員變數](variables-admin.md) 從 [!DNL Cloud Console] 或使用Adobe Commerce CLI。 您可以從管理其他環境變數 [`.magento.env.yaml`](configure-env-yaml.md) 檔案來管理所有環境的建置和部署動作，包括Pro Staging和生產環境，不需要支援票證。

>[!TIP]
>
>YAML檔案區分大小寫，不允許使用索引標籤。 請留意在整個過程中使用一致的縮排 `.magento.env.yaml` 檔案或您的設定可能無法如預期運作。 本檔案和範例檔案中的範例使用 _雙空格鍵_ 縮排。 使用 [ece-tools validate指令](configure-env-yaml.md#validate-configuration-file) 以檢查您的設定。
