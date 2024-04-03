---
title: Web屬性
description: 請參閱中如何設定Web屬性的範例 [!DNL Commerce] 應用程式組態檔。
feature: Cloud, Configuration
exl-id: 2ca94908-6fe1-42fd-bc3b-ef2dd473f1bb
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Web屬性

此 `web` 屬性定義應用程式向網頁公開的方式（以HTTP格式）、決定網頁應用程式提供內容的方式，以及透過在每個位置設定規則來控制應用程式容器如何回應傳入的請求 _區塊_. 區塊代表以正斜線(`/`)。

```yaml
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
```

您可以微調 `locations` 使用以下索引鍵值來設定 `locations` 區塊：

| 屬性 | 說明 |
| :--- | :--- |
| `allow` | 提供不符合「規則」的檔案。 預設值= `true` |
| `expires` | 設定要在瀏覽器中快取內容的秒數。 此索引鍵會啟用 `cache-control` 和 `expires` 靜態內容的標頭。 如果未設定此值，則 `expires` 提供靜態內容檔案時，不會包含指示詞和產生的標頭。 A負值1 (`-1`)值不會導致快取，且為預設值。 您可以使用以下單位表示時間值：  `ms` （毫秒）， `s` （秒）， `m` （分鐘）， `h` （小時）， `d` （天）， `w` （周）， `M` （月、30天），或 `y` （年，365天） |
| `headers` | 設定自訂標頭，例如 `X-Frame-Options`，適用於從此位置提供的靜態內容。 |
| `index` | 列出為應用程式提供服務的靜態檔案，例如 `index.html` 檔案。 此索引鍵必須是集合。 唯有當「允許」存取一或多個檔案時，才能使用此功能。 `allow` 或 `rules` 此位置的金鑰。 |
| `rules` | 指定位置的覆寫。 使用規則運算式來比對請求。 如果傳入的請求符合規則，則規則的索引鍵會覆寫對請求的一般處理。 |
| `passthru` | 設定在找不到靜態檔案或PHP檔案時使用的URL。 通常此URL是您應用程式的前端控制器，例如 `/index.php` 或 `/app.php`. |
| `root` | 設定相對於在網頁上公開之應用程式根目錄的路徑。 雲端專案的公用目錄（位置&quot;/&quot;）預設為「pub」。 |
| `scripts` | 允許在此位置載入指令碼。 將值設為 `true` 以允許指令碼。 |

預設設定允許以下專案：

- 從根(`/`)路徑，僅能存取網頁和媒體
- 從 `~/pub/static` 和 `~/pub/media` 路徑，任何檔案都可以存取

以下範例顯示 `.magento.app.yaml` 一組可於網頁存取之位置的檔案，這些位置與  [`mounts` 屬性](properties.md#mounts)：

```yaml
 # The configuration of app when it is exposed to the web.
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
            root: "pub"
            # The front-controller script to send non-static requests to.
            passthru: "/index.php"
            index:
                - index.php
            expires: -1
            scripts: true
            allow: false
            rules:
                \.(css|js|map|hbs|gif|jpe?g|png|tiff|wbmp|ico|jng|bmp|svgz|midi?|mp?ga|mp2|mp3|m4a|ra|weba|3gpp?|mp4|mpe?g|mpe|ogv|mov|webm|flv|mng|asx|asf|wmv|avi|ogx|swf|jar|ttf|eot|woff|otf|html?)$:
                    allow: true
                ^/sitemap(.*)\.xml$:
                    passthru: "/media/sitemap$1.xml"
        "/media":
            root: "pub/media"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/get.php"
        "/static":
            root: "pub/static"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/front-static.php"
            rules:
                ^/static/version\d+/(?<resource>.*)$:
                    passthru: "/static/$resource"
```

>[!NOTE]
>
>此範例顯示雲端專案的預設Web設定，該專案設定為支援單一網域。 對於需要支援多個網站或商店的專案， `web` 設定必須設定為支援共用網域。 另請參閱 [設定共用網域的位置](../store/multiple-sites.md#configure-locations-for-shared-domains).
