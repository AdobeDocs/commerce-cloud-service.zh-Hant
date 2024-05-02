---
title: 設定傳出電子郵件
description: 瞭解如何在雲端基礎結構上為Adobe Commerce啟用傳出電子郵件。
exl-id: 814fe2a9-15bf-4bcb-a8de-ae288fd7f284
source-git-commit: 59f82d891bb7b1953c1e19b4c1d0a272defb89c1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 設定傳出電子郵件

您可以透過為每個環境啟用和停用傳出電子郵件 [!DNL Cloud Console] 或從命令列。 啟用整合和中繼環境的傳出電子郵件，以傳送雙因素驗證或重設雲端專案使用者的密碼電子郵件。

外寄電子郵件預設會在生產和中繼環境中啟用。 不過， [!UICONTROL Enable outgoing emails] 在您設定之前，環境設定中可能會顯示為停用 `enable_smtp` 屬性透過 [命令列](#enable-emails-in-the-cli) 或 [雲端主控台](outgoing-emails.md#enable-emails-in-the-cloud-console).

更新 [!UICONTROL enable_smtp] 屬性值依據 [命令列](#enable-emails-in-the-cli) 也會變更 [!UICONTROL Enable outgoing emails] 在Cloud Console上為此環境設定值。

{{redeploy-warning}}

## 在Cloud Console中啟用電子郵件

使用 **[!UICONTROL Outgoing emails]** 切換至 _設定環境_ 檢視以啟用或停用電子郵件支援。

如果外寄電子郵件必須在Pro Production或Staging環境中停用或重新啟用，您可以提交 [Adobe Commerce支援票證](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

>[!TIP]
>
>Cloud Console上的Pro環境可能不會反映外寄電子郵件狀態。 請改用 [命令列](#enable-emails-in-the-cli) 用於啟用及測試外寄電子郵件。

**若要管理來自的電子郵件支援[!DNL Cloud Console]**：

1. 登入 [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. 從中選擇專案 _所有專案_ 清單。
1. 在「專案」控制面板上，按一下右上方的設定圖示。
1. 按一下 **[!UICONTROL Environments]** 並從清單中選取特定環境。
1. 若要啟用或停用外寄電子郵件，請切換 _啟用外寄電子郵件_ **開啟** 或 **關閉**.

   ![啟用外寄電子郵件設定](../../assets/outgoing-emails.png)

變更設定後，環境會使用新設定進行建置和部署。

## 在CLI中啟用電子郵件

您可以使用變更使用中環境的電子郵件設定 `magento-cloud` CLI `environment:info` 命令以設定 `enable_smtp` 屬性。 啟用SMTP更新 `MAGENTO_CLOUD_SMTP_HOST` 環境變數及其用於傳送郵件之SMTP主機的IP位址。

**若要從命令列管理電子郵件支援**：

1. 在本機工作站上，變更至專案目錄。

1. 檢查環境的傳出電子郵件設定。

   ```bash
   magento-cloud environment:info -e <environment-id> | grep enable_smtp
   ```

1. 透過設定 `enable_smtp` 環境變數至 `true` 或 `false`.

   ```bash
   magento-cloud environment:info --refresh -e <environment-id> enable_smtp true
   ```

   等待環境建置和部署。

1. 使用SSH登入遠端環境。

1. 驗證電子郵件是否有效；傳送測試電子郵件至您可檢查的地址。

   ```bash
   php -r 'mail("mail@example.com", "test message", "just testing", "From: tester@example.com");'
   ```

1. 驗證SendGrid是否擷取電子郵件。

   ```bash
   grep mail@example.com /var/log/mail.log
   ```
