---
title: 升級專案以使用ECE-Tools
description: 瞭解如何在雲端基礎結構專案上升級Adobe Commerce，以使用ECE-Tools套件並利用最新的修正和功能。
feature: Cloud, Install
exl-id: 820cca84-2817-4881-829f-ebb78400d8c7
source-git-commit: bcdb59f0d2a17e55e8b0479ee69fac06c710638f
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# 升級專案以使用ECE-Tools套件

Adobe已過時 `magento/magento-cloud-configuration` 和 `magento/ece-patches` 套件以支援 `ece-tools` 封裝，可簡化許多雲端程式。 如果您在雲端基礎結構專案上使用舊版的Adobe Commerce，可以 _非_ 包含 `ece-tools` 封裝，則您必須執行一次性的手動 _升級_ 處理至您的專案。

>[!WARNING]
>
>如果您的專案包含 `ece-tools` 封裝，您可以略過下列升級。 若要驗證，請擷取 [!DNL Commerce] 版本使用 `php vendor/bin/ece-tools -V` 命令於您的本機專案根目錄中。

此專案升級程式需要您更新 `magento/magento-cloud-metapackage` 中的版本限制 `composer.json` 根目錄下的檔案。 此限制可讓您更新雲端基礎結構中繼資料的Adobe Commerce （包括移除已棄用的套件），而不需升級您目前的Adobe Commerce版本。

{{upgrade-tip}}

## 移除已棄用的套件

執行升級前，請使用 `ece-tools` 封裝，檢查 `composer.lock` 下列已棄用套件的檔案：

- `magento/magento-cloud-configuration`
- `magento/ece-patches`

## 更新中繼資料

每個Adobe Commerce版本都需要不同的限制，基礎如下：

```terminal
>=current_version <next_version
```

- 的 `current_version`，指定要安裝的Adobe Commerce版本。
- 的 `next_version`，請在中指定的值後面指定下一個修補程式版本 `current_version`.

如果您想要安裝Adobe Commerce `2.3.5-p2`，設定 `current_version` 至 `2.3.5` 和 `next_version` 至 `2.3.6`. 限制 `">=2.3.5 <2.3.6"` 安裝2.3.5的最新可用套件。

您隨時可以在以下位置找到最新的中繼資料限制： [`magento-cloud` 範本](https://github.com/magento/magento-cloud/blob/master/composer.json).

下列範例會將雲端基礎結構中繼資料上Adobe Commerce的限制，設為大於或等於目前版本2.4.7且小於下一個版本2.4.8的任何版本：

```json
"require": {
    "magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
},
```

## 升級專案

若要升級您的專案以使用 `ece-tools` 封裝，您必須更新中繼封裝及 `.magento.app.yaml` 勾選屬性，然後執行Composer更新。

**若要升級專案以使用ece-tools**：

1. 更新 `magento/magento-cloud-metapackage` 中的版本限制 `composer.json` 檔案。

   ```bash
   composer require "magento/magento-cloud-metapackage":">=2.4.7 <2.4.8" --no-update
   ```

1. 更新中繼資料。

   ```bash
   composer update magento/magento-cloud-metapackage
   ```

1. 修改中的勾點指令 `magento.app.yaml` 檔案。

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. 檢查並移除 [已棄用的套件](#remove-deprecated-packages). 已棄用的套件可能會阻礙成功升級。

   ```bash
   composer remove magento/magento-cloud-configuration
   ```

   ```bash
   composer remove magento/ece-patches
   ```

1. 可能需要更新 `ece-tools` 封裝。

   ```bash
   composer update magento/ece-tools
   ```

1. 新增並認可程式碼變更。 在此範例中，已更新下列檔案：

   ```terminal
   .magento.app.yaml
   composer.json
   composer.lock
   ```

1. 將您的程式碼變更推送至遠端伺服器，並將此分支與 `integration` 分支。

   ```bash
   git push origin <branch-name>
   ```
