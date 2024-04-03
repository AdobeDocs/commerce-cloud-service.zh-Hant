---
title: 勾點屬性
description: 請參閱如何在中設定Hooks屬性的範例 [!DNL Commerce] 應用程式組態檔。
feature: Cloud, Configuration, Build, Deploy
exl-id: d9561f09-5129-4b72-978e-2e3873e8efae
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# 勾點屬性

使用 `hooks` 區段在建置、部署和建置後階段執行殼層命令：

- **`build`** — 執行命令 _早於_ 封裝您的應用程式。 資料庫或Redis等服務無法使用，因為應用程式尚未部署。 新增自訂命令 _早於_ 預設 `php ./vendor/bin/ece-tools` 命令來讓自訂產生的內容繼續進入部署階段。

- **`deploy`** — 執行命令 _晚於_ 封裝及部署您的應用程式。 此時您可以存取其他服務。 由於預設 `php ./vendor/bin/ece-tools` 指令會複製 `app/etc` 目錄至正確的位置，您必須新增自訂指令 _晚於_ 用來防止自訂命令失敗的部署命令。

- **`post_deploy`** — 執行命令 _晚於_ 部署您的應用程式和 _晚於_ 容器開始接受連線。 此 `post_deploy` 勾選會清除快取，並預先載入（加溫）快取。 您可以使用自訂頁面清單 `WARM_UP_PAGES` 中的變數 [部署後階段](../environment/variables-post-deploy.md). 雖然不需要，但這會與 `SCD_ON_DEMAND` 環境變數。

以下範例顯示 `.magento.app.yaml` 檔案。 在底下新增CLI命令 `build`， `deploy`，或 `post_deploy` 區段 _早於_ 此 `ece-tools` 命令：

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        composer install
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    # We run deploy hook after your application has been deployed and started.
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml
    # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

此外，您也可以使用進一步自訂建置階段 `generate` 和 `transfer` 指令來執行特定建置程式碼或移動檔案時的其他動作。

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        php ./vendor/bin/ece-tools build:generate
        # php /path/to/your/script
        php ./vendor/bin/ece-tools build:transfer
```

- `set -e` — 導致掛接在第一個失敗的命令上失敗，而不是在最後一個失敗的命令上失敗。
- `build:generate` — 如果針對建置階段啟用SCD，則套用修補程式、驗證組態、產生DI以及產生靜態內容。
- `build:transfer` — 將產生的程式碼和靜態內容傳輸到最終目的地。

從應用程式執行的命令(`/app`)目錄。 您可以使用 `cd` 變更目錄的指令。 如果掛接中的最終命令失敗，掛接就會失敗。 若要讓它們在第一個失敗的命令上失敗，請新增 `set -e` 到勾點的開頭。

**使用grunt編譯Sass檔案**：

```yaml
dependencies:
    ruby:
        sass: "3.4.7"
    nodejs:
        grunt-cli: "~0.1.13"

hooks:
    build: |
        cd public/profiles/project_name/themes/custom/theme_name
        npm install
        grunt
        cd
        php ./vendor/bin/ece-tools build
```

編譯Sass檔案，使用 `grunt` 靜態內容部署之前（在建置期間發生）。 放置 `grunt` 命令於 `build` 命令。

{{scenarios}}
