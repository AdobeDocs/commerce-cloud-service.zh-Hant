---
title: 更新ECE工具套件
description: 瞭解如何升級ECE-Tools套件，以運用雲端基礎結構上套用至Adobe Commerce的最新修正和功能。
feature: Cloud, Upgrade
exl-id: 7cce45eb-ae53-4468-b16d-4f4d3422ac52
source-git-commit: 513bc5b52f046ffd98005d80f34725b7f60b38bd
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# 更新ECE工具套件

的更新 `ece-tools` 套件也會更新其他 [Commerce套件的Cloud Tools Suite](../release-notes/cloud-tools-suite.md)，為的相依性 `ece-tools`. Adobe Commerce因此，您必須在支援 `ece-tools` 封裝。

{{ece-tools-package}}

**必要條件**：

- 更新之前 `ece-tools`，檢閱 [Cloud Tools Suite for Commerce發行說明](../release-notes/cloud-tools-suite.md).
- 如果您正在從更新 `ece-tools` 2002.0.22或更早版本至2002.1.0，檢閱 [與舊版不相容的變更](../release-notes/backward-incompatible-changes.md) 並對雲端基礎結構專案中的Adobe Commerce進行任何必要的變更。
- 檢閱 [升級與修補程式](../development/commerce-version.md#upgrade-from-older-versions) 決定與雲端基礎結構專案上Adobe Commerce相容的ECE-Tools版本。

{{upgrade-tip}}

**若要更新 `ece-tools` 封裝**：

1. 在您的本機工作站上，使用Composer執行更新。

   ```bash
   composer update magento/ece-tools --with-dependencies
   ```

   >[!NOTE]
   >
   >如果您無法更新超過以下時間 `ece-tools` 2002.0.8版，請參閱 [升級專案以使用ECE-Tools套件](install-package.md).

1. 新增、提交和推送程式碼變更。

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update magento/ece-tools"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. 測試驗證後，將此分支合併至整合分支。
