---
title: 管理員變數
description: 請參閱在雲端基礎結構上安裝Adobe Commerce時使用的環境變數清單。
feature: Cloud, Configuration, Install, Roles/Permissions
role: Developer
exl-id: 2829a9dc-40bb-4665-886e-a56d98468fc1
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# 管理員變數

對雲端基礎結構專案具有Adobe Commerce管理存取許可權的使用者可以使用以下專案環境變數覆寫管理使用者帳戶的組態設定，以存取管理UI。

## 管理員認證

您可以在安裝Commerce期間使用下表中的ADMIN變數覆寫管理員使用者憑證。

如果您想在安裝後變更值，請使用SSH連線至您的環境並使用Adobe Commerce CLI [`admin:user` 命令](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) 以建立或編輯管理員使用者認證。

| 變數 | 預設 | 說明 |
| -------------- | --------------------------- | ----------- |
| `ADMIN_USERNAME` | 授權擁有者電子郵件地址 | 管理員使用者的使用者名稱，可建立其他使用者，包括管理員使用者。 |
| `ADMIN_EMAIL` |                             | 管理使用者的電子郵件地址。 此位址用於傳送密碼重設通知。 |
| `ADMIN_PASSWORD` |                             | 管理使用者的密碼。 建立專案時，會產生隨機密碼並傳送電子郵件給授權所有者。 在專案建立期間，授權擁有者應該已經變更密碼。 請連絡授權擁有者，以取得更新的密碼。 |
| `ADMIN_LOCALE` | `en_US` | 管理員使用的預設地區設定。 |

## 管理員URL

使用以下環境變數來保護對管理員UI的存取。 若指定，此值會在安裝期間覆寫預設URL。

`ADMIN_URL` — 存取管理員UI的相對URL。 預設URL為 `/admin`. 基於安全考量，Adobe建議您變更預設為不容易猜測的唯一自訂管理員URL。

### 變更管理員URL

Adobe建議您在安裝後變更Admin URL的環境層級變數。 基於安全考量，在從複製的分支之前設定此設定 `master` 環境。 所有分支，建立自： `master` 分支會繼承環境層級變數及其值。

使用 `magento-cloud variable:update` 命令以更新變數值。 (此 `variable:set` 命令已棄用，無法使用。) 以下範例會將ADMIN_URL更新為 `newAdmin_A8v10`：

```bash
magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master
```

>[!NOTE]
>
>此 `ADMIN_URL` 值接受字母（a-z或A-Z）、數字(0-9)和底線字元(_)作為自訂管理路徑。 空格或其他字元為 **非** 已接受。

**若要使用[!DNL Cloud Console]**：

1. 登入 [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. 從中選擇專案 _所有專案_ 清單。

1. 在專案概述中，選取環境並按一下設定圖示。

   ![專案設定](../../assets/icon-configure.png){width="36"}

1. 選取 **變數** 標籤。

1. 按一下 **建立變數**.

1. 輸入下列內容：

   - **變數名稱** = `ADMIN_URL`
   - **值** =新URL。 例如，將管理員URL設為 `magento_A8v10`.

   根據預設， `Available during runtime` 和 `Make inheritable` 已選取。

1. 按一下 **建立變數** 並等候部署完成。 只有在必填欄位包含值時，才會顯示此按鈕。
