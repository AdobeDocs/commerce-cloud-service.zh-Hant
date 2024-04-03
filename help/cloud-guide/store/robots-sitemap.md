---
title: 新增網站地圖和搜尋引擎自動機制
description: 瞭解如何在雲端基礎結構上將網站地圖和搜尋引擎機器人新增到Adobe Commerce。
feature: Cloud, Configuration, Search, Site Navigation
exl-id: b98f43fa-1878-466d-8ea0-1e7207af8b60
source-git-commit: ee1db75c73c086e0ea54e1a7591ca7f2b4d2b36d
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# 新增網站地圖和搜尋引擎自動機制

嘗試產生並寫入 `sitemap.xml` 檔案到根目錄會導致下列錯誤：

```terminal
Please make sure that "/" is writable by the web-server.
```

在雲端基礎結構上使用Adobe Commerce，您只能寫入特定目錄，例如 `var`， `pub/media`， `pub/static`，或 `app/etc`. 當您產生 `sitemap.xml` 使用「管理」面板的檔案，您必須指定 `/media/` 路徑。

您不需要產生 `robots.txt` 因為會產生 `robots.txt` 隨選內容並將其儲存在資料庫中。 您可以在瀏覽器中使用檢視內容 `<domain.your.project>/robots.txt` 或 `<domain.your.project>/robots` 連結。

這需要ECE-Tools 2002.0.12版和更新版本 `.magento.app.yaml` 檔案。 請參閱以下檔案中的這些規則範例 [magento-cloud存放庫](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml#L43-L49).

**產生 `sitemap.xml` 2.2版及更新版本中的檔案**：

1. 存取「管理員」。
1. 在 _行銷_ 功能表，按一下 **網站地圖** 在 _SEO與搜尋_ 區段。
1. 在 _網站地圖_ 檢視，按一下 **新增Sitemap**.
1. 在 _新增網站地圖_ 檢視，請輸入下列值：

   - **檔案名稱**：`sitemap.xml`
   - **路徑**：`/media/`

1. 按一下 **儲存並產生**. 新的網站地圖會在 _網站地圖_ 格線。
1. 按一下 _適用於Google的連結_ 欄。

**若要將內容新增至 `robots.txt` 檔案**：

1. 存取「管理員」。
1. 在 _內容_ 功能表，按一下 **設定** 在 _設計_ 區段。
1. 在 _設計組態_ 檢視，按一下 **編輯** 中的網站 _動作_ 欄。
1. 在 _主要網站_ 檢視，按一下 **搜尋引擎自動機制**.
1. 更新 **編輯robots.txt的自訂指令** 欄位。
1. 按一下 **儲存設定**.
1. 驗證 `<domain.your.project>/robots.txt` 檔案或 `<domain.your.project>/robots` 瀏覽器中的URL。

>[!NOTE]
>
>如果 `<domain.your.project>/robots.txt` 檔案產生 `404 error`， [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 以移除重新導向 `/robots.txt` 至 `/media/robots.txt`.

## 使用Fastly VCL程式碼片段重新寫入

如果您有不同的網域，而且需要個別的網站地圖，您可以建立VCL以路由至適當的網站地圖。 產生 `sitemap.xml` 檔案，然後建立自訂Fastly VCL程式碼片段來管理重新導向。 另請參閱 [自訂Fastly VCL片段](../cdn/fastly-vcl-custom-snippets.md).

>[!NOTE]
>
> 您可以從管理員UI或使用Fastly API上傳自訂VCL程式碼片段。 另請參閱 [自訂VCL程式碼片段範例與教學課程](../cdn/fastly-vcl-custom-snippets.md#example-vcl-snippet-code).

### 使用Fastly VCL程式碼片段重新導向

建立自訂VCL程式碼片段來重寫路徑 `sitemap.xml` 至 `/media/sitemap.xml` 使用 `type` 和 `content` 機碼值組。

```json
{
  "name": "sitemapxml_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; }"
}
```

下列範例示範如何重寫的路徑 `robots.txt` 和 `sitemap.xml` 至 `/media/robots.txt` 和 `/media/sitemap.xml`

```json
{
  "name": "sitemaprobots_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; } else if (req.url.path ~ \"^/?robots.txt$\") { set req.url = \"/media/robots.txt\";}"
}
```

**若要針對特定網域重新導向使用Fastly VCL程式碼片段**：

建立 `pub/media/domain_robots.txt` 檔案，其中網域為 `domain.com`，並使用下一個VCL程式碼片段：

```json
{
  "name": "domain_robots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }}"
}
```

VCL程式碼片段路由 `http://domain.com/robots.txt` 並呈現 `pub/media/domain_robots.txt` 檔案。

若要設定的重新導向 `robots.txt` 和 `sitemap.xml` 在單一片段中，建立 `pub/media/domain_robots.txt` 和 `pub/media/domain_sitemap.xml` 檔案，其中網域為 `domain.com` 並使用下一個VCL程式碼片段：

```json
{
  "name": "domain_sitemaprobots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }} else if ( req.url.path == \"/sitemap.xml\" ) { if ( req.http.host ~ \"(domain).com$\" ) {  set req.url = \"/media/\" re.group.1 \"_sitemap.xml\"; }}"
}
```

在 `sitemap` admin config，您必須使用指定檔案的位置 `pub/media/` 而非 `/`.

### 依搜尋引擎設定索引

啟動 `robots.txt` 自訂，您必須啟用 **已開啟搜尋引擎的索引`<environment-name>`** 選項。

![使用 [!DNL Cloud Console] 管理環境](../../assets/robots-indexing-by-search-engine.png)

>[!NOTE]
>
>如果您正在使用PWA Studio且無法存取您已設定的 `robots.txt` 檔案，新增 `robots.txt` 至 [前方名稱允許清單](https://github.com/magento/magento2-upward-connector#front-name-allowlist) 在 **商店** >設定> **一般** > **Web** >向上PWA設定。
