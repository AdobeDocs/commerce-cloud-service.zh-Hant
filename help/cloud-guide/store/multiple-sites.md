---
title: 設定多個網站或商店
description: 瞭解如何在雲端基礎結構上為Adobe Commerce設定多個網站或商店。
feature: Cloud, Configuration, Routes, Site Navigation
exl-id: 16e932ef-f083-44d7-977f-0c78899e151a
source-git-commit: 85aa54af10e7ea44adde5403b69ff03d4a0c622f
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# 設定多個網站或商店

您可以將Adobe Commerce設定為擁有多個網站或商店，例如英文商店、法文商店和德文商店。 另請參閱 [瞭解網站、商店和商店檢視](best-practices.md#store-views).

>[!WARNING]
>
>目錄資料會隨著您增加網站和商店的數量而擴展。 根據您的專案架構，其他存放區可能會導致非快取型目錄頁面的索引程式較長且回應時間較慢。 Adobe建議您密切監視網站效能。

設定多個存放區的程式取決於您選擇使用唯一或共用網域。

具有唯一網域的多家商店：

```terminal
https://first.store.com/
https://second.store.com/
```

具有相同網域的多個商店：

```terminal
https://store.com/first/
https://store.com/second/
```

>[!TIP]
>
>若要將商店檢視新增至網站基底URL，您不必建立多個目錄。 另請參閱 [將商店程式碼新增至基底URL](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html) 在 _設定指南_.

## 新增網域

自訂網域可以新增到Pro Staging和任何生產環境；它們無法新增到整合環境。

新增網域的程式取決於雲端帳戶的型別：

- 適用於Pro測試與生產

  將新網域新增到Fastly，請參見 [管理網域](../cdn/fastly-custom-cache-configuration.md#manage-domains)，或開啟支援票證以請求協助。 此外，您必須 [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 以請求將新網域新增至叢集。

- 僅供入門級生產使用

  將新網域新增到Fastly，請參見 [管理網域](../cdn/fastly-custom-cache-configuration.md#manage-domains)，或 [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 以請求協助。 此外，您必須將新網域新增到 **網域** 索引標籤中的 [!DNL Cloud Console]： `https://<zone>.magento.cloud/projects/<project-ID>/edit`

## 設定本機安裝

若要設定本機安裝以使用多個存放區，請參閱 [多個網站或商店][config-multiweb] 在 _設定指南_.

成功建立並測試本機安裝以使用多個存放區後，您必須準備整合環境：

1. **設定路由或位置** — 指定Adobe Commerce處理傳入URL的方式

   - [不同網域的路由](#configure-routes-for-separate-domains)
   - [共用網域的位置](#configure-locations-for-shared-domains)

1. **設定網站、商店和商店檢視** — 使用Adobe Commerce管理UI進行設定
1. **修改變數** — 指定 `MAGE_RUN_TYPE` 和 `MAGE_RUN_CODE` 中的變數 `magento-vars.php` 檔案
1. **部署和測試環境** — 部署和測試 `integration` 分支

>[!TIP]
>
>您可以使用本機環境來設定多個網站或商店。 請參閱Cloud Docker指令，以 [設定多個網站或商店](https://developer.adobe.com/commerce/cloud-tools/docker/configure/multiple-sites/).

### Pro環境的設定更新

{{pro-self-service-warning}}

### 設定不同網域的路由

路由會定義如何處理傳入的URL。 多個具有唯一網域的存放區需要您定義 `routes.yaml` 檔案。 您設定路由的方式取決於您想要的網站運作方式。

**在整合環境中設定路由**：

1. 在本機工作站上，開啟 `.magento/routes.yaml` 文字編輯器中的檔案。

1. 定義網域和子網域。 此 `mymagento` 上游值與中的name屬性相同 `.magento.app.yaml` 檔案。

   ```yaml
   "http://{default}/":
       type: upstream
       upstream: "mymagento:http"
   
   "http://<second-site>.{default}/":
       type: upstream
       upstream: "mymagento:http"
   ```

1. 將變更儲存至 `routes.yaml` 檔案。

1. 繼續至 [設定網站、商店和商店檢視](#set-up-websites-stores-and-store-views).

### 設定共用網域的位置

路由設定會定義URL的處理方式， `web` 中的屬性 `.magento.app.yaml` 檔案會定義應用程式向網頁公開的方式。 Web _位置_ 允許傳入請求的更精細度。 例如，如果您的網域為 `store.com`，您可以使用 `/first` （預設網站）和 `/second` 將請求傳送給共用網域的兩個不同存放區。

**設定新網站位置**：

1. 建立根的別名(`/`)。 在此範例中，別名為 `&app` 第3行。

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
   ```

1. 為網站建立傳遞(`/website`)並使用上一步驟中的別名來參照根。

   別名允許 `website` 以從根位置存取值。 在此範例中，網站 `passthru` 為第21行。

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static":
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>": *app
             ...
   ```

**使用不同的目錄設定位置**：

1. 建立根的別名(`/`)和適用於靜態(`/static`)位置。

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/static": &static
               root: "pub/static"
   ```

1. 在下建立網站的子目錄 `pub` 目錄： `pub/<website>`

1. 複製 `pub/index.php` 將檔案移入 `pub/<website>` 目錄並更新 `bootstrap` 路徑(`/../../app/bootstrap.php`)。

   ```
   try {
       require __DIR__ . '/../../app/bootstrap.php';
   } catch (\Exception $e) { 
   ```

1. 為建立傳遞 `index.php` 檔案。

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static": &static
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>":
               <<: *root
               passthru: "<website>/index.php"
           "/<website>/static": *static
             ...
   ```

1. 提交並推送已變更的檔案。

   - `pub/<website>/index.php` (若此檔案位於 `.gitignore`，推送可能需要強制選項)。
   - `.magento.app.yaml`

### 設定網站、商店和商店檢視

在 _管理員UI_，設定您的Adobe Commerce **網站**， **商店**、和 **存放區檢視**. 另請參閱 [在管理員中設定多個網站、商店和商店檢視](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html) 在 _設定指南_.

當您設定本機安裝時，請務必使用管理員提供的相同名稱和程式碼，代表您的網站、商店和商店檢視。 更新「 」時需要這些值 `magento-vars.php` 檔案。

### 修改變數

不要設定NGINX虛擬主機，請傳遞 `MAGE_RUN_CODE` 和 `MAGE_RUN_TYPE` 變數使用 `magento-vars.php` 檔案的根目錄。

**若要使用傳遞變數 `magento-vars.php` 檔案**：

1. 開啟 `magento-vars.php` 文字編輯器中的檔案。

   此 [預設 `magento-vars.php` 檔案](https://github.com/magento/magento-cloud/blob/master/magento-vars.php) 應如下所示：

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   //if (isHttpHost("example.com")) {
   //    $_SERVER["MAGE_RUN_CODE"] = "default";
   //    $_SERVER["MAGE_RUN_TYPE"] = "store";
   //}
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] === $host;
   }
   ```

1. 移動註解 `if` 封鎖，因此它 _晚於_ 此 `function` 區塊且不再註解。

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("example.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "default";
       $_SERVER["MAGE_RUN_TYPE"] = "store";
   }
   ```

1. 將下列值取代為 `if (isHttpHost("example.com"))` 區塊：
   - `example.com` — 使用您的基底URL _網站_
   - `default` — 含您的專屬程式碼 _網站_ 或 _存放區檢視_
   - `store` — 使用下列其中一個值：
      - `website` — 載入 _網站_ 店面
      - `store` — 載入 _存放區檢視_ 店面

   針對使用唯一網域的多個網站：

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("second.store.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "<second-site>";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }elseif (isHttpHost("store.com")){
       $_SERVER["MAGE_RUN_CODE"] = "base";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }
   ```

   針對具有相同網域的多個網站，您必須檢查 _主機_ 和 _URI_：

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("store.com")) {
      $code = "base";
      $type = "website";
   
      $uri = explode('/', $_SERVER['REQUEST_URI']);
      if (isset($uri[1]) && $uri[1] == 'second') {
        $code = '<second-site>';
        $type = 'website';
      }
      $_SERVER["MAGE_RUN_CODE"] = $code;
      $_SERVER["MAGE_RUN_TYPE"] = $type;
   }
   ```

1. 將變更儲存至 `magento-vars.php` 檔案。

### 在整合伺服器上部署和測試

在雲端基礎結構整合環境中將變更推送至您的Adobe Commerce，並測試您的網站。

1. 新增、提交程式碼變更並將其推播至遠端分支。

   ```bash
   git add -A && git commit -m "Implement multiple sites" && git push origin <branch-name>
   ```

1. 等待部署完成。

1. 部署後，在網頁瀏覽器中開啟您的商店URL。

   如果是不重複網域，請使用格式： `http://<magento-run-code>.<site-URL>`

   例如， `http://french.master-name-projectID.us.magentosite.cloud/`

   在共用網域中，請使用格式： `http://<site-URL>/<magento-run-code>`

   例如， `http://master-name-projectID.us.magentosite.cloud/french/`

1. 徹底測試您的網站，並將程式碼合併至 `integration` 分支以供進一步部署。

## 部署至測試與生產

遵循部署流程 [部署到中繼和生產環境](../deploy/staging-production.md). 對於入門和專業環境，您使用 [!DNL Cloud Console] 以跨環境推送程式碼。

Adobe建議先在中繼環境中進行全面測試，然後再推送至生產環境。 在整合環境中變更程式碼，然後再次開始跨環境部署的程式。

<!-- link definitions -->

[config-multiweb]: https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-overview.html
