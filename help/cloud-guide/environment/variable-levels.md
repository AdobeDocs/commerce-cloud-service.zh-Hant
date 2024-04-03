---
title: 變數層級和選項
description: 瞭解在雲端基礎結構專案執行階段環境中自訂Adobe Commerce時所使用的不同變數層級和選項。
feature: Cloud, Configuration, Security
exl-id: 11aa0862-94c0-47fb-946a-0148f75cc24c
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# 變數層級

專案變數適用於專案內的所有環境。 環境變數會套用至特定環境或分支。 環境 _繼承_ 變數定義。

您可以特別為環境定義變數，藉此覆寫繼承的值。 例如，若要設定開發所需的變數，請在 `.magento.env.yaml` 整合環境中的檔案。 所有從整合環境分支的環境都會繼承這些值。 另請參閱 [部署設定](configure-env-yaml.md) 以取得有關使用設定環境的詳細資訊 `.magento.env.yaml` 檔案。

>[!BEGINTABS]

>[!TAB CLI]

**若要使用Cloud CLI設定變數**：

- **專案特定變數** — 設定相同的值 _全部_ 您專案中的環境。 這些變數可在所有環境的建置和執行階段使用。

  ```bash
  magento-cloud variable:create --level project --name <variable-name> --value <variable-value>
  ```

- **環境特定變數** — 設定唯一值 _特定_ 環境。 這些變數可在執行階段使用，並由子環境繼承。 使用在命令中指定環境 `-e` 選項。

  ```bash
  magento-cloud variable:create --level environment --name <variable-name> --value <variable-value>
  ```

設定專案特定變數後，您必須手動重新部署遠端環境，變更才會生效。 推送新認可以觸發重新部署。

>[!TAB 主控台]

**若要使用設定變數[!DNL Cloud Console]**：

1. 在 _[!DNL Cloud Console]_，按一下專案導覽右側的設定圖示。

   ![設定專案](../../assets/icon-configure.png){width="36"}

1. 若要設定專案層級變數，請在 _專案設定_ 按一下 **變數**.

   ![專案變數](../../assets/ui-project-variables.png)

1. 若要設定環境層級變數，請在 _環境_ 清單，選取環境並按一下 **[!UICONTROL Variables]** 標籤。

   ![「環境變數」標籤](../../assets/ui-environment-variables.png)

1. 按一下 **[!UICONTROL Create variable]**.

1. 提供變數的名稱和值。 從下列選項中選擇：

   - 在執行階段期間可用
   - 可在建置期間使用
   - JSON值
   - 敏感變數（隱藏在主控台和CLI回應中的值）
   - 讓可繼承（子環境可繼承環境層級變數）

1. 按一下 **[!UICONTROL Create variable]**.

>[!CAUTION]
>
>在中設定環境專用變數 [!DNL Cloud Console] 自動重新部署環境。

>[!ENDTABS]

## 可見度

您可以使用來限制變數在建置或執行階段的可見度 `--visible-<build|runtime>` 命令。 此外，也有設定繼承和敏感度的選項。

使用下列選項來防止變數被看到或繼承：

- `--inheritable false` — 停用子環境的繼承。 這對於在「 」上設定僅限生產的值很有用 `master` 分支並允許所有其他環境使用相同名稱的專案層級變數。
- `--sensitive true` — 將變數標籤為 _無法讀取_ 在 [!DNL Cloud Console]. 您無法在使用者介面中檢視變數；不過，您可以從應用程式容器中檢視變數，就像任何其他變數一樣。

下列範例示範無法看見或繼承變數的特定案例。 您只能在CLI中指定這些選項。 此案例並非適用於所有可用的環境變數。

```bash
magento-cloud variable:create --name <variable-name> --value <variable-value> --inheritable false --sensitive true
```

## 驗證變數層級和值

您可以使用Cloud CLI檢視現有變數的清單。

```bash
magento-cloud variables
```

```terminal
Variables on the project Project-Name (<project-id>), environment <environment-name>:
+----------------------------+-------------+-------------------------------------------+
| Name                       | Level       | Value                                     |
+----------------------------+-------------+-------------------------------------------+
| env:COMPOSER_AUTH          | project     | {                                         |
|                            |             |    "http-basic": {                        |
|                            |             |       "repo.magento.com": {               |
|                            |             |       "username":                         |
|                            |             | "<public-key>",                           |
|                            |             |       "password":                         |
|                            |             | "<private-key>"                           |
|                            |             |     }                                     |
|                            |             |   }                                       |
|                            |             | }                                         |
| ADMIN_EMAIL                | project     | admin@123.com                             |
| ADMIN_EMAIL                | environment | admin@123.com                             |
| ADMIN_PASSWORD             | environment | password                                  |
| ADMIN_URL                  | environment | admin123                                  |
| ADMIN_USERNAME             | environment | admin                                     |
| php:newrelic.license       | environment | xxxx71fb030366182117f955a22e4baf8exxxxxx  |
+----------------------------+-------------+-------------------------------------------+
```
