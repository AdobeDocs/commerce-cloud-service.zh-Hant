---
title: Cloud Tools Suite發行說明
description: 瞭解適用於Adobe Commerce的Cloud Tools套裝的最新改善。
feature: Cloud, Release Notes
exl-id: 6a652e93-46a2-4590-97fc-fb5d114ece9a
source-git-commit: e04a9de8f0e31098f0cc2e47112f206c11a0e23b
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---

# Commerce Cloud Tools Suite發行說明

此發行資訊詳細說明適用於Commerce套件的Cloud Tools Suite最新改善，這些改善旨在部署和管理Cloud平台上的Adobe Commerce安裝和升級。

| 發行說明 | 版本 | 說明 | 來源 |
| ----------------- |-----------| ---------------------------------------- | --------------------------- |
| [`ece-tools` 封裝](ece-tools-package.md) | 2002.1.19 | 一組用來管理和部署雲端專案的指令碼和工具 | [`magento/ece-tools`](https://github.com/magento/ece-tools/tree/2002.1) |
| [Commerce雲端修補程式](cloud-patches.md) | 1.0.27 | 一組修補程式，可改善所有Adobe Commerce版本與雲端環境的整合。 此套件包含Adobe Commerce修補程式，以及您使用時套用的可用Hotfix `ece-tools` 待部署 | [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches/tree/1.0.1) |
| [Cloud Docker for Commerce](cloud-docker.md) | 1.3.7 | Docker映像將Adobe Commerce部署到本地雲端環境的功能和設定檔案 | [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker/tree/1.0) |
| [Commerce的雲端元件](cloud-components.md) | 1.0.14 | 針對部署在雲端基礎結構上的網站延伸Adobe Commerce核心功能 | [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components/tree/1.0.2) |

當您更新至ECE-Tools 2002.1.0或更新版本時，會自動更新至其他套件的最新版本，這些套件的相依性為 `ece-tools` 封裝。 另請參閱 [雲端中繼](../development/overview.md#cloud-metapackage) 以取得相依性清單。
