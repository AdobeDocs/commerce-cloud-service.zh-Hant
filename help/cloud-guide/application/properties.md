---
title: 屬性
description: 設定時，請使用屬性清單作為參考 [!DNL Commerce] 用於建置和部署至雲端基礎建設的應用程式。
feature: Cloud, Configuration, Build, Deploy, Roles/Permissions, Storage
exl-id: 58a86136-a9f9-4519-af27-2f8fa4018038
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# 應用程式設定的屬性

此 `.magento.app.yaml` 檔案使用屬性來管理環境支援 [!DNL Commerce] 應用程式。

| 名稱 | 說明 | 預設 | 必填 |
| ------ | --------------------------------- | ------- | -------- |
| [`access`](#access) | 自訂使用者角色 | — | 否 |
| [`crons`](crons-property.md) | 更新規格並排程cron工作 | — | 否 |
| [`dependencies`](#dependencies) | 啟用其他相依性 | `php:composer/composer: '2.2.4'` | 否 |
| [`disk`](#disk) | 定義永續性磁碟大小 | `5120` | 是 |
| [`firewall`](firewall-property.md) | （僅限入門者）控制傳出流量 | — | 否 |
| [`hooks`](hooks-property.md) | 自訂建置、部署和部署後階段的殼層命令 | — | 否 |
| [`mounts`](#mounts) | 設定路徑 | 路徑：<ul><li>`"var": "shared:files/var"`</li><li>`"app/etc": "shared:files/etc"`</li><li>`"pub/media": "shared:files/media"`</li><li>`"pub/static": "shared:files/static"`</li></ul> | 否 |
| [`name`](#name) | 定義應用程式名稱 | `mymagento` | 是 |
| [`relationships`](#relationships) | 對應服務 | 服務：<ul><li>`database: "mysql:mysql"`</li><li>`redis: "redis:redis"`</li><li>`opensearch: "opensearch:opensearch"`</li></ul> | 否 |
| [`runtime`](#runtime) | 執行階段屬性包含 [!DNL Commerce] 應用程式。 | 擴充功能：<ul><li>`xsl`</li><li>`newrelic`</li><li>`sodium`</li></ul> | 是 |
| [`type`](#type-and-build) | 設定基本容器影像 | `php:8.1` | 是 |
| [`variables`](variables-property.md) | 為特定Commerce版本套用環境變數 | — | 否 |
| [`web`](web-property.md) | 處理外部請求 | — | 是 |
| [`workers`](workers-property.md) | 處理外部請求 | — | 是（如果未使用Web屬性） |

{style="table-layout:auto"}

## `name`

此 `name` 屬性提供在 [`routes.yaml`](../routes/routes-yaml.md) 檔案定義HTTP上游(預設為 `mymagento:http`)。 例如，如果 `name` 是 `app`，您必須使用 `app:http` 在上游欄位中。

>[!WARNING]
>
>部署應用程式後，請勿變更其名稱。 這麼做會導致資料遺失。

## `type` 和 `build`

此 `type`  和 `build` 屬性會提供基本容器影像的相關資訊，以建置和執行專案。

支援的 `type` 語言是PHP。 請依照以下步驟指定PHP版本：

```yaml
type: php:<version>
```

此 `build` 屬性會決定建立專案時預設執行的動作。 此 `flavor` 指定要執行的預設組建工作集。 下列範例顯示預設設定 `type` 和 `build` 從 `magento-cloud/.magento.app.yaml`：

```yaml
# The toolstack used to build the application.
type: php:8.1
build:
    flavor: none

dependencies:
    php:
        composer/composer: '2.2.4'
```

### 安裝和使用Composer 2

此 `build: flavor:` 屬性不用於Composer 2.x；因此，您必須在建置階段手動安裝Composer。 若要在Starter和Pro專案中安裝及使用Composer 2.x，您必須對進行三項變更 `.magento.app.yaml` 設定：

1. 移除 `composer` 作為 `build: flavor:` 並新增 `none`. 這項變更導致Cloud無法使用預設的1.x Composer版本來執行組建工作。
1. 新增 `composer/composer: '^2.0'` as a `php` 安裝Composer 2.x的相依性。
1. 新增 `composer` 將任務建置到 `build` 勾選以使用Composer 2.x執行建置工作。

在自己中使用以下設定片段 `.magento.app.yaml` 設定：

```yaml
# 1. Change flavor to none.
build:
    flavor: none

# 2. Add Composer ^2.0 as a php dependency.
dependencies:
    php:
        composer/composer: '^2.0'

# 3. Add a build hook to run the build tasks using Composer 2.x.
hooks:
    build: |
        set -e
        composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
```

另請參閱 [必要的套件](../development/overview.md#required-packages) 以取得有關Composer的詳細資訊。

## `dependencies`

指定您的應用程式在建置流程中可能需要的相關性。

Adobe Commerce支援下列語言的相依性：

- PHP
- 拼音
- Node.js

這些相依性與應用程式的最終相依性無關，並且可在以下位置找到： `PATH`，會在建置程式期間和應用程式的執行階段環境中進行。

您可以依照以下方式指定這些相依性：

```yaml
ruby:
   sass: "~3.4"
nodejs:
   grunt-cli: "~0.3"
```

## `runtime`

使用在執行階段修改PHP組態，例如啟用擴充功能。 需要下列擴充功能：

```yaml
runtime:
    extensions:
        - xsl
        - newrelic
        - sodium
```

另請參閱 [PHP設定](php-settings.md) 以取得啟用擴充功能的詳細資訊。

## `disk`

定義應用程式的永續性磁碟大小。

```yaml
disk: 5120
```

建議的磁碟大小下限為256 MB。 如果您看到錯誤 `UserError: Error building the project: Disk size may not be smaller than 128MB`，將大小增加到256 MB。

>[!NOTE]
>
>對於Pro測試和生產環境，您必須 [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 更新 `mounts` 和 `disk` 應用程式的設定。 當您提交票證時，請指出所需的設定變更，並包含更新版本的 `.magento.app.yaml` 檔案。

## `relationships`

定義應用程式中的服務對應。

關係 `name` 可供應用程式使用 `MAGENTO_CLOUD_RELATIONSHIPS` 環境變數。 此 `<service-name>:<endpoint-name>` 關係對應至中定義的名稱和型別值 `.magento/services.yaml` 檔案。

```yaml
relationships:
    <name>: "<service-name>:<endpoint-name>"
```

以下是預設關係的範例：

```yaml
relationships:
    database: "mysql:mysql"
    redis: "redis:redis"
    opensearch: "opensearch:opensearch"
    rabbitmq: "rabbitmq:rabbitmq"
```

另請參閱 [服務](../services/services-yaml.md) 以取得目前支援的服務型別和端點的完整清單。

## `mounts`

其索引鍵是相對於應用程式根目錄的路徑的物件。 掛載是磁碟上檔案的可寫入區域。 以下是在中設定的預設掛載清單 `magento.app.yaml` 檔案使用 `volume_id[/subpath]` 語法：

```yaml
 # The mounts that will be performed when the package is deployed.
mounts:
    "var": "shared:files/var"
    "app/etc": "shared:files/etc"
    "pub/media": "shared:files/media"
    "pub/static": "shared:files/static"
```

將掛載新增至此清單的格式如下：

```bash
"/public/sites/default/files": "shared:files/files"
```

- `shared` — 在環境中的應用程式之間共用磁碟區。
- `disk` — 定義共用磁碟區可用的大小。

>[!NOTE]
>
>對於Pro測試和生產環境，您必須 [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 更新 `mounts` 和 `disk` 應用程式的設定。 當您提交票證時，請指出所需的設定變更，並包含更新版本的 `.magento.app.yaml` 檔案。

您可以將掛載網頁新增至 [`web`](web-property.md) 位置區塊。

>[!WARNING]
>
>一旦您的網站擁有資料，請勿變更 `subpath` 裝載名稱的一部分。 此值是的唯一識別碼， `files` 區域。 如果您變更此名稱，將會遺失所有儲存在舊位置的網站資料。

## `access`

此 `access` 屬性指出最低使用者角色層級，可允許對環境進行SSH存取。 可用的使用者角色包括：

- `admin` — 可以在環境中變更設定並執行動作；具有 _投稿人_ 和 _檢視者_ 權利。
- `contributor` — 可以將程式碼推送至此環境，並從環境分支；具有 _檢視者_ 權利。
- `viewer` — 只能檢視環境。

預設的使用者角色為 `contributor`，會限制僅具有的使用者的SSH存取 _檢視者_ 權利。 您可以將使用者角色變更為 `viewer` 僅允許具有的使用者使用SSH存取 _檢視者_ 權利：

```yaml
access:
    ssh: viewer
```
