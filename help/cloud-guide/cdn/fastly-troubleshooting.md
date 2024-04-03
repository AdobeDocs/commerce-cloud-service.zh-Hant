---
title: Fastly疑難排解
description: 瞭解如何疑難排解和管理Adobe Commerce的Fastly CDN模組和服務。
feature: Cloud, Configuration, Cache, Services
exl-id: e4c47035-cbad-4838-8d44-fa5eaaac42d1
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 0%

---

# Fastly疑難排解

使用以下資訊來疑難排解和管理雲端基礎結構專案環境中Adobe Commerce中用於Magento2的Fastly CDN模組。 例如，您可以調查回應標頭值和快取行為來解決Fastly服務和效能問題。

在Pro生產和中繼環境中，您可以使用 [New Relic記錄](../monitor/log-management.md) 檢視和分析Fastly CDN和WAF記錄檔資料，以疑難排解錯誤和效能問題。

>[!NOTE]
>
>如需有關設定和設定Fastly的資訊，請參閱 [設定Fastly](fastly.md).

## 找到Fastly服務ID

您需要Fastly服務ID才能從管理員設定Fastly，或提交Fastly API請求以進行進階Fastly設定和疑難排解。

如果您的專案環境中啟用了Fastly，則可以從管理員那裡取得服務ID。 另請參閱 [取得Fastly認證](fastly-configuration.md#get-fastly-credentials).

開發人員和進階VCL使用者可以使用自訂VCL來使用Fastly變數擷取服務ID `req.service_id`. 例如，您可以新增 `req.service_id` 至您的VCL中的自訂記錄指示詞，以擷取服務ID值：

```json
log {"syslog"} req.service_id {" my_logging_endpoint_name :: "}
```

您可以在生產和測試環境中使用相同的VCL。 另請參閱 [如何配置vcl_log](https://support.fastly.com/hc/en-us/community/posts/360040447172-How-to-configure-vcl-log).

## 網站效能、清除和快取問題

使用以下清單來識別和疑難排解與雲端基礎結構環境中Adobe Commerce的Fastly服務設定相關的問題。

- **存放區功能表未顯示或運作** — 您可能使用直接連至原始伺服器的連結或臨時連結，而不使用即時網站URL，或您已使用 `-H "host:URL"` 在 [cURL命令](#check-live-site-through-fastly). 如果您略過Fastly前往原始伺服器，主功能表將無法運作，且顯示的標頭不正確，導致瀏覽器端無法快取。

- **上層導覽無法運作** — 頂端導覽仰賴Edge Side Include (ESI)處理，此處理會在您上傳預設MagentoFastly VCL片段時啟用。 如果導覽無法運作， [上傳Fastly VCL](fastly-configuration.md#upload-vcl-to-fastly) 並重新檢查網站。

- **地理位置/GeoIP無法運作** — 預設MagentoFastly VCL片段會將國家/地區代碼附加至URL。 如果國家/地區代碼無法運作， [上傳Fastly VCL](fastly-configuration.md#upload-vcl-to-fastly) 並重新檢查網站。

- **頁面未快取** — 依預設，Fastly不會使用 `Set-Cookies` 標頭。 Adobe Commerce甚至會在可快取的頁面上設定Cookie (TTL > 0)。 預設MagentoFastly VCL會移除可快取頁面上的這些Cookie。 如果頁面沒有快取， [上傳Fastly VCL](fastly-configuration.md#upload-vcl-to-fastly) 並重新檢查網站。

  如果範本中的頁面區塊標示為無法快取，也會發生此問題。 在這種情況下，問題很可能是因為協力廠商模組或擴充功能封鎖或移除Adobe Commerce標頭所造成。 若要解決問題，請參閱 [X-Cache只包含MISS，沒有HIT](#x-cache-contains-only-miss-no-hit).

- **清除請求失敗** — 當您提交清除請求時，Fastly會傳回下列錯誤：

  ```text
  The purge request was not processed successfully.
  ```

  此問題可能是由以下任一問題造成：

   - 雲端基礎結構專案環境上Adobe Commerce的Fastly服務設定中有無效的Fastly認證
   - 自訂VCL程式碼片段中的程式碼無效

  若要解決問題，請參閱 [清除雲端上的Fastly快取時發生錯誤](https://support.magento.com/hc/en-us/articles/115001853194-Error-purging-Fastly-cache-on-Cloud-The-purge-request-was-not-processed-successfully-) 在Adobe Commerce說明中心。

## 來自Fastly的503錯誤

如果Fastly傳回503逾時錯誤，請檢查錯誤記錄檔和503錯誤頁面以找出根本原因。

>[!NOTE]
>
>如果執行大量作業時發生逾時，您可以 [延長管理員的Fastly逾時](fastly-custom-cache-configuration.md#extend-fastly-timeout).

如果您收到503錯誤，請檢視生產或中繼環境錯誤記錄檔和php存取記錄檔，以疑難排解問題。

**檢查錯誤記錄檔的方式**：

- [錯誤記錄](../test/log-locations.md#application-logs)

  ```text
  /var/log/platform/<project-ID>/error.log
  ```

  此記錄檔包含來自應用程式或PHP引擎的任何錯誤，例如 `memory_limit` 或 `max_execution_time exceeded` 錯誤。 如果找不到任何Fastly相關錯誤，請檢查PHP存取記錄。

- PHP存取記錄

  ```text
  /var/log/platform/<project-ID>/php.access.log
  ```

  在記錄中搜尋傳回503錯誤之URL的HTTP 200回應。 如果您找到200回應，表示Adobe Commerce未傳回錯誤頁面。 這表示在超過間隔後可能發生的問題 `first_byte_timeout` 在Fastly服務設定中設定的值。

發生503錯誤時，Fastly會在錯誤和維護頁面上傳回原因。 如果您為新增程式碼，可能無法檢視原因 [自訂回應頁面](fastly-custom-response.md). 若要在預設錯誤頁面上檢視原因代碼，您可以移除自訂錯誤頁面的HTML代碼。

**檢查Fastly 503錯誤頁面**：

{{admin-login-step}}

1. 按一下 **商店** > **設定** > **設定** > **進階** > **系統**.

1. 在右窗格中，展開 **完整頁面快取**.

1. 在 **Fastly設定** 區段，展開 **自訂綜合頁面** 如下圖所示。

   ![自訂503錯誤頁面](../../assets/cdn/fastly-custom-synthetic-pages-edit-html.png)

1. 按一下 **設定HTML**.

1. 移除自訂程式碼。 您可以將它儲存在文字程式中以便稍後再新增。

1. 按一下 **上傳** 將您的更新傳送給Fastly。

1. 按一下 **儲存設定** ，位於頁面頂端。

1. 重新開啟造成503錯誤的URL。 Fastly傳回錯誤頁面，其原因如以下範例所示。

   ![Fastly錯誤](../../assets/cdn/fastly-503-example.png)

## Apex和子網域已與Fastly帳戶相關聯

如果雲端基礎結構專案中Adobe Commerce的頂點網域和子網域已與一個指派的服務ID相關聯的現有Fastly帳戶，您必須更新Fastly設定才能啟動：

- 更新現有Fastly帳戶上的Apex和子網域設定。 另請參閱 [多個Fastly帳戶和指派的網域](fastly.md#domain).

- [啟用和設定Fastly](fastly-configuration.md#enable-fastly-caching) 並完成 [DNS設定](../launch/checklist.md#update-dns-configuration-with-production-settings)

## 驗證或偵錯Fastly服務

您可以測試網站URL並檢查回應中傳回的標頭值，藉此疑難排解雲端基礎結構網站上Adobe Commerce的效能或快取問題。

### 透過Fastly檢查即時網站

使用Fastly API檢查  `Fastly-Magento-VCL-Uploaded` 和 `X-Cache` 從您的即時網站傳回的回應標頭。

Fastly API請求會透過Fastly擴充功能傳遞，以從原始伺服器取得回應。 如果回應傳回錯誤的標頭，請測試 [直接來源伺服器](#bypass-fastly-cache-to-check-adobe-commerce-sites).

**檢查回應標頭的方式**：

1. 在終端機中，使用下列專案 `curl` 用來測試您的即時網站URL的命令：

   ```bash
   curl https://<live URL> -vo /dev/null -H Fastly-Debug:1
   ```

   如果您尚未設定靜態路由或完成線上站台上網域的DNS設定，請使用 `--resolve` 會略過DNS名稱解析的旗標。

   ```bash
   curl -svo /dev/null --resolve '<your_hostname>:443:<IP-address-of-cache-node>' <https-URL>
   ```

   >[!NOTE]
   >
   >若要將此指令與 `--resolve` 選項，您必須透過SSL/TLS憑證使用Fastly啟用TLS，並尋找快取節點的IP位址。

1. 在回應中，驗證 [標頭](#check-cache-hit-and-miss-response-headers) 以確保Fastly正常運作。 您應該會在回應中看到下列不重複標題：

   ```http
   < Fastly-Magento-VCL-Uploaded: yes
   < X-Cache: HIT, MISS
   ```

如果標題的值不正確，請參閱下列資訊：

- [檢查VCL上傳](#fastly-vcl-has-not-been-uploaded)

- [X-Cache只包含MISS，沒有HIT](#x-cache-contains-only-miss-no-hit)

### 略過Fastly快取以檢查Adobe Commerce網站

如果Fastly服務傳回錯誤的標頭，您可以建立VCL程式碼片段，讓您提交繞過Fastly快取的請求。 另請參閱 [略過Fastly快取](fastly-vcl-bypass-to-origin.md).

新增VCL程式碼片段後，請使用cURL命令從指定的IP位址將請求提交至原始伺服器。 然後，檢查回應是否有錯誤。

### 檢查快取命中和未命中的回應標題

確認傳回的回應包含下列資訊：

- 包含 `X-Magento-Tags` 頁首

- 的值 `Fastly-Module-Enabled` 標題為 `Yes` 或專案環境中安裝的Fastly for CDNMagento2模組的版本號碼

- [Cache-Control： max-age](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) 大於0

- [Pragma](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.32) 設定為 `cache`

以下摘錄自cURL命令輸出，顯示 `Pragma`， `X-Magento-Tags`、和 `Fastly-Module-Enabled` 標頭：

```terminal
* STATE: INIT => CONNECT handle 0x600057800; line 1402 (connection #-5000)
* Rebuilt URL to: https://www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud/
* Added connection 0. The cache now contains 1 members
* Trying 192.0.2.31...
* STATE: CONNECT => WAITCONNECT handle 0x600057800; line 1455 (connection #0)

% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* Connected to www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud (54.229.163.31) port 443 (#0)

* STATE: WAITCONNECT => SENDPROTOCONNECT handle 0x600057800; line 1562 (connection #0)
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* ALPN, offering h2

... portion omitted for brevity ...

< Set-Cookie: mage-messages=%5B%5D; expires=Wed, 22-Nov-2017 17:39:58 GMT; Max-Age=31536000; path=/
< Pragma: cache
< Expires: Wed, 23 Nov 2016 17:39:56 GMT
< Cache-Control: max-age=86400, public, s-maxage=86400, stale-if-error=5, stale-while-revalidate=5
< X-Magento-Tags: cb_welcome_popup store cb cb_store_info_mobile cb_header_promotional_bar cb_store_info cb_discount-promo-bar cpg_2 cb_83 cb_81 cb_84 cb_85 cb_86 cb_87 cb_88 cb_89 p5646 catalog_product p5915 p6040 p6197 p6227 p7095 p6109 p6122 p6331 p7592 p7651 p7690
< Fastly-Module-Enabled: yes
< Strict-Transport-Security: max-age=31536000
    < Content-Security-Policy: upgrade-insecure-requests
    < X-Content-Type-Options: nosniff
    < X-XSS-Protection: 1; mode=block
    < X-Frame-Options: SAMEORIGIN
    < X-Platform-Server: i-dff64b52
    <
    * STATE: PERFORM => DONE handle 0x600057800; line 1955 (connection #0)
    * multi_done
      0     0    0     0    0     0      0      0 --:--:--  0:00:02 --:--:--     0
    * Connection #0 to host www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud left intact
```

>[!NOTE]
>
>如需有關點選和遺漏的詳細資訊，請參閱 [瞭解具有受防護服務的快取HIT和MISS標頭](https://docs.fastly.com/guides/performance-tuning/understanding-cache-hit-and-miss-headers-with-shielded-services) 在Fastly檔案中。

### 解決在回應標頭中發現的錯誤

本節提供解決使用Fastly API檢查回應標頭時傳回的錯誤的建議。

#### Fastly模組未啟用

如果Fastly模組未啟用(`Fastly-Module-Enabled: no`)或如果標題遺失， [使用SSH登入](../development/secure-connections.md#connect-to-a-remote-environment) 至專案。 然後，執行下列命令以檢查模組狀態。

```bash
php bin/magento module:status Fastly_Cdn
```

根據傳回的狀態，使用以下指示來更新Fastly設定。

- `Module does not exist` — 如果模組不存在 [安裝與設定](https://github.com/fastly/fastly-magento2/blob/master/Documentation/INSTALLATION.md) 整合分支中Magento2的Fastly CDN模組。 安裝完成後，請啟用並設定模組。 另請參閱 [設定Fastly](fastly-configuration.md).

- `Module is disabled` — 如果Fastly模組已停用，請在 `integration` 分支以啟用它。 然後，將變更推送到「測試」和「生產」。 另請參閱 [管理擴充功能](../store/extensions.md#install-an-extension).

  如果您使用 [設定管理](../store/store-settings.md#configure-store)，檢視 `app/etc/config.php` 將變更推送至生產或預備環境前的設定檔。

  如果模組未啟用(`Fastly_CDN => 0`)中 `config.php` 檔案，刪除檔案，然後執行以下命令進行更新 `config.php` 具有最新的組態設定。

  ```bash
  bin/magento magento-cloud:scd-dump
  ```

#### Fastly VCL尚未上傳

如果Fastly VCL尚未上傳(`Fastly-Magento-VCL-Uploaded`： `false`)，使用 *上傳VCL* 管理員中的選項以上傳它。 另請參閱 [上傳Fastly VCL片段](fastly-configuration.md#upload-vcl-to-fastly).

#### X-Cache只包含MISS，沒有HIT

如果 `X-Cache` 標頭包含 `HIT` (`HIT, HIT` 或 `HIT, MISS`)，表示Fastly成功傳回快取的內容。

如果 `X-Cache` 標題為 `MISS, MISS` 且不包含 `HIT`，執行 `curl` 再次執行命令以確定頁面最近未從快取中清除。

如果您得到相同的結果，請使用 [`curl` 命令](#check-live-site-through-fastly) 並驗證 [回應標頭](#check-cache-hit-and-miss-response-headers)：

- `Pragma` 是 `cache`
- `X-Magento-Tags` 已存在
- `Cache-Control: max-age` 大於0

如果問題仍然存在，其他擴充功能可能會重設這些標題。 在中繼環境中重複下列程式，方法是停用所有擴充功能並重新啟用每個擴充功能，以決定要重設標題的擴充功能。 識別導致問題的擴充功能後，您必須在生產環境中將其停用。

**識別重設回應標題的擴充功能：**

{{admin-login-step}}

1. 瀏覽至 **商店** > **設定** > **設定** > **進階** > **進階**.

1. 在 *停用模組輸出* 區段中，尋找並停用所有擴充功能。

1. 按一下 **儲存設定**.

1. 按一下 **系統** > **工具** > **快取管理**.

1. 按一下 **排清Magento快取**.

1. 對每個擴充功能完成以下步驟，可能會導致Fastly標題問題：

   - 一次啟用一個擴充功能、儲存設定，然後排清Adobe Commerce快取。

   - 執行 [`curl` 命令](#check-live-site-through-fastly) 驗證 [回應標頭](#check-cache-hit-and-miss-response-headers).

   對每個擴充功能重複此程式。 如果Fastly回應標題不再顯示，表示您已識別造成Fastly問題的擴充功能。

在您識別正在重設Fastly標題的擴充功能後，請聯絡擴充功能開發人員以取得其他協助。 我們無法提供修正或更新，讓協力廠商擴充功能可搭配Fastly快取運作。

## 復原Fastly設定

如果自訂VCL片段更新或其他Fastly設定變更導致雲端基礎結構網站上的Adobe Commerce中斷或傳回錯誤，請使用Fastly API [啟用](https://docs.fastly.com/api/config#version_0b79ae1ba6aee61d64cc4d43fed1e0d5) 回覆至較舊VCL版本的指令。 您無法從「管理員」回覆VCL版本。

**回覆VCL版本**：

1. 若要取得服務的可用VCL版本清單，請執行以下命令

   ```bash
   curl -H "Fastly-Key: <FASTLY_API_TOKEN>" -H "Accept: application/json" https://api.fastly.com/service/<FASTLY_SERVICE_ID>/version
   ```

1. 執行下列指令，將作用中的VCL版本變更為指定的版本。

   ```bash
   curl -H "Fastly-Key: <FASTLY_API_TOKEN>" -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -X PUT https://api.fastly.com/service/<FASTLY_SERVICE_ID>/version/<VERSION_ID>/activate
   ```

如需有關使用Fastly API來檢閱和管理VCL的詳細資訊，請參閱 [使用API管理VCL](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
