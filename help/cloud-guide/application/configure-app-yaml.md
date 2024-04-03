---
title: 設定應用程式部署
description: 瞭解如何在應用程式設定檔案中設定屬性，以控制 [!DNL Commerce] 應用程式會建置並部署到雲端環境。
feature: Cloud, Configuration, Build, Deploy
exl-id: 900da20d-98d2-4c9f-97ec-578aee775b55
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# 設定應用程式部署

此 `.magento.app.yaml` 檔案會控制應用程式建置和部署的方式。 雖然雲端基礎結構上的Adobe Commerce支援每個專案使用多個應用程式，但通常一個專案有一個應用程式具有 `.magento.app.yaml` 存放庫根目錄下的檔案。

此 `.magento.app.yaml` 有許多預設值，請參閱 [範例 `.magento.app.yaml` 檔案](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). 一律檢閱 `.magento.app.yaml` 已安裝的版本。 此檔案在雲端基礎結構版本上可能因Adobe Commerce而異。

使用 `.magento.app.yaml` 檔案來定義下列組態值：

- [屬性](properties.md) — 定義應用程式例項的屬性值。
- [變數屬性](variables-property.md) — 檢閱所需的環境變數 [!DNL Commerce] 應用程式版本。
- [PHP設定](php-settings.md) — 配置執行階段PHP選項。
- [設定靜態檔案的快取](set-cache.md) — 設定媒體和靜態檔案的快取TTL。
