---
title: 設定PayPal付款方法
description: 在雲端基礎結構上為Adobe Commerce設定PayPal付款方法。
feature: Cloud, Checkout, Payments
exl-id: e52fd719-f936-4e8b-8222-af133389d9e2
source-git-commit: aa1a334ca1383559194ca75247679c6fb5411802
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# 設定PayPal付款方法

雲端基礎結構上的Adobe Commerce提供上線工具，以便直接透過管理員設定PayPal Express結帳帳戶。 此工具適用於ECE 2.1.8和更新版本。 為了更妥善地支援上線及測試PayPal付款方法，您可以為沙箱或生產帳戶啟用並設定您的PayPal Express結帳帳戶。

您可以在每個環境中設定沙箱或生產帳戶：

* 針對整合和中繼環境，請設定沙箱認證。
* 針對您的生產環境，設定用於初始測試的沙箱認證，然後以已啟動存放區的即時生產認證取代。

## PayPal帳戶

雖然最好使用已準備並設定的PayPal商家帳戶，但您可以透過「管理員」建立帳戶或升級個人帳戶。

[!DNL PayPal onboarding] 支援與下列帳戶連線：

* PayPal企業帳戶
* PayPal個人帳戶，轉換為商務帳戶。 如果您有現有的個人PayPal帳戶，您可以使用這些憑證登入，並在完成同步處理時將此帳戶升級為商業帳戶。

如果您沒有現有的PayPal帳戶，請建立一個。 輸入新帳戶的電子郵件地址。 如果找不到相符的PayPal帳戶，請依照提示建立PayPal Business帳戶。 或者，您可以直接透過以下方式建立帳戶： [PayPal](https://www.paypal.com/us/webapps/mpp/account-selection).

### PayPal限制

PayPal支援全球各地的PayPal Express Checkout連線，但下列限制除外：

* 印度和日本（未來的PayPal更新可能會支援這些帳戶）
* 以色列

對於巴西，您必須擁有現有的PayPal企業帳戶才能連線。 在此過程中，您無法轉換巴西的現有個人PayPal帳戶。 如果您需要帳戶， [建立企業PayPal帳戶](https://www.paypal.com/us/webapps/mpp/account-selection).

## 設定PayPal Express簽出

若要設定PayPal Express簽出：

1. 存取環境的「管理員」。
1. 在左側導覽中選取 **商店** > **設定**，然後選取 **銷售** > **付款方法**.
1. 若為PayPal，請選取 **設定**. 設定欄位會顯示在「快速結帳」、「廣告PayPal點數」以及「基本」和「進階」設定的可展開區段中。
1. 連線您的PayPal帳戶。 在帳戶連線之前，會停用要啟用的選項。 如需可用和支援帳戶連線的詳細資訊和限制，請參閱 [PayPal帳戶](#paypal-account).

   * 若要連線您的PayPal即時帳戶，請按一下「使用PayPal連線」並依照提示操作。 任何客戶使用即時PayPal購買都會在即時商店中完成並主動向客戶收費。
   * 若要連線您的沙箱帳戶以進行測試，請按一下沙箱憑證，然後遵循提示操作。 客戶使用Sandbox PayPal購買時無需主動向客戶收費，即可完成購買。

1. 設定「快速簽出」設定，驗證並使用PayPal API：

   * **與PayPal商家帳戶相關聯的電子郵件** （選擇性）輸入與您的PayPal商家帳戶相關聯的電子郵件地址。 此電子郵件區分大小寫。
   * **API驗證方法** 作為API簽章或API憑證。
   * 從您的PayPal帳戶擷取的API使用者名稱、密碼和簽名。
   * **沙箱模式** 選取是或否，指出您輸入的認證是否適用於沙箱。 如果您已輸入生產認證，請選取「否」。
   * **api使用Proxy** 如果系統使用Proxy伺服器建立Adobe Commerce與PayPal付款系統之間的連線，請選取「是」或「否」來設定。 如果是，請輸入Proxy主機和連線埠。

1. 如需設定帳戶的詳細資訊和步驟，請參閱 [PayPal Express簽出](https://docs.magento.com/user-guide/payment/paypal-express-checkout.html) 從步驟2開始，完成必要的設定。

設定並驗證帳戶後，您可以在「必要的PayPal設定」下啟用和停用PayPal付款選項：

* **啟用此解決方案** 透過網站向客戶顯示PayPal付款方式。
* **啟用In-Context簽出體驗**
* **啟用PayPal點數** 允許客戶進行PayPal信用融資，不需額外費用。 PayPal會預先支付訂單，並直接與客戶處理信用額度的所有還款。

## paypal變數

在雲端基礎結構上將PayPal上線工具與Adobe Commerce搭配使用時，請將下列變數新增至 `variables:env` 的區段 `magento.app.yaml` 檔案。

```yaml
# Environment variables
variables:
  env:
    CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
```

如果您從2.1.8或更新版本升級至2.2，仍需要新增此變數。
