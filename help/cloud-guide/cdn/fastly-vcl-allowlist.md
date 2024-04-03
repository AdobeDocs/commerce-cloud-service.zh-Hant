---
title: 允許要求的自訂VCL
description: 使用Fastly Edge ACL清單和自訂VCL程式碼片段，篩選傳入的請求並允許透過IP位址存取Adobe Commerce網站。
feature: Cloud, Configuration, Security
exl-id: a6ee958a-c3d3-47be-b2df-510707f551fc
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# 允許要求的自訂VCL

您可以使用Fastly Edge ACL清單搭配自訂VCL程式碼片段，篩選傳入的請求並允許IP位址存取。 ACL清單指定要允許的IP位址。

建立允許清單來限制對測試環境的存取，以便只允許來自指定之IP位址的請求，提供給內部開發人員和核准的外部服務。 您也可以建立允許清單，以安全地存取中繼和生產環境上的Admin。

下列範例說明如何將自訂VCL程式碼片段搭配 [Fastly存取控制清單(ACL)](https://docs.fastly.com/guides/access-control-lists/about-acls) 保護對雲端基礎結構專案環境上Adobe Commerce管理員的存取權。 當您將自訂VCL片段新增到雲端環境時，Fastly只允許來自ACL中包含的IP位址的請求。

>[!TIP]
>
>對於不應公開存取的測試和整合環境，請使用中可用的HTTP存取控制選項 [[!DNL Cloud Console]](../project/overview.md#access-the-project-web-interface) 管理整個網站的IP位址存取權。

**先決條件：**


{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- 要包含在允許清單中的使用者端IP位址清單

## 建立邊緣ACL以允許使用者端IP位址

Edge ACL會建立IP位址清單，用於管理對您網站的存取。 在此範例中，您會建立Edge ACL，並新增允許存取專案環境管理員的使用者端IP位址清單。

{{admin-login-step}}

1. 按一下 **商店** >設定> **設定** > **進階** > **系統**.

1. 展開 **完整頁面快取** > **Fastly設定** > **邊緣ACL**.

1. 建立ACL容器：

   - 按一下 **新增ACL**.

   - 在 *ACL容器* 頁面，輸入 **ACL名稱**—`allowlist`.

   - 選取 **變更後啟動** 將變更部署至您正在編輯的Fastly服務設定版本。

   - 按一下 **上傳** 以將ACL附加至您的Fastly服務設定。

1. 新增允許存取管理員的IP位址清單：

   - 按一下的「設定」圖示 `allowlist` ACL。

   - 新增並儲存 *IP值* 每個使用者端IP位址。

   - 按一下 **取消** 以返回系統設定頁面。

1. 按一下 **儲存設定**.

1. 根據頁面頂端的通知重新整理快取。

## 建立自訂VCL程式碼片段以保障管理員存取權

以下自訂VCL程式碼片段代碼（JSON格式）顯示邏輯，用於篩選送給管理員的請求，以及在使用者端IP位址符合 `allowlist` ACL。

```json
{
  "name": "allowlist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ((req.url ~ \"^/admin\") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 \"Forbidden\"; }"
}
```

早於 [建立自訂程式碼片段](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-allowlist.html#add-the-custom-vcl-snippet) 從此範例中，檢閱值以決定您是否需要進行任何變更。 然後在個別欄位中輸入每個值，例如 `type` 到「型別」欄位中， `content` 到「內容」欄位。

- `name` — VCL程式碼片段的名稱。 在此範例中， `allowlist`.

- `priority`  — 決定VCL程式碼片段何時執行。 優先順序為 `5` 立即執行並檢查管理員請求是否來自允許的IP位址。 此程式碼片段會在任何預設MagentoVCL程式碼片段之前執行(`magentomodule_*`)已指派優先順序50。 視您希望程式碼片段執行的時間而定，將每個自訂程式碼片段的優先順序設定為高於或低於50。 優先順序較低的程式碼片段會先執行。

- `type`  — 指定將程式碼片段插入版本化VCL程式碼中的位置。 此VCL為 `recv` 將程式碼片段新增至 `vcl_recv` 副程式位於預設Fastly VCL程式碼下方，以及任何物件上方。

- `content`  — 要執行的VCL程式碼片段。 在此範例中，代碼會篩選對管理員的請求，並允許使用者端IP位址符合以下位置中的位址時允許存取： `allowlist` ACL。 如果位址不符，則會以封鎖要求 `403 Forbidden` 錯誤。

  如果您管理員的URL已變更，請取代範例值 `/admin` 以及您環境的URL。 例如， `/company-admin`.

在程式碼範例中，條件 `!req.http.Fastly-FF` 使用時很重要 [來源遮蔽](fastly-custom-cache-configuration.md#configure-back-ends-and-origin-shielding). 請勿移除或編輯此程式碼。

檢閱並更新您環境的程式碼後，請使用下列其中一種方法，將自訂VCL程式碼片段新增至您的Fastly服務設定：

- [從管理員新增自訂VCL程式碼片段](#add-the-custom-vcl-snippet). 如果您可以存取Admin，則建議使用此方法。 (需要 [Magento2 1.2.58版的Fastly CDN模組](fastly-configuration.md#upgrade) 或更新版本。)

- 將JSON程式碼範例儲存至檔案(例如 `allowlist.json`)和 [使用Fastly API上傳](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). 如果您無法存取Admin，請使用此方法。

## 新增自訂VCL片段

{{admin-login-step}}

1. 按一下 **商店** >設定> **設定** > **進階** > **系統**.

1. 展開 **完整頁面快取** > **Fastly設定** > **自訂VCL程式碼片段**.

1. 按一下 **建立自訂程式碼片段**.

1. 新增VCL程式碼片段值：

   - **名稱** — `allowlist`

   - **型別** — `recv`

   - **優先順序** — `5`

   - 新增 **VCL** 程式碼片段內容：

     ```conf
     if ((req.url ~ "^/admin") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
     ```

1. 按一下 **建立** 產生具有名稱模式的VCL程式碼片段檔案 `type_priority_name.vcl`，例如 `recv_5_allowlist.vcl`

1. 重新載入頁面後，按一下 **將VCL上傳到Fastly** 在 *Fastly設定* 區段，以將檔案新增到Fastly服務設定。

1. 上傳完成後，請根據頁面頂端的通知重新整理快取。

Fastly會在上傳過程中驗證VCL程式碼的更新版本。 如果驗證失敗，請編輯自訂VCL程式碼片段以修正問題。 然後，再次上傳VCL。

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
