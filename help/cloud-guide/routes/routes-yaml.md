---
title: 設定路由
description: 瞭解如何在雲端基礎結構環境中為Adobe Commerce定義傳入HTTPS要求的路由。
feature: Cloud, Configuration, Routes
exl-id: a33797e5-14cc-45eb-a048-96180b872a4a
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# 設定路由

此 `routes.yaml` 中的檔案 `.magento/routes.yaml` directory會定義雲端基礎結構整合、測試和生產環境上Adobe Commerce的路由。 路由決定應用程式如何處理傳入的HTTP和HTTPS要求。

預設 `routes.yaml` file指定在擁有單一預設網域的專案上以及在針對多個網域設定的專案上以HTTPS形式處理HTTP請求的路由範本：

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"
"http://{all}/":
    type: upstream
    upstream: "mymagento:http"
```

使用 `magento-cloud` CLI可檢視已設定路由的清單：

```bash
magento-cloud environment:routes

+-------------------+----------+---------------+
| Route             | Type     | To            |
+-------------------+----------+---------------+
| http://{default}/ | upstream | mymagento     |
+-------------------+----------+---------------+
```

## Pro環境的設定更新

{{pro-self-service-warning}}

## 路由範本

此 `routes.yaml` 檔案是樣板路由及其組態的清單。 您可以在路由範本中使用下列預留位置：

- 此 `{default}` 預留位置代表設定為專案預設值的限定網域名稱。

  例如，具有預設網域的專案 `example.com` 以及下列路由範本：

  ```text
  https://www.{default}/
  https://{default}/blog
  ```

  這些範本會解析為生產環境中的下列URL：

  ```text
  https://www.example.com/
  https://example.com/blog
  ```

- 此 `{all}` 預留位置代表為專案設定的所有網域名稱。

  例如，專案具有 `example.com` 和 `example1.com` 具有下列路由範本的網域：

  ```text
  https://www.{all}/
  
  https://{all}/blog
  ```

  這些範本會針對專案中的所有網域解析為下列路由：

  ```text
  https://www.example.com/
  
  https://www.example1.com/
  
  https://example.com/blog
  
  https://example1.com/blog
  ```

  此 `{all}` 預留位置適合用於針對多個網域設定的專案。 在非生產分支中， `{all}` 會以每個網域的專案ID和環境ID取代。

  如果專案未設定任何網域（這在開發期間很常見），則 `{all}` 預留位置的行為與 `{default}` 預留位置。

Adobe Commerce也會為每個使用中的整合環境產生路由。 對於整合環境， `{default}` 預留位置已取代為下列網域名稱：

```text
[branch]-[per-environment-random-string]-[project-id].[region].magentosite.cloud
```

例如， `refactorcss` 分支 `mswy7hzcuhcjw` 在中託管的專案 `us` 叢集有下列網域：

```text
https://refactorcss-oy3m2pq-mswy7hzcuhcjw.us.magentosite.cloud/
```

>[!NOTE]
>
>如果您的雲端專案支援多個存放區，請遵循以下路徑設定指示 [多個網站或商店](../store/multiple-sites.md).

### 尾隨斜線

路由定義包含尾隨斜線，用以表示資料夾或目錄；不過，相同的內容可以有尾隨斜線或不有尾隨斜線。 下列URL解析的方式相同，但可解譯為 _兩個不同的_ URL：

```text
https://www.example.com/blog/

https://www.example.com/blog
```

>[!TIP]
>
>最佳做法是在目錄中使用結尾斜線，但無論您選擇哪種方法，請務必注意 **保持一致** 以避免產生兩個位置。

## 路由通訊協定

所有環境都會自動支援HTTP和HTTPS。

- 如果設定僅指定HTTP路由，則會自動建立HTTPS路由，允許從HTTP和HTTPS提供網站服務，而不需要重新導向。

  例如，具有預設網域的專案 `example.com` 以及下列路徑範本：

  ```text
  http://{default}/
  ```

  此範本解析至下列URL：

  ```text
  http://example.com/
  
  https://example.com/
  ```

- 如果設定僅指定HTTPS路由，則所有HTTP請求都會重新導向至HTTPS。

  例如，具有預設網域的專案 `example.com` 與下列路由範本：

  ```text
  https://{default}/
  ```

  此範本解析至下列URL：

  ```text
  https://example.com/
  ```

  它也會處理下列重新導向：

  `http://example.com/` ==> `https://example.com/`

透過TLS提供所有頁面。 對於此設定，您必須使用下列其中一種方法，將所有未加密的請求重新導向設定為等效的TLS：

- 將中的通訊協定變更為HTTPS `routes.yaml` 檔案。

  ```yaml
  "https://{default}/":
      type: upstream
      upstream: "mymagento:http"
  "https://{all}/":
      type: upstream
      upstream: "mymagento:http"
  ```

