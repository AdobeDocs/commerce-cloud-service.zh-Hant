---
source-git-commit: c160be020d855983eaf7a06d04cee6e27819b2a0
workflow-type: tm+mt
source-wordcount: '21467'
ht-degree: 0%

---
# magento-cloud (雲端基礎結構上的Adobe Commerce)

<!-- The template to render with above values -->
**版本**： 1.46.1

此參考包含119個指令，這些指令可透過 `magento-cloud` 命令列工具。
初始清單會使用 `magento-cloud list` 在雲端基礎結構上的Adobe Commerce執行命令。

>[!NOTE]
>
>此參考是從應用程式程式碼基底產生的。 若要變更內容，您可以更新中對應命令實施的原始碼 [程式碼基底](https://github.com/magento/magento-cloud-cli) 存放庫並提交您的變更以供檢閱。 另一種方式是 _提供意見反應_ （尋找右上方的連結）。 如需貢獻准則，請參閱 [程式碼協助撰寫](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `clear-cache`

清除CLI快取

```bash
magento-cloud cc
```

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `decode`

解碼編碼字串，例如MAGENTO_CLOUD_VARIABLES

```bash
magento-cloud decode [-P|--property PROPERTY] [--] <value>
```


### `value`

要解碼的變數值

- 必填

### `--property`， `-P`

要在變數中檢視的屬性

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `docs`

開啟線上檔案

```bash
magento-cloud docs [--browser BROWSER] [--pipe] [--] [<search>]...
```


### `search`

搜尋字詞

- 預設： `[]`

- 陣列

### `--browser`

用來開啟URL的瀏覽器。 將0設為無。

- 需要值

### `--pipe`

將URL輸出到stdout。

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `help`

顯示命令的說明

```bash
magento-cloud help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

命令名稱

- 預設： `help`


### `--format`

輸出格式（txt、json或md）

- 預設： `txt`
- 需要值

### `--raw`

輸出原始指令說明

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `list`

列出命令

```bash
magento-cloud list [--raw] [--format FORMAT] [--all] [--] [<namespace>]
```


### `command`

要執行的命令

- 必填

### `namespace`

名稱空間名稱


### `--raw`

輸出原始命令清單

- 預設： `false`
- 不接受值

### `--format`

輸出格式（txt、xml、json或md）

- 預設： `txt`
- 需要值

### `--all`

顯示所有命令，包括隱藏的命令

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `multi`

在多個專案上執行命令

```bash
magento-cloud multi [-p|--projects PROJECTS] [--continue] [--sort SORT] [--reverse] [--] <cmd> (<cmd>)...
```


### `cmd`

要執行的命令

- 預設： `[]`

- 必填
- 陣列

### `--projects`， `-p`

專案ID清單，以逗號和/或空格分隔

- 需要值

### `--continue`

即使發生例外狀況，仍繼續執行命令

- 預設： `false`
- 不接受值

### `--sort`

用來排序專案選項清單的屬性

- 預設： `title`
- 需要值

### `--reverse`

反轉專案選項的順序

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `web`

在Web UI中開啟專案

```bash
magento-cloud web [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--browser`

用來開啟URL的瀏覽器。 將0設為無。

- 需要值

### `--pipe`

將URL輸出到stdout。

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `activity:cancel`

取消活動

```bash
magento-cloud activity:cancel [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

活動ID。 預設為最近的可取消活動。


### `--type`， `-t`

依型別篩選（選取預設活動時）。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。 %或*字元可作為此型別的萬用字元，例如&#39;%var%&#39;以選取變數相關的活動。

- 預設： `[]`
- 需要值

### `--exclude-type`， `-x`

依型別排除（選取預設活動時）。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。 %或*字元可作為萬用字元來排除型別。

- 預設： `[]`
- 需要值

### `--all`， `-a`

檢查所有環境上最近的活動（當選取預設活動時）

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `activity:get`

檢視單一活動的詳細資訊

```bash
magento-cloud activity:get [-P|--property PROPERTY] [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

活動ID。 預設為最近的活動。


### `--property`， `-P`

要檢視的屬性

- 需要值

### `--type`， `-t`

依型別篩選（選取預設活動時）。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。 %或*字元可作為此型別的萬用字元，例如&#39;%var%&#39;以選取變數相關的活動。

- 預設： `[]`
- 需要值

### `--exclude-type`， `-x`

依型別排除（選取預設活動時）。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。 %或*字元可作為萬用字元來排除型別。

- 預設： `[]`
- 需要值

### `--state`

依狀態篩選（選取預設活動時）： in_progress、pending、complete或canceled。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--result`

依結果篩選（選取預設活動時）：成功或失敗

- 需要值

### `--incomplete`， `-i`

僅包含未完成的活動（選取預設活動時）。 這是\&lt;info>—state=in_progress，pending\&lt;/info>

- 預設： `false`
- 不接受值

### `--all`， `-a`

檢查所有環境上最近的活動（當選取預設活動時）

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `activity:list`

取得環境或專案的活動清單

```bash
magento-cloud activities [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--type`， `-t`

依型別篩選活動值可能會以逗號（例如&quot;a，b，c&quot;）和/或空白字元分割。 活動名稱的第一部分可以省略，例如，「cron」可以選擇「environment.cron」活動。 %或*字元可作為萬用字元使用，例如&#39;%var%&#39;以選取與變數相關的活動。

- 預設： `[]`
- 需要值

### `--exclude-type`， `-x`

依型別排除活動。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。 活動名稱的第一部分可以省略，例如，「cron」可以排除「environment.cron」活動。 %或*字元可作為萬用字元來排除型別。

- 預設： `[]`
- 需要值

### `--limit`

限制顯示的結果數

- 預設： `10`
- 需要值

### `--start`

只會列出在此日期之前建立的活動

- 需要值

### `--state`

依狀態篩選活動： in_progress、pending、complete或canceled。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--result`

依結果篩選活動：成功或失敗

- 需要值

### `--incomplete`， `-i`

僅列出未完成的活動

- 預設： `false`
- 不接受值

### `--all`， `-a`

列出所有環境上的活動

- 預設： `false`
- 不接受值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用欄： id*、created*、description*、progress*、state*、result*、completed、environments、type （* =預設欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `activity:log`

顯示活動的記錄

```bash
magento-cloud activity:log [--refresh REFRESH] [-t|--timestamps] [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

活動ID。 預設為最近的活動。


### `--refresh`

活動重新整理間隔（秒）。 設為0可停用重新整理。

- 預設： `3`
- 需要值

### `--timestamps`， `-t`

在每個訊息旁邊顯示時間戳記

- 預設： `false`
- 不接受值

### `--type`

依型別篩選（選取預設活動時）。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。 %或*字元可作為此型別的萬用字元，例如&#39;%var%&#39;以選取變數相關的活動。

- 預設： `[]`
- 需要值

### `--exclude-type`， `-x`

依型別排除（選取預設活動時）。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。 %或*字元可作為萬用字元來排除型別。

- 預設： `[]`
- 需要值

### `--state`

依狀態篩選（選取預設活動時）： in_progress、pending、complete或canceled。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--result`

依結果篩選（選取預設活動時）：成功或失敗

- 需要值

### `--incomplete`， `-i`

僅包含未完成的活動（選取預設活動時）。 這是\&lt;info>—state=in_progress，pending\&lt;/info>

- 預設： `false`
- 不接受值

### `--all`， `-a`

檢查所有環境上最近的活動（當選取預設活動時）

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `app:config-get`

檢視應用程式的設定

```bash
magento-cloud app:config-get [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--property`， `-P`

要檢視的設定屬性

- 需要值

### `--refresh`

是否要重新整理快取

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--identity-file`， `-i`

[已棄用的選項，不再使用]

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `app:list`

列出專案中的應用程式

```bash
magento-cloud apps [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

是否要重新整理快取

- 預設： `false`
- 不接受值

### `--pipe`

僅輸出應用程式名稱清單

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄： name*、type*、disk、path、size （* =預設欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `auth:api-token-login`

使用API權杖登入Magento Cloud

```bash
magento-cloud auth:api-token-login
```

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `auth:browser-login`

透過瀏覽器登入Magento Cloud

```bash
magento-cloud login [-f|--force] [--browser BROWSER] [--pipe]
```

### `--force`， `-f`

再次登入，即使已登入

- 預設： `false`
- 不接受值

### `--browser`

用來開啟URL的瀏覽器。 將0設為無。

- 需要值

### `--pipe`

將URL輸出到stdout。

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `auth:info`

顯示您的帳戶資訊

```bash
magento-cloud auth:info [--no-auto-login] [-P|--property PROPERTY] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--] [<property>]
```


### `property`

要檢視的帳戶屬性


### `--no-auto-login`

略過自動登入。 若未登入，將不會輸出任何內容，且退出代碼將為0 （假設沒有其他錯誤）。

- 預設： `false`
- 不接受值

### `--property`， `-P`

要檢視的帳戶屬性（替代語法）

- 需要值

### `--refresh`

是否要重新整理快取

- 預設： `false`
- 不接受值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `auth:logout`

登出Magento Cloud

```bash
magento-cloud logout [-a|--all] [--other]
```

### `--all`， `-a`

從所有本機工作階段登出

- 預設： `false`
- 不接受值

### `--other`

從其他本機工作階段登出

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `blackfire:setup`

設定專案的Blackfire.io整合

```bash
magento-cloud blackfire:setup [--server_id SERVER_ID] [--server_token SERVER_TOKEN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--server_id`

伺服器ID

- 需要值

### `--server_token`

伺服器權杖

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `certificate:add`

將SSL憑證新增至專案

```bash
magento-cloud certificate:add [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--cert`

憑證檔案的路徑

- 需要值

### `--key`

憑證私密金鑰檔案的路徑

- 需要值

### `--chain`

憑證鏈結檔案的路徑

- 預設： `[]`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `certificate:delete`

從專案刪除憑證

```bash
magento-cloud certificate:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <id>
```


### `id`

憑證ID （或其開頭）

- 必填

### `--project`， `-p`

專案ID或URL

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `certificate:get`

檢視憑證

```bash
magento-cloud certificate:get [-P|--property PROPERTY] [--date-fmt DATE-FMT] [-p|--project PROJECT] [--] <id>
```


### `id`

憑證ID （或其開頭）

- 必填

### `--property`， `-P`

要檢視的憑證屬性

- 需要值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `certificate:list`

列出專案憑證

```bash
magento-cloud certificates [--domain DOMAIN] [--exclude-domain EXCLUDE-DOMAIN] [--issuer ISSUER] [--only-auto] [--no-auto] [--ignore-expiry] [--only-expired] [--no-expired] [--pipe-domains] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--domain`

依網域名稱篩選（不區分大小寫搜尋）

- 需要值

### `--exclude-domain`

排除憑證，依網域名稱比對（搜尋不區分大小寫）

- 需要值

### `--issuer`

依簽發者篩選

- 需要值

### `--only-auto`

僅顯示自動提供的憑證

- 預設： `false`
- 不接受值

### `--no-auto`

僅顯示手動新增的憑證

- 預設： `false`
- 不接受值

### `--ignore-expiry`

顯示過期和未過期的憑證

- 預設： `false`
- 不接受值

### `--only-expired`

僅顯示過期的憑證

- 預設： `false`
- 不接受值

### `--no-expired`

僅顯示未過期的憑證（預設）

- 預設： `false`
- 不接受值

### `--pipe-domains`

僅傳回憑證涵蓋的網域名稱清單

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄：已建立、網域、過期、ID、簽發者。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `commit:get`

顯示認可詳細資料

```bash
magento-cloud commit:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

認可SHA。 這也可以接受父項認可的「HEAD」，以及插入符號(^)或波狀符號(~)尾碼。

- 預設： `HEAD`


### `--property`， `-P`

要顯示的認可屬性。

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `commit:list`

清單認可

```bash
magento-cloud commits [--limit LIMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

起始Git認可SHA。 這也可以接受父項認可的「HEAD」，以及插入符號(^)或波狀符號(~)尾碼。


### `--limit`

要顯示的認可數目。

- 預設： `10`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用欄：作者、日期、sha、摘要。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `db:dump`

建立遠端資料庫的本機傾印

```bash
magento-cloud db:dump [--schema SCHEMA] [-f|--file FILE] [-d|--directory DIRECTORY] [-z|--gzip] [-t|--timestamp] [-o|--stdout] [--table TABLE] [--exclude-table EXCLUDE-TABLE] [--schema-only] [--charset CHARSET] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--schema`

要傾印的結構描述。 省略以使用預設架構（通常為「主要」）。

- 需要值

### `--file`， `-f`

傾印的自訂檔案名稱

- 需要值

### `--directory`， `-d`

傾印的自訂目錄

- 需要值

### `--gzip`， `-z`

使用gzip壓縮傾印

- 預設： `false`
- 不接受值

### `--timestamp`， `-t`

將時間戳記新增到傾印檔案名稱

- 預設： `false`
- 不接受值

### `--stdout`， `-o`

輸出到STDOUT而非檔案

- 預設： `false`
- 不接受值

### `--table`

要包含的表格

- 預設： `[]`
- 需要值

### `--exclude-table`

要排除的表格

- 預設： `[]`
- 需要值

### `--schema-only`

僅傾印結構描述，無資料

- 預設： `false`
- 不接受值

### `--charset`

傾印的字元集編碼

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--relationship`， `-r`

要使用的服務關係

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `db:size`

預估資料庫的磁碟使用量

```bash
magento-cloud db:size [-B|--bytes] [-C|--cleanup] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE]
```

### `--bytes`， `-B`

以位元組為單位顯示大小。

- 預設： `false`
- 不接受值

### `--cleanup`， `-C`

檢查是否可以清除資料表並顯示建議（僅限InnoDb）。

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--relationship`， `-r`

要使用的服務關係

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用欄：max、percent_used、used。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `db:sql`

在遠端資料庫上執行SQL

```bash
magento-cloud sql [--raw] [--schema SCHEMA] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [--] [<query>]
```


### `query`

要執行的SQL敘述句


### `--raw`

產生原始、非表格式輸出

- 預設： `false`
- 不接受值

### `--schema`

要使用的結構描述。 省略以使用預設架構（通常為「主要」）。 傳遞空字串以不使用任何結構描述。

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--relationship`， `-r`

要使用的服務關係

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `domain:add`

將新網域新增至專案

```bash
magento-cloud domain:add [--cert CERT] [--key KEY] [--chain CHAIN] [--attach ATTACH] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

網域名稱

- 必填

### `--cert`

此網域的憑證檔案路徑

- 需要值

### `--key`

所提供憑證之私密金鑰檔案的路徑。

- 需要值

### `--chain`

提供的憑證的憑證鏈結檔案的路徑

- 預設： `[]`
- 需要值

### `--attach`

此將在環境的路由中取代的生產網域。 非生產環境網域需要。

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `domain:delete`

從專案刪除網域

```bash
magento-cloud domain:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

網域名稱

- 必填

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `domain:get`

顯示網域的詳細資訊

```bash
magento-cloud domain:get [-P|--property PROPERTY] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<name>]
```


### `name`

網域名稱


### `--property`， `-P`

要檢視的網域屬性

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `domain:list`

取得所有網域的清單

```bash
magento-cloud domains [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的資料欄： name*、ssl*、created_at*、registered_name、replacement_for、type、updated_at （* =預設資料欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `domain:update`

更新網域

```bash
magento-cloud domain:update [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

網域名稱

- 必填

### `--cert`

此網域的憑證檔案路徑

- 需要值

### `--key`

所提供憑證之私密金鑰檔案的路徑。

- 需要值

### `--chain`

提供的憑證的憑證鏈結檔案的路徑

- 預設： `[]`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:activate`

啟用環境

```bash
magento-cloud environment:activate [--parent PARENT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```


### `environment`

要啟用的環境

- 預設： `[]`

- 陣列

### `--parent`

在啟用之前設定新的環境父項

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:branch`

分支環境

```bash
magento-cloud branch [--title TITLE] [--type TYPE] [--no-clone-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>] [<parent>]
```


### `id`

新環境的ID （分支名稱）


### `parent`

新環境的父級


### `--title`

新環境的標題

- 需要值

### `--type`

新環境的型別

- 需要值

### `--no-clone-parent`

不要複製父環境的資料

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:checkout`

檢視環境

```bash
magento-cloud checkout [-i|--identity-file IDENTITY-FILE] [--] [<id>]
```


### `id`

要簽出之環境的ID。 例如：「sprint2」


### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:delete`

刪除一或多個環境

```bash
magento-cloud environment:delete [--delete-branch] [--no-delete-branch] [--type TYPE] [-t|--only-type ONLY-TYPE] [--exclude EXCLUDE] [--exclude-type EXCLUDE-TYPE] [--inactive] [--merged] [--allow-delete-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```


### `environment`

要刪除的環境。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`

- 陣列

### `--delete-branch`

刪除非使用中環境的Git分支，無需確認

- 預設： `false`
- 不接受值

### `--no-delete-branch`

請勿刪除任何Git分支（非使用中環境）

- 預設： `false`
- 不接受值

### `--type`

刪除某型別的所有環境（新增至其他任何選取的專案）值可能會以逗號（例如&quot;a，b，c&quot;）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--only-type`， `-t`

只有特定型別的刪除環境值才可以分割為逗號（例如&quot;a，b，c&quot;）和/或空格。

- 預設： `[]`
- 需要值

### `--exclude`

不要刪除的環境。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--exclude-type`

不得刪除的環境型別值可能會以逗號（例如&quot;a，b，c&quot;）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--inactive`

刪除所有非使用中的環境（新增到其他所選環境）

- 預設： `false`
- 不接受值

### `--merged`

刪除所有合併的環境（新增至其他所選環境）

- 預設： `false`
- 不接受值

### `--allow-delete-parent`

允許刪除具有子項的環境

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:http-access`

更新環境的HTTP存取設定

```bash
magento-cloud httpaccess [--access ACCESS] [--auth AUTH] [--enabled ENABLED] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--access`

存取限制，格式為「permission：address」。 使用0以清除所有地址。

- 預設： `[]`
- 需要值

### `--auth`

HTTP基本驗證認證，格式為「使用者名稱：密碼」。 使用0可清除所有認證。

- 預設： `[]`
- 需要值

### `--enabled`

存取控制是否應該啟用：1代表啟用，0代表停用

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:info`

讀取或設定環境的屬性

```bash
magento-cloud environment:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

屬性的名稱


### `value`

設定屬性的新值


### `--refresh`

是否要重新整理快取

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:init`

從公共Git存放庫初始化環境

```bash
magento-cloud environment:init [--profile PROFILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <url>
```


### `url`

Git存放庫的URL

- 必填

### `--profile`

設定檔的名稱

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:list`

取得環境清單

```bash
magento-cloud environments [-I|--no-inactive] [--pipe] [--refresh REFRESH] [--sort SORT] [--reverse] [--type TYPE] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--no-inactive`， `-I`

不要顯示非使用中的環境

- 預設： `false`
- 不接受值

### `--pipe`

輸出環境ID的簡單清單。

- 預設： `false`
- 不接受值

### `--refresh`

是否要重新整理清單。

- 預設： `1`
- 需要值

### `--sort`

排序依據的屬性

- 預設： `title`
- 需要值

### `--reverse`

以反向（遞減）順序排序

- 預設： `false`
- 不接受值

### `--type`

依環境型別篩選清單。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄： id*、title*、status*、type*、created、machine_name、updated （* =預設欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:logs`

讀取環境的記錄

```bash
magento-cloud log [--lines LINES] [--tail] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<type>]
```


### `type`

紀錄型別，例如「存取」或「錯誤」


### `--lines`

要顯示的行數

- 預設： `100`
- 需要值

### `--tail`

持續追蹤記錄

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--worker`

背景工作名稱

- 需要值

### `--instance`， `-I`

例項ID

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:merge`

合併環境

```bash
magento-cloud merge [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

要合併的環境


### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:pause`

暫停環境

```bash
magento-cloud environment:pause [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:push`

將程式碼推送至環境

```bash
magento-cloud push [--target TARGET] [-f|--force] [--force-with-lease] [-u|--set-upstream] [--activate] [--parent PARENT] [--type TYPE] [--no-clone-parent] [-W|--no-wait] [--wait] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-i|--identity-file IDENTITY-FILE] [--] [<source>]
```


### `source`

來源參考：分支名稱或認可雜湊

- 預設： `HEAD`


### `--target`

目標分支名稱。 預設為目前的分支。

- 需要值

### `--force`， `-f`

允許非快轉更新

- 預設： `false`
- 不接受值

### `--force-with-lease`

如果遠端追蹤分支為最新狀態，則允許非快轉更新

- 預設： `false`
- 不接受值

### `--set-upstream`， `-u`

將目標環境設定為來源分支的上游。 這也會將目標專案設定為本機存放庫的遠端。

- 預設： `false`
- 不接受值

### `--activate`

在推播之前啟動環境

- 預設： `false`
- 不接受值

### `--parent`

設定新環境父項（僅用於 — activate）

- 需要值

### `--type`

設定環境型別（僅用於 — activate ）

- 需要值

### `--no-clone-parent`

請勿原地複製父分支的資料（僅用於 — activate）

- 預設： `false`
- 不接受值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:redeploy`

重新部署環境

```bash
magento-cloud redeploy [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:relationships`

顯示環境的關係

```bash
magento-cloud relationships [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<environment>]
```


### `environment`

環境


### `--property`， `-P`

要檢視的關係屬性

- 需要值

### `--refresh`

是否要重新整理關係

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:resume`

繼續暫停的環境

```bash
magento-cloud environment:resume [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:scp`

使用scp將檔案複製到環境或從環境複製檔案

```bash
magento-cloud scp [-r|--recursive] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<files>]...
```


### `files`

要複製的檔案。 使用remote：前置詞來定義遠端位置。

- 預設： `[]`

- 陣列

### `--recursive`， `-r`

遞回複製整個目錄

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--worker`

背景工作名稱

- 需要值

### `--instance`， `-I`

例項ID

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:ssh`

SSH連線至目前的環境

```bash
magento-cloud ssh [--pipe] [--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<cmd>]...
```


### `cmd`

要在環境中執行的命令。

- 預設： `[]`

- 陣列

### `--pipe`

僅輸出SSH URL。

- 預設： `false`
- 不接受值

### `--all`

輸出所有SSH URL （適用於每個應用程式）。

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--worker`

背景工作名稱

- 需要值

### `--instance`， `-I`

例項ID

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:synchronize`

同步環境的程式碼和/或其父系資料

```bash
magento-cloud sync [--rebase] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<synchronize>]...
```


### `synchronize`

要同步的專案：「代碼」、「資料」或兩者

- 預設： `[]`

- 陣列

### `--rebase`

透過重新基底而不是合併來同步程式碼

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:url`

取得環境的公用URL

```bash
magento-cloud url [-1|--primary] [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--primary`， `-1`

只傳回主要路由的URL

- 預設： `false`
- 不接受值

### `--browser`

用來開啟URL的瀏覽器。 將0設為無。

- 需要值

### `--pipe`

將URL輸出到stdout。

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `environment:xdebug`

開啟環境上的Xdebug通道

```bash
magento-cloud xdebug [--port PORT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

本機連線埠

- 預設： `9000`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--worker`

背景工作名稱

- 需要值

### `--instance`， `-I`

例項ID

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `integration:activity:get`

檢視單一整合活動的詳細資訊

```bash
magento-cloud integration:activity:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<integration>] [<activity>]
```


### `integration`

整合ID。 保留空白以從清單中選擇。


### `activity`

活動ID。 預設為最近的整合活動。


### `--property`， `-P`

要檢視的屬性

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

[已棄用的選項，未使用]

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `integration:activity:list`

取得整合的活動清單

```bash
magento-cloud int:act [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

整合ID。 保留空白以從清單中選擇。


### `--type`

依型別篩選活動。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--exclude-type`， `-x`

依型別排除活動。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。 %或*字元可作為萬用字元來排除型別。

- 預設： `[]`
- 需要值

### `--limit`

限制顯示的結果數

- 預設： `10`
- 需要值

### `--start`

只會列出在此日期之前建立的活動

- 需要值

### `--state`

依狀態篩選活動。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--result`

依結果篩選活動

- 需要值

### `--incomplete`， `-i`

僅列出未完成的活動

- 預設： `false`
- 不接受值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄： id*、created*、description*、type*、state*、result*、completed （* =預設欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

[已棄用的選項，未使用]

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `integration:activity:log`

顯示整合活動的記錄

```bash
magento-cloud integration:activity:log [-t|--timestamps] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<integration>] [<activity>]
```


### `integration`

整合ID。 保留空白以從清單中選擇。


### `activity`

活動ID。 預設為最近的整合活動。


### `--timestamps`， `-t`

在每個訊息旁邊顯示時間戳記

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

[已棄用的選項，未使用]

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `integration:add`

將整合新增至專案

```bash
magento-cloud integration:add [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--type`

整合型別(「bitbucket」、「bitbucket_server」、「github」、「gitlab」、「webhook」、「health.email」、「health.pagerduty」、「health.slack」、「health.webhook」、「httplog」、「script」、「newrelic」、「splunk」、「sumologic」、「syslog」)

- 需要值

### `--base-url`

伺服器安裝的基底URL

- 需要值

### `--bitbucket-url`

Bitbucket伺服器安裝的基底URL

- 需要值

### `--username`

Bitbucket伺服器使用者名稱

- 需要值

### `--token`

整合的驗證或存取權杖

- 需要值

### `--key`

Bitbucket OAuth消費者金鑰

- 需要值

### `--secret`

Bitbucket OAuth消費者密碼

- 需要值

### `--license-key`

New Relic記錄授權金鑰

- 需要值

### `--server-project`

專案（例如「namespace/repo」）

- 需要值

### `--repository`

要追蹤的存放庫（例如「所有者/存放庫」）

- 需要值

### `--build-merge-requests`

GitLab：將合併請求建置為環境

- 預設： `true`
- 需要值

### `--build-pull-requests`

將每個提取請求建置為環境

- 預設： `true`
- 需要值

### `--build-draft-pull-requests`

建立草稿提取請求

- 預設： `true`
- 需要值

### `--build-pull-requests-post-merge`

根據它們的合併後狀態建置提取請求

- 預設： `false`
- 需要值

### `--build-wip-merge-requests`

GitLab：建置WIP合併請求

- 預設： `true`
- 需要值

### `--merge-requests-clone-parent-data`

GitLab：複製合併請求的資料

- 預設： `true`
- 需要值

### `--pull-requests-clone-parent-data`

為提取請求複製父環境的資料

- 預設： `true`
- 需要值

### `--resync-pull-requests`

重新同步處理每個組建的提取請求環境資料

- 預設： `false`
- 需要值

### `--fetch-branches`

從遠端擷取所有分支（以非使用中環境的形式）

- 預設： `true`
- 需要值

### `--prune-branches`

刪除遠端上不存在的分支

- 預設： `true`
- 需要值

### `--resources-init`

初始化新服務時要使用的資源(&#39;minimum&#39;、&#39;default&#39;、&#39;manual&#39;、&#39;parent&#39;)

- 需要值

### `--url`

整合的URL或API端點

- 需要值

### `--shared-key`

Webhook： JWS共用秘密金鑰

- 需要值

### `--file`

包含要上傳之指令碼的本機檔案名稱

- 需要值

### `--events`

要執行動作的事件清單，例如environment.push

- 預設： `*`
- 需要值

### `--states`

要採取行動的狀態清單，例如pending、 in_progress、 complete

- 預設： `complete`
- 需要值

### `--environments`

要包含的環境ID

- 預設： `*`
- 需要值

### `--excluded-environments`

要排除的環境ID

- 預設： `[]`
- 需要值

### `--from-address`

[可選] 警示電子郵件的自訂寄件者地址

- 需要值

### `--recipients`

收件者電子郵件地址

- 預設： `[]`
- 需要值

### `--channel`

Slack管道

- 需要值

### `--routing-key`

PagerDuty路由索引鍵

- 需要值

### `--category`

相撲邏輯類別，用於篩選

- 需要值

### `--index`

Splunk索引

- 需要值

### `--sourcetype`

Splunk事件來源型別

- 需要值

### `--protocol`

Syslog傳輸通訊協定(&#39;tcp&#39;、&#39;udp&#39;、&#39;tls&#39;)

- 預設： `tls`
- 需要值

### `--syslog-host`

Syslog轉送/收集器主機

- 需要值

### `--syslog-port`

Syslog轉送/收集器連線埠

- 需要值

### `--facility`

Syslog工具

- 預設： `1`
- 需要值

### `--message-format`

Syslog訊息格式（&#39;rfc3164&#39;或&#39;rfc5424&#39;）

- 預設： `rfc5424`
- 需要值

### `--auth-mode`

驗證模式（「prefix」或「structured_data」）

- 預設： `prefix`
- 需要值

### `--auth-token`

驗證Token

- 需要值

### `--verify-tls`

是否應啟用HTTPS憑證驗證（建議）

- 預設： `true`
- 需要值

### `--header`

用於POST請求的HTTP標頭。 以冒號(：)分隔名稱和值。

- 預設： `[]`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `integration:delete`

從專案刪除整合

```bash
magento-cloud integration:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

整合ID。 保留空白以從清單中選擇。


### `--project`， `-p`

專案ID或URL

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `integration:get`

檢視整合的詳細資訊

```bash
magento-cloud integration:get [-P|--property [PROPERTY]] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<id>]
```


### `id`

整合ID。 保留空白以從清單中選擇。


### `--property`， `-P`

要檢視的整合屬性

- 接受值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `integration:list`

檢視專案整合的清單

```bash
magento-cloud integrations [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄：id、摘要、型別。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `integration:update`

更新整合

```bash
magento-cloud integration:update [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

要更新的整合ID


### `--type`

整合型別(「bitbucket」、「bitbucket_server」、「github」、「gitlab」、「webhook」、「health.email」、「health.pagerduty」、「health.slack」、「health.webhook」、「httplog」、「script」、「newrelic」、「splunk」、「sumologic」、「syslog」)

- 需要值

### `--base-url`

伺服器安裝的基底URL

- 需要值

### `--bitbucket-url`

Bitbucket伺服器安裝的基底URL

- 需要值

### `--username`

Bitbucket伺服器使用者名稱

- 需要值

### `--token`

整合的驗證或存取權杖

- 需要值

### `--key`

Bitbucket OAuth消費者金鑰

- 需要值

### `--secret`

Bitbucket OAuth消費者密碼

- 需要值

### `--license-key`

New Relic記錄授權金鑰

- 需要值

### `--server-project`

專案（例如「namespace/repo」）

- 需要值

### `--repository`

要追蹤的存放庫（例如「所有者/存放庫」）

- 需要值

### `--build-merge-requests`

GitLab：將合併請求建置為環境

- 預設： `true`
- 需要值

### `--build-pull-requests`

將每個提取請求建置為環境

- 預設： `true`
- 需要值

### `--build-draft-pull-requests`

建立草稿提取請求

- 預設： `true`
- 需要值

### `--build-pull-requests-post-merge`

根據它們的合併後狀態建置提取請求

- 預設： `false`
- 需要值

### `--build-wip-merge-requests`

GitLab：建置WIP合併請求

- 預設： `true`
- 需要值

### `--merge-requests-clone-parent-data`

GitLab：複製合併請求的資料

- 預設： `true`
- 需要值

### `--pull-requests-clone-parent-data`

為提取請求複製父環境的資料

- 預設： `true`
- 需要值

### `--resync-pull-requests`

重新同步處理每個組建的提取請求環境資料

- 預設： `false`
- 需要值

### `--fetch-branches`

從遠端擷取所有分支（以非使用中環境的形式）

- 預設： `true`
- 需要值

### `--prune-branches`

刪除遠端上不存在的分支

- 預設： `true`
- 需要值

### `--resources-init`

初始化新服務時要使用的資源(&#39;minimum&#39;、&#39;default&#39;、&#39;manual&#39;、&#39;parent&#39;)

- 需要值

### `--url`

整合的URL或API端點

- 需要值

### `--shared-key`

Webhook： JWS共用秘密金鑰

- 需要值

### `--file`

包含要上傳之指令碼的本機檔案名稱

- 需要值

### `--events`

要執行動作的事件清單，例如environment.push

- 預設： `*`
- 需要值

### `--states`

要採取行動的狀態清單，例如pending、 in_progress、 complete

- 預設： `complete`
- 需要值

### `--environments`

要包含的環境ID

- 預設： `*`
- 需要值

### `--excluded-environments`

要排除的環境ID

- 預設： `[]`
- 需要值

### `--from-address`

[可選] 警示電子郵件的自訂寄件者地址

- 需要值

### `--recipients`

收件者電子郵件地址

- 預設： `[]`
- 需要值

### `--channel`

Slack管道

- 需要值

### `--routing-key`

PagerDuty路由索引鍵

- 需要值

### `--category`

相撲邏輯類別，用於篩選

- 需要值

### `--index`

Splunk索引

- 需要值

### `--sourcetype`

Splunk事件來源型別

- 需要值

### `--protocol`

Syslog傳輸通訊協定(&#39;tcp&#39;、&#39;udp&#39;、&#39;tls&#39;)

- 預設： `tls`
- 需要值

### `--syslog-host`

Syslog轉送/收集器主機

- 需要值

### `--syslog-port`

Syslog轉送/收集器連線埠

- 需要值

### `--facility`

Syslog工具

- 預設： `1`
- 需要值

### `--message-format`

Syslog訊息格式（&#39;rfc3164&#39;或&#39;rfc5424&#39;）

- 預設： `rfc5424`
- 需要值

### `--auth-mode`

驗證模式（「prefix」或「structured_data」）

- 預設： `prefix`
- 需要值

### `--auth-token`

驗證Token

- 需要值

### `--verify-tls`

是否應啟用HTTPS憑證驗證（建議）

- 預設： `true`
- 需要值

### `--header`

用於POST請求的HTTP標頭。 以冒號(：)分隔名稱和值。

- 預設： `[]`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `integration:validate`

驗證現有的整合

```bash
magento-cloud integration:validate [-p|--project PROJECT] [--] [<id>]
```


### `id`

整合ID。 保留空白以從清單中選擇。


### `--project`， `-p`

專案ID或URL

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `local:build`

在本機建置目前的專案

```bash
magento-cloud build [-a|--abslinks] [-s|--source SOURCE] [-d|--destination DESTINATION] [-c|--copy] [--clone] [--run-deploy-hooks] [--no-clean] [--no-archive] [--no-backup] [--no-cache] [--no-build-hooks] [--no-deps] [--working-copy] [--concurrency CONCURRENCY] [--lock] [--] [<app>]...
```


### `app`

指定要建置的應用程式

- 預設： `[]`

- 陣列

### `--abslinks`， `-a`

使用絕對連結

- 預設： `false`
- 不接受值

### `--source`， `-s`

來源目錄。 預設為目前的專案根目錄。

- 需要值

### `--destination`， `-d`

每個應用程式的Web根目錄將與其符號連結的目的地。 預設： _www

- 需要值

### `--copy`， `-c`

複製到組建目錄，而非從來源同步連結

- 預設： `false`
- 不接受值

### `--clone`

使用Git將目前的HEAD複製至組建目錄

- 預設： `false`
- 不接受值

### `--run-deploy-hooks`

執行部署和/或post_deploy鉤點

- 預設： `false`
- 不接受值

### `--no-clean`

不要移除舊的組建

- 預設： `false`
- 不接受值

### `--no-archive`

請勿建立或使用組建封存

- 預設： `false`
- 不接受值

### `--no-backup`

不要備份先前的組建

- 預設： `false`
- 不接受值

### `--no-cache`

停用快取

- 預設： `false`
- 不接受值

### `--no-build-hooks`

請勿執行建置後鉤點

- 預設： `false`
- 不接受值

### `--no-deps`

請勿在本機安裝組建相依性

- 預設： `false`
- 不接受值

### `--working-copy`

Drush：使用Git來複製每個Drupal模組的存放庫，而不只是下載版本

- 預設： `false`
- 不接受值

### `--concurrency`

Drush：設定將同時處理的並行專案數目

- 預設： `4`
- 需要值

### `--lock`

Drush：建立或更新鎖定檔案（僅適用於Drush 7+版）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `local:dir`

尋找本機專案根目錄

```bash
magento-cloud dir [<subdir>]
```


### `subdir`

要尋找的子目錄（&#39;local&#39;、&#39;web&#39;或&#39;shared&#39;）


### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `metrics:all`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/>顯示環境的CPU、磁碟和記憶體量度

```bash
magento-cloud metrics [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`， `-B`

以位元組為單位顯示大小

- 預設： `false`
- 不接受值

### `--range`， `-r`

時間範圍。 此期間將載入量度，直到結束時間(—to)為止。 您可以指定單位：小時(h)、分鐘(m)或秒(s)。 最小\&lt;comment>5分鐘\&lt;/comment>，最大值\&lt;comment>8h\&lt;/comment> 或更多（視專案而定）、預設\&lt;comment>10分鐘\&lt;/comment>.

- 需要值

### `--interval`， `-i`

時間間隔。 預設為範圍的除法。 您可以指定單位：小時(h)、分鐘(m)或秒(s)。 最小\&lt;comment>1分鐘\&lt;/comment>.

- 需要值

### `--to`

結束時間。 預設為現在。

- 需要值

### `--latest`， `-1`

僅顯示最新的單一資料點

- 預設： `false`
- 不接受值

### `--service`， `-s`

依服務或應用程式名稱篩選%或*字元可當作萬用字元。

- 預設： `[]`
- 需要值

### `--type`

依服務型別篩選（如果未提供 — 服務）。 不需要版本。 %或*字元可作為萬用字元使用。

- 預設： `[]`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的資料欄：timestamp*、service*、cpu_percent*、mem_percent*、disk_percent*、tmp_disk_percent*、cpu_limit、cpu_used、disk_limit、disk_used、inodes_limit、inodes_percent、inodes_used、mem_limit、mem_used、tmp_disk_used、tmp_inodes_limit、tmp_inodes_percent、tmp_inodes_used、型別（* =預設資料欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `metrics:cpu`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/>顯示環境的CPU使用量

```bash
magento-cloud cpu [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--range`， `-r`

時間範圍。 此期間將載入量度，直到結束時間(—to)為止。 您可以指定單位：小時(h)、分鐘(m)或秒(s)。 最小\&lt;comment>5分鐘\&lt;/comment>，最大值\&lt;comment>8h\&lt;/comment> 或更多（視專案而定）、預設\&lt;comment>10分鐘\&lt;/comment>.

- 需要值

### `--interval`， `-i`

時間間隔。 預設為範圍的除法。 您可以指定單位：小時(h)、分鐘(m)或秒(s)。 最小\&lt;comment>1分鐘\&lt;/comment>.

- 需要值

### `--to`

結束時間。 預設為現在。

- 需要值

### `--latest`， `-1`

僅顯示最新的單一資料點

- 預設： `false`
- 不接受值

### `--service`， `-s`

依服務或應用程式名稱篩選%或*字元可當作萬用字元。

- 預設： `[]`
- 需要值

### `--type`

依服務型別篩選（如果未提供 — 服務）。 不需要版本。 %或*字元可作為萬用字元使用。

- 預設： `[]`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄： timestamp*、service*、used*、limit*、%*、type （* =預設欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `metrics:disk-usage`

顯示環境的磁碟使用情況

```bash
magento-cloud disk [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [--tmp] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`， `-B`

以位元組為單位顯示大小

- 預設： `false`
- 不接受值

### `--range`， `-r`

時間範圍。 此期間將載入量度，直到結束時間(—to)為止。 您可以指定單位：小時(h)、分鐘(m)或秒(s)。 最小\&lt;comment>5分鐘\&lt;/comment>，最大值\&lt;comment>8h\&lt;/comment> 或更多（視專案而定）、預設\&lt;comment>10分鐘\&lt;/comment>.

- 需要值

### `--interval`， `-i`

時間間隔。 預設為範圍的除法。 您可以指定單位：小時(h)、分鐘(m)或秒(s)。 最小\&lt;comment>1分鐘\&lt;/comment>.

- 需要值

### `--to`

結束時間。 預設為現在。

- 需要值

### `--latest`， `-1`

僅顯示最新的單一資料點

- 預設： `false`
- 不接受值

### `--service`， `-s`

依服務或應用程式名稱篩選%或*字元可當作萬用字元。

- 預設： `[]`
- 需要值

### `--type`

依服務型別篩選（如果未提供 — 服務）。 不需要版本。 %或*字元可作為萬用字元使用。

- 預設： `[]`
- 需要值

### `--tmp`

報告暫存磁碟使用狀況（顯示資料欄：timestamp、service、tmp_used、tmp_limit、tmp_percent、tmp_ipercent）

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄：timestamp*、service*、used*、limit*、percent*、tmp_percent*、ilimit、iused、tmp_ilimit、tmp_ipercent、tmp_iused、tmp_limit、tmp_used、type （* =預設欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `metrics:memory`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/>顯示環境的記憶體使用情況

```bash
magento-cloud mem [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`， `-B`

以位元組為單位顯示大小

- 預設： `false`
- 不接受值

### `--range`， `-r`

時間範圍。 此期間將載入量度，直到結束時間(—to)為止。 您可以指定單位：小時(h)、分鐘(m)或秒(s)。 最小\&lt;comment>5分鐘\&lt;/comment>，最大值\&lt;comment>8h\&lt;/comment> 或更多（視專案而定）、預設\&lt;comment>10分鐘\&lt;/comment>.

- 需要值

### `--interval`， `-i`

時間間隔。 預設為範圍的除法。 您可以指定單位：小時(h)、分鐘(m)或秒(s)。 最小\&lt;comment>1分鐘\&lt;/comment>.

- 需要值

### `--to`

結束時間。 預設為現在。

- 需要值

### `--latest`， `-1`

僅顯示最新的單一資料點

- 預設： `false`
- 不接受值

### `--service`， `-s`

依服務或應用程式名稱篩選%或*字元可當作萬用字元。

- 預設： `[]`
- 需要值

### `--type`

依服務型別篩選（如果未提供 — 服務）。 不需要版本。 %或*字元可作為萬用字元使用。

- 預設： `[]`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄： timestamp*、service*、used*、limit*、%*、type （* =預設欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `mount:download`

使用rsync從掛載下載檔案

```bash
magento-cloud mount:download [-a|--all] [-m|--mount MOUNT] [--target TARGET] [--source-path] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--all`， `-a`

從所有掛載下載

- 預設： `false`
- 不接受值

### `--mount`， `-m`

掛載（作為應用程式相對路徑）

- 需要值

### `--target`

檔案將下載到的目錄。 如果 — all已使用，則會附加掛載路徑

- 需要值

### `--source-path`

使用 — all時，請使用掛載的來源路徑（而非掛載路徑）作為目標的子目錄

- 預設： `false`
- 不接受值

### `--delete`

是否要刪除目標目錄中的無關檔案

- 預設： `false`
- 不接受值

### `--exclude`

要從下載排除的檔案（模式）

- 預設： `[]`
- 需要值

### `--include`

不排除的檔案（模式）

- 預設： `[]`
- 需要值

### `--refresh`

是否要重新整理快取

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--worker`

背景工作名稱

- 需要值

### `--instance`， `-I`

例項ID

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `mount:list`

取得掛載清單

```bash
magento-cloud mounts [--paths] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--paths`

僅輸出掛載路徑（每行一個）

- 預設： `false`
- 不接受值

### `--refresh`

是否要重新整理快取

- 預設： `false`
- 不接受值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄：定義、路徑。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--worker`

背景工作名稱

- 需要值

### `--instance`， `-I`

例項ID

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `mount:size`

檢查掛載的磁碟使用量

```bash
magento-cloud mount:size [-B|--bytes] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--bytes`， `-B`

以位元組為單位顯示大小

- 預設： `false`
- 不接受值

### `--refresh`

重新整理快取

- 預設： `false`
- 不接受值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用欄： available、max、mounts、percent_used、sizes、used。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--worker`

背景工作名稱

- 需要值

### `--instance`， `-I`

例項ID

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `mount:upload`

使用rsync將檔案上傳到掛載

```bash
magento-cloud mount:upload [--source SOURCE] [-m|--mount MOUNT] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--source`

包含要上傳之檔案的目錄

- 需要值

### `--mount`， `-m`

掛載（作為應用程式相對路徑）

- 需要值

### `--delete`

是否要刪除掛載中的無關檔案

- 預設： `false`
- 不接受值

### `--exclude`

要從上傳排除的檔案（模式）

- 預設： `[]`
- 需要值

### `--include`

不排除的檔案（模式）

- 預設： `[]`
- 需要值

### `--refresh`

是否要重新整理快取

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--worker`

背景工作名稱

- 需要值

### `--instance`， `-I`

例項ID

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `operation:list`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/>列出環境上的執行階段作業

```bash
magento-cloud ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

不要限制要顯示的命令長度。 預設限製為24行。

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--worker`

背景工作名稱

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄： service*、name*、start*、role、stop （* =預設欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `operation:run`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/>在環境中執行操作

```bash
magento-cloud operation:run [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

作業名稱


### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--worker`

背景工作名稱

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `project:clear-build-cache`

清除專案的建置快取

```bash
magento-cloud project:clear-build-cache [-p|--project PROJECT]
```

### `--project`， `-p`

專案ID或URL

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `project:get`

在本機複製專案

```bash
magento-cloud get [-e|--environment ENVIRONMENT] [--depth DEPTH] [--build] [-p|--project PROJECT] [-i|--identity-file IDENTITY-FILE] [--] [<project>] [<directory>]
```


### `project`

專案ID


### `directory`

要複製的目標目錄。 預設為專案標題


### `--environment`， `-e`

要複製的環境ID。 預設為專案預設值，或第一個可用的環境

- 需要值

### `--depth`

建立淺層複製：限制歷史記錄中的認可數量

- 需要值

### `--build`

複製後建置專案

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `project:info`

讀取或設定專案的屬性

```bash
magento-cloud project:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

屬性的名稱


### `value`

設定屬性的新值


### `--refresh`

是否要重新整理快取

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `project:list`

取得所有使用中專案的清單

```bash
magento-cloud projects [--pipe] [--region REGION] [--title TITLE] [--my] [--refresh REFRESH] [--sort SORT] [--reverse] [--page PAGE] [-c|--count COUNT] [--format FORMAT] [--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--pipe`

輸出專案ID的簡單清單。 停用分頁。

- 預設： `false`
- 不接受值

### `--region`

依區域篩選（完全相符）

- 需要值

### `--title`

依標題篩選（不區分大小寫的搜尋）

- 需要值

### `--my`

僅顯示您擁有的專案

- 預設： `false`
- 不接受值

### `--refresh`

是否要重新整理清單

- 預設： `1`
- 需要值

### `--sort`

排序依據的屬性

- 預設： `title`
- 需要值

### `--reverse`

以反向（遞減）順序排序

- 預設： `false`
- 不接受值

### `--page`

頁碼。 無論設定或 — count為何，這都能啟用分頁。 如果指定了 — pipe，則忽略。

- 需要值

### `--count`， `-c`

每頁要顯示的專案數目。 使用0停用分頁。 若指定 — page，則忽略。

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`

要顯示的欄。 可用的資料欄：id*、title*、region*、created_at、organization_id、organization_label、organization_name、status （* =預設資料欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `project:set-remote`

設定目前Git存放庫的遠端專案

```bash
magento-cloud set-remote [<project>]
```


### `project`

專案ID


### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `repo:cat`

讀取專案存放庫中的檔案

```bash
magento-cloud repo:cat [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] <path>
```


### `path`

檔案的路徑

- 必填

### `--commit`， `-c`

認可SHA。 這也可以接受父項認可的「HEAD」，以及插入符號(^)或波狀符號(~)尾碼。

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `repo:ls`

列出專案存放庫中的檔案

```bash
magento-cloud repo:ls [-d|--directories] [-f|--files] [--git-style] [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

子目錄的路徑


### `--directories`， `-d`

僅顯示目錄

- 預設： `false`
- 不接受值

### `--files`， `-f`

僅顯示檔案

- 預設： `false`
- 不接受值

### `--git-style`

類似於「git ls-tree」的樣式輸出

- 預設： `false`
- 不接受值

### `--commit`， `-c`

認可SHA。 這也可以接受父項認可的「HEAD」，以及插入符號(^)或波狀符號(~)尾碼。

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `repo:read`

讀取專案存放庫中的目錄或檔案

```bash
magento-cloud read [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

目錄或檔案的路徑


### `--commit`， `-c`

認可SHA。 這也可以接受父項認可的「HEAD」，以及插入符號(^)或波狀符號(~)尾碼。

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `route:get`

檢視路由的詳細資訊

```bash
magento-cloud route:get [--id ID] [-1|--primary] [-P|--property PROPERTY] [--refresh] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<route>]
```


### `route`

路由的原始URL


### `--id`

要選取的路由ID

- 需要值

### `--primary`， `-1`

選取主要路由

- 預設： `false`
- 不接受值

### `--property`， `-P`

要顯示的屬性

- 需要值

### `--refresh`

略過路由的快取

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

[已棄用的選項，不再使用]

- 需要值

### `--identity-file`， `-i`

[已棄用的選項，不再使用]

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `route:list`

列出環境的所有路由

```bash
magento-cloud routes [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<environment>]
```


### `environment`

環境ID


### `--refresh`

略過路由的快取

- 預設： `false`
- 不接受值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄： route*、type*、to*、url （* =預設欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `self:install`

安裝或更新CLI組態檔

```bash
magento-cloud self:install [--shell-type SHELL-TYPE]
```

### `--shell-type`

自動完成的殼層型別（bash或zsh）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `self:update`

將CLI更新至最新版本

```bash
magento-cloud update [--no-major] [--unstable] [--manifest MANIFEST] [--current-version CURRENT-VERSION] [--timeout TIMEOUT]
```

### `--no-major`

只在次要版本或修補程式版本之間更新

- 預設： `false`
- 不接受值

### `--unstable`

更新至不穩定的新版本（如果有的話）

- 預設： `false`
- 不接受值

### `--manifest`

覆寫資訊清單檔案位置

- 需要值

### `--current-version`

覆寫目前版本

- 需要值

### `--timeout`

版本檢查的逾時

- 預設： `30`
- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `service:list`

列出專案中的服務

```bash
magento-cloud services [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

是否要重新整理快取

- 預設： `false`
- 不接受值

### `--pipe`

僅輸出服務名稱清單

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄：磁碟、名稱、大小、型別。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `service:mongo:dump`

從MongoDB建立資料的二進位封存傾印

```bash
magento-cloud mongodump [-c|--collection COLLECTION] [-z|--gzip] [-o|--stdout] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`， `-c`

要傾印的集合

- 需要值

### `--gzip`， `-z`

使用gzip壓縮傾印

- 預設： `false`
- 不接受值

### `--stdout`， `-o`

輸出到STDOUT而非檔案

- 預設： `false`
- 不接受值

### `--relationship`， `-r`

要使用的服務關係

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `service:mongo:export`

從MongoDB匯出資料

```bash
magento-cloud mongoexport [-c|--collection COLLECTION] [--jsonArray] [--type TYPE] [-f|--fields FIELDS] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`， `-c`

要匯出的集合

- 需要值

### `--jsonArray`

將資料匯出為單一JSON陣列

- 預設： `false`
- 不接受值

### `--type`

匯出型別，例如&quot;csv&quot;

- 需要值

### `--fields`， `-f`

要匯出的欄位

- 預設： `[]`
- 需要值

### `--relationship`， `-r`

要使用的服務關係

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `service:mongo:restore`

將資料的二進位封存傾印還原到MongoDB

```bash
magento-cloud mongorestore [-c|--collection COLLECTION] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`， `-c`

要還原的集合

- 需要值

### `--relationship`， `-r`

要使用的服務關係

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `service:mongo:shell`

使用MongoDB殼層

```bash
magento-cloud mongo [--eval EVAL] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--eval`

將JavaScript片段傳遞至Shell

- 需要值

### `--relationship`， `-r`

要使用的服務關係

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `service:redis-cli`

存取Redis CLI

```bash
magento-cloud redis [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<args>]
```


### `args`

要新增到Redis命令的引數


### `--relationship`， `-r`

要使用的服務關係

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `snapshot:create`

建立環境的快照

```bash
magento-cloud backup [--live] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

環境


### `--live`

即時備份：請勿停止環境。 如果設定，這將讓環境在執行中，並在備份期間開啟連線。 這樣可以減少停機時間，同時冒著備份狀態不一致的資料的風險。

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `snapshot:delete`

刪除環境快照

```bash
magento-cloud snapshot:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

快照識別碼。 在非互動模式中是必要的。


### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `snapshot:get`

檢視環境快照

```bash
magento-cloud snapshot:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

快照識別碼。 預設為最近一個。


### `--property`， `-P`

要顯示的屬性。

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `snapshot:list`

列出環境的可用快照

```bash
magento-cloud snapshots [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `snapshot:restore`

還原環境快照

```bash
magento-cloud snapshot:restore [--target TARGET] [--branch-from BRANCH-FROM] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<snapshot>]
```


### `snapshot`

快照的名稱。 預設為最近一個


### `--target`

要還原的環境。 預設為快照的目前環境

- 需要值

### `--branch-from`

如果 — target尚不存在，這會指定新環境的父系

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `source-operation:list`

列出環境上的來源作業

```bash
magento-cloud source-ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

不要限制要顯示的命令長度。 預設限製為24行。

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄：應用程式、命令、作業。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `source-operation:run`

執行來源作業

```bash
magento-cloud source-operation:run [--variable VARIABLE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

作業名稱


### `--variable`

作業期間要設定的變數，格式為\&lt;info>type：name=value\&lt;/info>

- 預設： `[]`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `ssh-cert:load`

產生SSH憑證

```bash
magento-cloud ssh-cert:load [--refresh-only] [--new] [--new-key]
```

### `--refresh-only`

如有必要，請只重新整理憑證（不寫入SSH設定）

- 預設： `false`
- 不接受值

### `--new`

強制重新整理憑證

- 預設： `false`
- 不接受值

### `--new-key`

[已棄用] 使用 — 改用新增

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `ssh-key:add`

新增SSH金鑰

```bash
magento-cloud ssh-key:add [--name NAME] [--] [<path>]
```


### `path`

現有SSH公開金鑰的路徑


### `--name`

用於識別金鑰的名稱

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `ssh-key:delete`

刪除SSH金鑰

```bash
magento-cloud ssh-key:delete [<id>]
```


### `id`

要刪除的SSH金鑰ID


### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `ssh-key:list`

取得帳戶中的SSH金鑰清單

```bash
magento-cloud ssh-keys [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄： id*、title*、path*、指紋（* =預設欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `subscription:info`

讀取或修改訂閱屬性

```bash
magento-cloud subscription:info [-s|--id ID] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<property>] [<value>]
```


### `property`

屬性的名稱


### `value`

設定屬性的新值


### `--id`， `-s`

訂閱ID

- 需要值

### `--date-fmt`

日期格式（作為PHP日期格式字串）

- 預設： `c`
- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `tunnel:close`

關閉SSH通道

```bash
magento-cloud tunnel:close [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--all`， `-a`

關閉所有通道

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `tunnel:info`

檢視SSH通道的關係資訊

```bash
magento-cloud tunnel:info [-P|--property PROPERTY] [-c|--encode] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--property`， `-P`

要檢視的關係屬性

- 需要值

### `--encode`， `-c`

以base64編碼的JSON輸出

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `tunnel:list`

列出SSH通道

```bash
magento-cloud tunnels [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--all`， `-a`

檢視所有通道

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄： port*、project*、environment*、app*、relationship*、url （* =預設欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `tunnel:open`

開啟應用程式關係的SSH通道

```bash
magento-cloud tunnel:open [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--gateway-ports`， `-g`

允許遠端主機連線到本機轉送的連線埠

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `tunnel:single`

開啟與應用程式關聯的單一SSH通道

```bash
magento-cloud tunnel:single [--port PORT] [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

本機連線埠

- 需要值

### `--gateway-ports`， `-g`

允許遠端主機連線到本機轉送的連線埠

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--app`， `-A`

遠端應用程式名稱

- 需要值

### `--relationship`， `-r`

要使用的服務關係

- 需要值

### `--identity-file`， `-i`

要使用的SSH身分識別（私密金鑰）

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `user:add`

將使用者新增至專案

```bash
magento-cloud user:add [-r|--role ROLE] [--force-invite] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

使用者的電子郵件地址


### `--role`， `-r`

使用者的專案角色（「管理員」或「檢視者」）或環境型別角色（例如「staging：contributor」或「production：viewer」）。 若要從環境型別中移除使用者，請將角色設定為「無」。 %或*字元可作為環境型別的萬用字元，例如&#39;%：viewer&#39;，為所有型別賦予使用者「檢視者」角色。 角色可縮寫，例如「production：v」。

- 預設： `[]`
- 需要值

### `--force-invite`

傳送邀請，即使已傳送邀請

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `user:delete`

從專案刪除使用者

```bash
magento-cloud user:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <email>
```


### `email`

使用者的電子郵件地址

- 必填

### `--project`， `-p`

專案ID或URL

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `user:get`

檢視使用者的角色

```bash
magento-cloud user:get [-l|--level LEVEL] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [-r|--role ROLE] [--] [<email>]
```


### `email`

使用者的電子郵件地址


### `--level`， `-l`

角色層級（「專案」或「環境」）

- 需要值

### `--pipe`

將角色輸出到stdout （進行任何變更後）

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--role`， `-r`

[已棄用：使用user：update變更使用者的角色]

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `user:list`

列出專案使用者

```bash
magento-cloud users [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄：email*、name*、role*、id*、granted_at、updated_at （* =預設欄）。 字元「+」可作為預設欄的預留位置。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `user:update`

更新專案上的使用者角色

```bash
magento-cloud user:update [-r|--role ROLE] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

使用者的電子郵件地址


### `--role`， `-r`

使用者的專案角色（「管理員」或「檢視者」）或環境型別角色（例如「staging：contributor」或「production：viewer」）。 若要從環境型別中移除使用者，請將角色設定為「無」。 %或*字元可作為環境型別的萬用字元，例如&#39;%：viewer&#39;，為所有型別賦予使用者「檢視者」角色。 角色可縮寫，例如「production：v」。

- 預設： `[]`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `variable:create`

建立變數

```bash
magento-cloud variable:create [-u|--update] [-l|--level LEVEL] [--name NAME] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--prefix PREFIX] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<name>]
```


### `name`

變數名稱


### `--update`， `-u`

如果變數已存在，請更新變數

- 預設： `false`
- 不接受值

### `--level`， `-l`

設定變數的等級（「專案」或「環境」）

- 需要值

### `--name`

變數名稱

- 需要值

### `--value`

變數的值

- 需要值

### `--json`

變數值是否為JSON格式

- 預設： `false`
- 需要值

### `--sensitive`

變數值是否區分大小寫

- 預設： `false`
- 需要值

### `--prefix`

變數名稱的前置詞，可決定其型別，例如「env」。 僅適用於名稱尚未包含首碼時。 （例如「無」或「環境：」）

- 預設： `none`
- 需要值

### `--enabled`

是否應在環境中啟用變數

- 預設： `true`
- 需要值

### `--inheritable`

變數是否可由子環境繼承

- 預設： `true`
- 需要值

### `--visible-build`

變數在建置時是否應顯示

- 需要值

### `--visible-runtime`

變數是否應在執行階段顯示

- 預設： `true`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `variable:delete`

刪除變數

```bash
magento-cloud variable:delete [-l|--level LEVEL] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

變數名稱

- 必填

### `--level`， `-l`

變數層級（「專案」、「環境」、「p」或「e」）

- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `variable:get`

檢視變數

```bash
magento-cloud vget [-P|--property PROPERTY] [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--pipe] [--] [<name>]
```


### `name`

變數的名稱


### `--property`， `-P`

檢視單一變數屬性

- 需要值

### `--level`， `-l`

變數層級（「專案」、「環境」、「p」或「e」）

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--pipe`

[已棄用的選項] 僅輸出變數值

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `variable:list`

清單變數

```bash
magento-cloud variables [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--level`， `-l`

變數層級（「專案」、「環境」、「p」或「e」）

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄：is_enabled、level、name、value。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `variable:update`

更新變數

```bash
magento-cloud variable:update [--allow-no-change] [-l|--level LEVEL] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

變數名稱

- 必填

### `--allow-no-change`

如果未提供變更，則傳回成功（零退出代碼）

- 預設： `false`
- 不接受值

### `--level`， `-l`

變數層級（「專案」、「環境」、「p」或「e」）

- 需要值

### `--value`

變數的值

- 需要值

### `--json`

變數值是否為JSON格式

- 預設： `false`
- 需要值

### `--sensitive`

變數值是否區分大小寫

- 預設： `false`
- 需要值

### `--enabled`

是否應在環境中啟用變數

- 預設： `true`
- 需要值

### `--inheritable`

變數是否可由子環境繼承

- 預設： `true`
- 需要值

### `--visible-build`

變數在建置時是否應顯示

- 需要值

### `--visible-runtime`

變數是否應在執行階段顯示

- 預設： `true`
- 需要值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--no-wait`， `-W`

請勿等待作業完成

- 預設： `false`
- 不接受值

### `--wait`

等候作業完成（預設）

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值


## `worker:list`

取得所有已部署背景工作程式的清單

```bash
magento-cloud workers [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

是否要重新整理快取

- 預設： `false`
- 不接受值

### `--pipe`

僅輸出工作者名稱清單

- 預設： `false`
- 不接受值

### `--project`， `-p`

專案ID或URL

- 需要值

### `--environment`， `-e`

環境識別碼。 使用「。」 以選取專案的預設環境。

- 需要值

### `--format`

輸出格式：table、csv、tsv或plain

- 預設： `table`
- 需要值

### `--columns`， `-c`

要顯示的欄。 可用的欄：命令、名稱、型別。 %或*字元可作為萬用字元使用。 值可能會以逗號（例如「a，b，c」）和/或空白字元分割。

- 預設： `[]`
- 需要值

### `--no-header`

不要輸出表格標頭

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示此說明訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--yes`， `-y`

對確認問題回答「是」；接受其他問題的預設值；停用互動

- 預設： `false`
- 不接受值

### `--no-interaction`

請勿詢問任何互動式問題；接受預設值。 等同於使用環境變數： \&lt;comment>Magento_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- 預設： `false`
- 不接受值

