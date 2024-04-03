---
title: 套用修補程式
description: 瞭解如何在雲端基礎結構專案上套用Adobe Commerce中的修補程式。
feature: Cloud, Upgrade
exl-id: a7bf672f-7b89-45cd-8436-e885bca9029d
source-git-commit: e67d3259b1b5195147e4e441fe9efd82e48241ab
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# 套用修補程式

[Commerce雲端修補程式](https://github.com/magento/magento-cloud-patches) 和 [品質修補工具](https://github.com/magento/quality-patches) 為已安裝的Adobe Commerce應用程式提供修補程式。

- Commerce雲端修補程式套件提供必要修補程式和關鍵修正
- 品質修補程式提供選購且低影響的品質修正，例如 [個別修補程式](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/versioning-policy.html#individual-patch) 不包含回溯不相容的變更

另請參閱 [可用的修補程式](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) 在 _Commerce Operations工具指南_ 以檢視已發行修補程式的完整清單。

這兩個套件都改善所有Adobe Commerce版本與雲端環境的整合，並支援快速傳送關鍵、選用和自訂修正。 您可以使用這些套裝軟體套用、還原和檢視有關Commerce可用的所有個別修補程式的一般資訊。

>[!TIP]
>
>您可以使用 [品質修補工具](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) 和Cloud Patches for Commerce作為Magento Open Source和Adobe Commerce專案的獨立套件。 我們建議針對非雲端專案使用品質修補工具。

將變更部署到遠端環境時， `ece-tools` 套件使用 `magento/magento-cloud-patches` 和 `magento/quality-patches` 若要檢查暫止的修補程式，並依照下列順序自動套用它們：

1. 套用Commerce雲端修補程式套件中包含的所有必要Commerce修補程式。
1. 套用「品質修補工具」中所選的Commerce修補程式。
1. 在中套用自訂修補程式 `/m2-hotfixes` 目錄，依修補程式名稱的字母順序。

>[!NOTE]
>
>當您更新 `ece-tools` package或Cloud Patches for Commerce套件，下次部署專案時會套用最新的必要修補程式，或者您可以使用 `ece-patches apply` CLI命令並重新部署您的雲端環境。 您無法略過 [必要的修補程式](https://github.com/magento/magento-cloud-patches/tree/develop/patches) 部署過程中。

## 必要條件

{{upgrade-tip}}

Quality Patches Tool依賴Commerce的雲端修補程式和 `ece-tools` 封裝。 若要套用最新的修補程式，您必須有 [最新版的ECE-Tools](../dev-tools/update-package.md) 已安裝。 ECE-Tools的最低要求版本為2002.1.2。

## 檢視可用的修補程式和狀態

若要檢視可用的個別修補程式清單：

```bash
php ./vendor/bin/ece-patches status
```

範例回應：

```terminal
More detailed information about patches you can find on https://support.magento.com/
╔════════════════╤═════════════════════════════════════════════════╤══════════╤═════════════╤═════════════════════════════════╗
║ Id             │ Title                                           │ Type     │ Status      │ Details                         ║
╠════════════════╪═════════════════════════════════════════════════╪══════════╪═════════════╪═════════════════════════════════╣
║ MAGECLOUD-5069 │ FPC is getting disabled during deployments      │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-page-cache    ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5650    │ Hold deployment config after reading from file  │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5684    │ Pagination Not working - product_list_limit=all │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-elasticsearch ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-65837       │ Fix load balancer issue                         │Deprecated│ Applied     │ Recommended replacement: MC-1   ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ BUNDLE-2554    │ Set Payment info bug                            │ Required │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - amzn/amazon-pay-module       ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-1           │ Fixes issue 1                                   │ Optional │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-2           │ Fixes issue 2                                   │ Optional │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-3           │ Fixes issue 3                                   │ Optional │ Not applied │ Required patches:               ║
║                │                                                 │          │             │  - MC-2                         ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ N/A            │ ../m2-hotfixes/MDVA_custom__2.3.5_ce.patch      │ Custom   │ N/A         │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-framework     ║
╚════════════════╧═════════════════════════════════════════════════╧══════════╧═════════════╧═════════════════════════════════╝
Magento 2 Enterprise Edition, version 2.3.5.0
```

狀態表格包含下列資訊型別：

- **型別**：
   - `Optional`—Adobe Commerce和Magento Open Source安裝可選擇使用「品質修補程式工具」和「雲端修補程式套件」的所有修補程式。 對於雲端基礎結構上的Adobe Commerce，所有修補程式均為選購。
   - `Required`—Cloud客戶需要Commerce適用的Cloud Patches套件中的所有修補程式。
   - `Deprecated` — 個別修補程式會標示為已棄用，若您已套用，建議您加以回覆。 回覆已棄用的修補程式後，該修補程式將不再顯示在狀態表格中。
   - `Custom` — 來自&#39;m2-hotfix&#39;目錄的所有修補程式。

- **狀態**：
   - `Applied` — 已套用修補程式。
   - `Not applied` — 尚未套用修補程式。
   - `N/A` — 由於衝突，無法定義修補程式的狀態。

- **詳細資料**：
   - `Affected components` — 受影響模組的清單。
   - `Required patches` — 所需的修補程式（相依性）清單。
   - `Recommended replacement` — 建議用來取代已棄用修補程式的修補程式。

## 在本機環境中套用修補程式

您可以在本機環境中手動套用修補程式，並在部署之前對其進行測試。

**在本機開發環境中套用個別修補程式**：

1. 將&#39;QUALITY_PATCH&#39;變數新增至 `.magento.env.yaml` 並列出底下所需的修補程式。

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

1. 從專案根目錄，套用修補程式。

   ```bash
   php ./vendor/bin/ece-patches apply
   ```

   此 `ece-patches apply` 指令會以下列順序套用修補程式：
   - 必要的修補程式
   - 選用的個別修補程式
   - 來自的自訂修補程式 `/m2-hotfixes` 目錄

1. 清除快取。

   ```bash
   php ./bin/magento cache:clean
   ```

1. 測試修補程式，對自訂修補程式進行任何必要的變更。

## 在遠端環境中套用修補程式

>[!WARNING]
>
>我們強烈建議先在整合或中繼環境中測試所有修補程式，再部署至生產環境。

**在遠端環境中套用修補程式**：

1. 新增 `QUALITY_PATCHES` 變數至 `.magento.env.yaml` 並列出底下所需的修補程式。

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

   >[!NOTE]
   >
   >升級至新版Adobe Commerce後，如果新版本未包含修補程式，您必須重新套用修補程式。

1. 新增、認可及推送已更新的 `.magento.env.yaml` 檔案。

   ```bash
   git add .magento.env.yaml
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

## 套用自訂修補程式

部署時，ECE-Tools會套用所有Adobe修補程式，以及您新增至的任何自訂修補程式 `/m2-hotfixes` 目錄。

>[!NOTE]
>
>所有修補程式檔案名稱都必須以 `.patch` 副檔名。

**若要在雲端環境中套用及測試自訂修補程式**：

1. 在專案根目錄中，建立名為的目錄 `m2-hotfixes` 如果它不存在

   ```bash
   mkdir m2-hotfixes
   ```

1. 將修補程式檔案複製到 `/m2-hotfixes` 目錄。

1. 新增、提交和推送程式碼變更。

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >請務必在預先生產環境中測試所有修補程式。 對於雲端基礎結構上的Adobe Commerce，您可以使用以下專案建立分支： `magento-cloud environment:branch <branch-name>` CLI命令。

## 還原自訂修補程式

若要還原或解除安裝先前套用的自訂修補程式：

1. 從刪除修補程式檔案 `/m2-hotfixes` 目錄。

1. 新增、提交和推送程式碼變更。

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Revert patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >請務必在生產前環境中測試。 對於雲端基礎結構上的Adobe Commerce，您可以使用以下專案建立分支： `magento-cloud environment:branch <branch-name>` CLI命令。

## 將修補程式套用至非雲端專案

使用 [品質修補工具](https://github.com/magento/quality-patches) 用於Magento Open Source和Adobe Commerce專案。

## 還原本機環境中的修補程式

您可以使用還原本機開發環境中先前套用的所有修補程式 `ece-patches` CLI

若要還原所有套用的修補程式：

```bash
php ./vendor/bin/ece-patches revert
```

這個指令會依照下列順序回覆所有修補程式：

- 還原從/m2-hotfixes目錄套用的所有自訂修補程式。
- 還原所有套用的選擇性個別修補程式。
- 還原所有套用的必要修補程式。

## 記錄

「品質修補程式」工具會將所有作業記錄到 `<Project_root>/var/log/patch.log` 檔案。
