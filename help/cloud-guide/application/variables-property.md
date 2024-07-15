---
title: 變數屬性
description: 使用variables屬性自訂 [!DNL Commerce] 應用程式的存放區組態選項。
feature: Cloud, Configuration
exl-id: 5cd92fbb-8bff-48b1-9658-500140591344
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# 變數屬性

您可以使用應用程式型環境變數來自訂商店設定。 這些變數使用特定語法。 請參閱&#x200B;_組態指南_&#x200B;中的[覆寫組態設定](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html)。

[!DNL Commerce]應用程式的特定版本需要`.magento.app.yaml`檔案中包含的下列環境變數。

Adobe Commerce 2.2.x至2.3.x的必要專案：

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```

若為Adobe Commerce 2.4.x，請設定下列變數：

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```
