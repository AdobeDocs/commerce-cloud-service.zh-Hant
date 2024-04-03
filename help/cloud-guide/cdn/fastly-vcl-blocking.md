---
title: 封鎖要求的自訂VCL
description: 使用具有自訂VCL程式碼片段的Edge Access Control list (ACL)，依IP位址封鎖傳入要求。
feature: Cloud, Configuration, Security
exl-id: 1f637612-3858-49d0-91f7-9b8823933cc9
source-git-commit: 0e9ace747cc56808108781e42b97c86756089818
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---

# 封鎖要求的自訂VCL

您可以使用適用於Magento2的Fastly CDN模組，以使用您要封鎖的IP位址清單來建立Edge ACL。 然後，您可以將該清單與VCL程式碼片段搭配使用，以封鎖傳入的請求。 此程式碼會檢查傳入要求的IP位址。 如果它符合ACL清單中包含的IP位址，Fastly會封鎖存取您網站的請求並傳回 `403 Forbidden error`. 允許存取所有其他使用者端IP位址。

**先決條件：**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- 要封鎖的使用者端IP位址清單

## 建立封鎖使用者端IP位址的邊緣ACL

您可以建立Edge ACL來定義要封鎖的IP位址清單。 建立ACL之後，您可以在自訂VCL程式碼片段中使用它來管理對測試或生產網站的存取。

透過在兩個環境中建立具有相同名稱的Edge ACL來管理中繼和生產網站的存取權。 VCL程式碼片段程式碼適用於兩種環境。

1. 登入管理員。
1. 瀏覽至 **商店** >設定> **設定** > **進階** > **系統** > **完整頁面快取** > **Fastly設定**.
1. 展開 **邊緣ACL** 區段。
1. 按一下 **新增ACL** 以建立清單。 在此範例中，將清單命名為「blocklist」。
1. 在清單中輸入IP位址值。 所有新增至此清單的使用者端IP位址都會遭到封鎖，無法存取網站。
1. 或者，選取 **已否定** 核取方塊（如果需要）。

您可以在VCL程式碼片段中依名稱參照Edge ACL。

## 建立封鎖清單的自訂VCL

>[!NOTE]
>
>此範例向進階使用者說明如何建立VCL程式碼片段，以設定自訂封鎖規則以上傳到Fastly服務。 您可以使用，根據Adobe Commerce管理員的國家/地區來設定封鎖清單或允許清單 [封鎖](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) Magento2模組可在Fastly CDN中使用的功能。

定義Edge ACL之後，您可以使用它來建立VCL片段，以封鎖對ACL中所指定IP位址的存取。 您可以在測試環境和生產環境中使用相同的VCL程式碼片段，但必須分別將程式碼片段上傳至每個環境。

以下自訂VCL片段代碼（JSON格式）顯示邏輯，用於封鎖使用者端IP位址符合封鎖清單ACL位址的傳入請求。

```json
{
  "name": "blocklist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( client.ip ~ blocklist) { error 403 \"Forbidden\"; }"
}
```

根據此範例建立程式碼片段之前，請檢閱值以判斷是否需要進行任何變更：

- `name`：VCL程式碼片段的名稱。 在此範例中，我們使用名稱 `blocklist`.

- `priority`：決定VCL程式碼片段何時執行。 優先順序為 `5` 立即執行並檢查管理員請求是否來自允許的IP位址。 此程式碼片段會在任何預設MagentoVCL程式碼片段之前執行(`magentomodule_*`)已指派優先順序50。 視您希望程式碼片段執行的時間而定，將每個自訂程式碼片段的優先順序設定為高於或低於50。 優先順序較低的程式碼片段會先執行。

- `type`：指定VCL程式碼片段的型別，用來決定程式碼片段在產生的VCL程式碼中的位置。 在此範例中，我們使用 `recv`，會將VCL程式碼插入 `vcl_recv` 副程式，位於樣板VCL下方及任何物件上方。 請參閱 [Fastly VCL程式碼片段參考](https://docs.fastly.com/api/config#api-section-snippet) 以取得程式碼片段型別清單。

- `content`：要執行的VCL程式碼片段，會檢查使用者端IP位址。 如果IP位在Edge ACL中，則會封鎖它的 `403 Forbidden` 整個網站的錯誤。 允許存取所有其他使用者端IP位址。

檢閱並更新您環境的程式碼後，請使用下列其中一種方法，將自訂VCL程式碼片段新增至您的Fastly服務設定：

- [從管理員新增自訂VCL程式碼片段](#add-the-custom-vcl-snippet). 如果您可以存取Admin，則建議使用此方法。 (需要 [Fastly 1.2.58版](fastly-configuration.md#upgrade-fastly-module) 或更新版本。)

- 將JSON程式碼範例儲存至檔案(例如 `blocklist.json`)和 [使用Fastly API上傳](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). 如果您無法存取Admin，請使用此方法。

## 新增自訂VCL片段

{{admin-login-step}}

1. 按一下 **商店** >設定> **設定** > **進階** > **系統**.

1. 展開 **完整頁面快取** > **Fastly設定** > **自訂VCL程式碼片段**.

1. 按一下 **建立自訂程式碼片段**.

1. 新增VCL程式碼片段值：

   - **名稱** — `blocklist`

   - **型別** — `recv`

   - **優先順序** — `5`

   - 新增 **VCL** 程式碼片段內容：

     ```conf
     if ( client.ip ~ blocklist) { error 403 "Forbidden"; }
     ```

1. 按一下 **建立** 產生具有名稱模式的VCL程式碼片段檔案 `type_priority_name.vcl`，例如 `recv_5_blocklist.vcl`

1. 重新載入頁面後，按一下 **將VCL上傳到Fastly** 在 *Fastly設定* 區段，以將檔案新增到Fastly服務設定。

1. 上傳後，請根據頁面頂端的通知重新整理快取。

Fastly會在上傳過程中驗證VCL程式碼的更新版本。 如果驗證失敗，請編輯自訂VCL程式碼片段以修正問題。 然後，再次上傳VCL。

## 封鎖要求的其他VCL範例

以下範例說明如何使用內嵌條件陳述式而非ACL清單來封鎖請求。

>[!WARNING]
>
>在這些範例中，VCL程式碼會格式化為JSON裝載，可儲存至檔案並以Fastly API請求提交。 您可以提交 [來自管理員的VCL程式碼片段](#add-the-custom-vcl-snippet)，或使用Fastly API做為JSON字串。 若要防止在搭配JSON字串使用Fastly API時進行驗證，您必須使用反斜線來逸出特殊字元。

另請參閱 [使用動態VCL程式碼片段](https://docs.fastly.com/vcl/vcl-snippets/) 在Fastly VCL檔案中。

### VCL程式碼範例：依國家/地區程式碼分塊

此範例針對與IP位址相關聯的國家/地區使用兩個字元的ISO 3166-1國碼。

```json
{
  "name": "blockbycountrycode",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( client.geo.country_code == \"HK\" ) { error 405 \"Not allowed\";}"
}
```

>[!NOTE]
>
>您可以使用Fastly，而不使用自訂VCL程式碼片段 [封鎖](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) 雲端基礎結構管理員中Adobe Commerce的功能，可依國家/地區代碼或國家/地區代碼清單設定封鎖。

### VCL程式碼範例： Block by HTTP User-Agent要求標頭

```json
{
  "name": "blockbyuseragent",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( req.http.User-Agent ~ \"(UCBrowser|MQQBrowser|LieBaoFast|Mb2345Browser)\" ) {error 405 \"Not allowed\";}"
}
```

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