- 對於測試和生產環境，請啟用 [強制Fastly上的TLS](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/redirect-http-to-https-for-all-pages-on-cloud-force-tls.html) Admin UI中的選項。 使用此選項時，Fastly會處理到HTTPS的重新導向，因此您不必更新 `routes.yaml` 設定。

## 路由選項

使用下列屬性分別設定每個路由：

| 屬性 | 說明 |
| ---------------- | ----------- |
| `type: upstream` | 為應用程式提供服務。 此外，它具有 `upstream` 指定應用程式名稱（如中所定義）的屬性 `.magento.app.yaml`)後按一下 `:http` 端點。 |
| `type: redirect` | 重新導向至其他路由。 後面接著 `to` 屬性，這是一個HTTP重新導向，指向由其範本識別的另一個路由。 |
| `cache:` | 控制項 [路由的快取](caching.md). |
| `redirects:` | 控制項 [重新導向規則](redirects.md). |
| `ssi:` | 控制項啟用 [伺服器端包含](server-side-includes.md). |

## 簡單路由

在下列範例中，路由設定會路由Apex網域和 `www` 子網域至 `mymagento` 應用程式。 此路由不會重新導向HTTPS請求。

**範例1：**

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"

"http://www.{default}/":
    type: redirect
    to: "http://{default}/"
```

在此範例中，請求路由會遵循下列規則：

- 伺服器會使用下列URL模式直接回應要求：

  ```text
  http://example.com/path
  ```

- 伺服器發出 _301重新導向_ 適用於具有下列URL模式的請求：

  ```text
  http://www.example.com/mypath
  ```

  這些要求會重新導向至Apex網域，例如：

  ```text
  http://example.com/mypath
  ```

在下列範例中，路由設定不會將URL從www網域重新導向至Apex網域。 相反地，會同時從www和apex網域提供請求。

**範例2：**

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"

"http://www.{default}/":
    type: upstream
    upstream: "mymagento:http"
```

## 萬用字元路由

雲端基礎結構上的Adobe Commerce支援萬用字元路由，因此您可以將多個子網域對應至相同的應用程式。 這適用於重新導向與上游路由。 您以星號(\*)作為路由的前置詞。 例如，下列路由至相同的應用程式：

- `*.example.com`
- `www.example.com`
- `blog.example.com`
- `us.example.com`

這可在即時環境中當成是所有網域。

### 路由未對應的網域

您可以使用點(`.`)以分隔子網域。

**範例：**

具有的專案 `add-theme` 分支路由至下列URL：

```text
http://add-theme-projectID.us.magento.com/
```

如果您定義下列繞線範本：

```text
http://www.{default}/
```

路由解析至下列URL：

```text
http://www.add-theme-projectID.us.magento.com/
```

您可以在點之前插入任何子網域，而且路由會解析。

**範例：**

定義下列路由範本：

```text
http://*.{default}/
```

此範本會解析下列兩個URL：

```text
http://foo.add-theme-projectID.us.magentosite.cloud/
http://bar.add-theme-projectID.us.magentosite.cloud/
```

您可以建立與環境的SSH連線，並使用 `magento-cloud` 列出路由的CLI：

```terminal
web@mymagento.0:~$ vendor/bin/ece-tools env:config:show routes

Magento Cloud Routes:
+------------------------------------------+--------------------------------------------------------------+
| Route configuration                      | Value                                                        |
+------------------------------------------+--------------------------------------------------------------+
| http://www.add-theme-projectID.us.magento.com/:                                                         |
+------------------------------------------+--------------------------------------------------------------+
| primary                                  | false                                                        |
| id                                       | null                                                         |
| attributes                               |                                                              |
| type                                     | upstream                                                     |
| to                                       | mymagento                                                    |
| original_url                             | https:/{default}/                                            |
+------------------------------------------+--------------------------------------------------------------+
| https://*.add-theme-projectID.us.magentosite.cloud/:                                                    |
+------------------------------------------+--------------------------------------------------------------+
| primary                                  | false                                                        |
| id                                       | null                                                         |
| attributes                               |                                                              |
| type                                     | upstream                                                     |
| to                                       | mymagento                                                    |
| original_url                             | https://*.{default}/                                         |
+------------------------------------------+--------------------------------------------------------------+
```

## 重新導向與快取

如中更詳細地討論 [重新導向](redirects.md)，您可以管理複雜的重新導向規則，例如 _部分重新導向_，並指定路由型規則 [快取](caching.md)：

```yaml
https://www.{default}/:
    type: redirect
    to: https://{default}/
https://{default}/:
    cache:
        cookies: [""]
        default_ttl: 0
        enabled: true
        headers:
            - Accept
            - Accept-Language
    ssi:
        enabled: false
    type: upstream
    upstream: mymagento:http
```
