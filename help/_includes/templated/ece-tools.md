---
source-git-commit: 6d8c082d78259f8f7adb0fb7f11ff4fcdb234124
workflow-type: tm+mt
source-wordcount: '4030'
ht-degree: 0%

---
# ece-tools

<!-- The template to render with above values -->
**版本**：2002.1.18

此參照包含34個命令，這些命令可透過 `ece-tools` 命令列工具。
初始清單會使用 `ece-tools list` 在雲端基礎結構上的Adobe Commerce執行命令。

>[!NOTE]
>
>此參考是從應用程式程式碼基底產生的。 若要變更內容，您可以更新中對應命令實施的原始碼 [程式碼基底](https://github.com/magento/magento-cloud-cli) 存放庫並提交您的變更以供檢閱。 另一種方式是 _提供意見反應_ （尋找右上方的連結）。 如需貢獻准則，請參閱 [程式碼協助撰寫](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `_complete`

提供殼層完成建議的內部命令

```bash
ece-tools _complete [-s|--shell SHELL] [-i|--input INPUT] [-c|--current CURRENT] [-a|--api-version API-VERSION] [-S|--symfony SYMFONY]
```

### `--shell`， `-s`

殼層型別(「bash」、「fish」、「zsh」)

- 需要值

### `--input`， `-i`

輸入權杖的陣列（例如COMP_WORDS或argv）

- 預設： `[]`
- 需要值

### `--current`， `-c`

游標所在的「輸入」陣列索引（例如COMP_CWORD）

- 需要值

### `--api-version`， `-a`

完成指令碼的API版本

- 需要值

### `--symfony`， `-S`

已棄用

- 需要值

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `build`

建置應用程式。

```bash
ece-tools build
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `completion`

傾印殼層完成指令碼

```bash
ece-tools completion [--debug] [--] [<shell>]
```


### `shell`

如果未指定shell型別（例如&quot;bash&quot;），則會使用&quot;$SHELL&quot;環境變數的值


### `--debug`

追蹤完成偵錯記錄

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `db-dump`

建立資料庫備份。

```bash
ece-tools db-dump [-d|--remove-definers] [-a|--dump-directory DUMP-DIRECTORY] [--] [<databases>...]
```


### `databases`

用於備份的資料庫。 可用值： [主要報價銷售]. 如果未指定引數值，則會使用儲存在 `MAGENTO_CLOUD_RELATIONSHIP` 環境變數或/和 `stage.deploy.DATABASE_CONFIGURATION` .magento.env.yaml組態檔的屬性。

- 預設： `[]`

- 陣列

### `--remove-definers`， `-d`

從資料庫傾印中移除定義項

- 預設： `false`
- 不接受值

### `--dump-directory`， `-a`

使用替代目錄來儲存傾印

- 需要值

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `deploy`

部署應用程式。

```bash
ece-tools deploy
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `help`

顯示命令的說明

```bash
ece-tools help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

命令名稱

- 預設： `help`


### `--format`

輸出格式（txt、xml、json或md）

- 預設： `txt`
- 需要值

### `--raw`

輸出原始指令說明

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `list`

清單命令

```bash
ece-tools list [--raw] [--format FORMAT] [--short] [--] [<namespace>]
```


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

### `--short`

略過描述命令引數的方式

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `patch`

套用自訂修補程式。

```bash
ece-tools patch
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `post-deploy`

在部署作業之後執行。

```bash
ece-tools post-deploy
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `run`

執行案例。

```bash
ece-tools run <scenario>...
```


### `scenario`

個案例

- 預設： `[]`

- 必填
- 陣列

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `backup:list`

顯示備份檔案的清單。

```bash
ece-tools backup:list
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `backup:restore`

還原重要的組態檔。 執行backup：list以顯示備份檔案的清單。

```bash
ece-tools backup:restore [-f|--force] [--file [FILE]]
```

### `--force`， `-f`

還原備份期間覆寫現有檔案

- 預設： `false`
- 不接受值

### `--file`

特定檔案復原路徑

- 接受值

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `build:generate`

產生建置階段的所有必要檔案。

```bash
ece-tools build:generate
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `build:transfer`

將產生的檔案傳輸到init目錄中。

```bash
ece-tools build:transfer
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `cloud:config:create`

建立 `.magento.env.yaml` 具有指定組建、部署和部署後變數設定的檔案。 覆寫任何現有的 `.magento,.env.yaml` 檔案。

```bash
ece-tools cloud:config:create <configuration>
```


### `configuration`

JSON格式的設定

- 必填

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `cloud:config:update`

更新現有的 `.magento.env.yaml` 具有指定組態的檔案。 建立 `.magento.env.yaml` 如果檔案不存在。

```bash
ece-tools cloud:config:update <configuration>
```


### `configuration`

JSON格式的設定

- 必填

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `cloud:config:validate`

驗證 `.magento.env.yaml` 組態檔

```bash
ece-tools cloud:config:validate
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `config:dump`

靜態內容部署的傾印設定。

```bash
ece-tools config:dump
```


```bash
ece-tools dump
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `cron:disable`

停用所有Magentocron處理序，並終止所有正在執行的處理序。

```bash
ece-tools cron:disable
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `cron:enable`

啟用Magentocron程式。

```bash
ece-tools cron:enable
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `cron:kill`

終止所有Magentocron程式。

```bash
ece-tools cron:kill
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `cron:unlock`

解鎖卡在「執行中」狀態的cron工作。

```bash
ece-tools cron:unlock [--job-code [JOB-CODE]]
```

### `--job-code`

要解除鎖定的Cron工作代碼。

- 預設： `[]`
- 接受多個值

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `dev:generate:schema-error`

從schema.error.yaml檔案產生dist/error-codes.md檔案。

```bash
ece-tools dev:generate:schema-error
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `dev:git:update-composer`

從Git更新部署的撰寫器。

```bash
ece-tools dev:git:update-composer
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `env:config:show`

顯示編碼的雲端設定環境變數。

```bash
ece-tools env:config:show [<variable>...]
```


### `variable`

要顯示的環境變數，可能的選項：服務、路由、變數

- 預設： `[]`

- 陣列

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `error:show`

依錯誤ID顯示錯誤相關資訊或上次部署的所有錯誤相關資訊。

```bash
ece-tools error:show [-j|--json] [--] [<error-code>]
```


### `error-code`

錯誤代碼（如果未傳遞命令），顯示有關上次部署發生的所有錯誤的資訊


### `--json`， `-j`

用於取得JSON格式的結果

- 預設： `false`
- 不接受值

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `module:refresh`

重新整理設定以啟用新新增的模組。

```bash
ece-tools module:refresh
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `schema:generate`

產生結構描述*.dist檔案。

```bash
ece-tools schema:generate
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `wizard:ideal-state`

驗證設定的理想狀態。

```bash
ece-tools wizard:ideal-state
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `wizard:master-slave`

驗證主從配置。

```bash
ece-tools wizard:master-slave
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `wizard:scd-on-build`

驗證組建組態上的SCD。

```bash
ece-tools wizard:scd-on-build
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `wizard:scd-on-demand`

驗證SCD on demand設定。

```bash
ece-tools wizard:scd-on-demand
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `wizard:scd-on-deploy`

驗證部署組態上的SCD。

```bash
ece-tools wizard:scd-on-deploy
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值


## `wizard:split-db-state`

驗證分割DB的能力以及DB是否已分割。

```bash
ece-tools wizard:split-db-state
```

### `--help`， `-h`

顯示指定指令的說明。 當沒有指定命令時，顯示清單命令的說明

- 預設： `false`
- 不接受值

### `--quiet`， `-q`

不輸出任何訊息

- 預設： `false`
- 不接受值

### `--verbose`， `-v|-vv|-vvv`

增加訊息的詳細程度：1代表一般輸出，2代表較詳細輸出，3代表偵錯

- 預設： `false`
- 不接受值

### `--version`， `-V`

顯示此應用程式版本

- 預設： `false`
- 不接受值

### `--ansi`

強制（或停用 — no-ansi） ANSI輸出

- 不接受值

### `--no-ansi`

否定「 — ansi」選項

- 預設： `false`
- 不接受值

### `--no-interaction`， `-n`

請勿詢問任何互動式問題

- 預設： `false`
- 不接受值

