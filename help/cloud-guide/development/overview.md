---
title: 開發概覽
description: 使用Adobe Commerce在雲端基礎結構專案上準備本機開發。
role: Developer
feature: Cloud, Install
topic: Development
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: d4452d7d-d3dc-4f8d-8bd7-76f05d89f545
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# 開發概覽

雲端基礎結構遠端環境上的Adobe Commerce為 **唯讀**，包括所有入門環境和所有Pro整合、測試和生產環境。 在本機開發環境中，您可以先撰寫及測試程式碼，再將程式碼推送至整合環境，進一步測試並部署到中繼和生產環境。

在準備本機工作區之前，請確定您擁有 [認證](../../get-started/prepare-workspace.md). 本機開發需要安裝PHP和Composer，除非您選擇使用 [Cloud Docker for Commerce](#docker-environment).

## 必要的套件

雲端基礎結構上的Adobe Commerce使用Composer來管理專案的相依性和升級。 對於本機開發，您必須安裝與您的雲端專案相容的PHP和Composer版本。 例如，如果您使用 [!DNL Commerce] 2.4.6雲端範本，您可以看到 [`.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/2.4.6/.magento.app.yaml) 組態檔案使用 **PHP 8.2** 和 **撰寫器2.2.21**.

Composer會在中安裝專案所需的程式庫和相依性 `vendor` 目錄。 下列必要的撰寫器檔案位於專案根目錄中：

- `composer.json` — 使用 `composer.json` 檔案來管理產品的安裝和升級。
- `composer.lock` — 此 `composer.lock` 檔案儲存一組精確的版本相依性，這些相依性滿足專案相依性樹狀結構中每個套件的版本限制。

**常用命令：**

| 命令 | 說明 |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update` | 最新版本的相依性更新反映在 `composer.json` 檔案。 這會更新 `composer.lock` 檔案。 |
| `composer install` | 閱讀 `composer.lock` 檔案以下載相依性。 最佳實務是儲存最新的副本 `composer.lock` 在您的專案存放庫中。 |

{style="table-layout:auto"}

新增、提交和推送更新後的程式碼後，部署程式就會自動執行 `composer install` 命令執行期間 [建置階段](../deploy/process.md#build-phase-build-phase).

### 雲端中繼

雲端基礎結構上的Adobe Commerce使用中繼，此中繼 `magento/product-enterprise-edition`. 若要取得最新版Commerce的最新更新，請使用以下限制語法：

```text
>=current_version <next_version
```

例如，若要使用最新的Adobe Commerce 2.4.5版，請設定 `2.4.5` 作為「目前」版本和 `2.4.6` 作為 `composer.json` 檔案：

```text
"magento/magento-cloud-metapackage": ">=2.4.5 <2.4.6"
```

此中繼封裝的主要封裝如下：

- **vendor/magento/ece-tools** — 此 `ece-tools` 套件與Adobe Commerce 2.1.4版或更新版本相容，提供您可用來在雲端基礎結構專案上管理Adobe Commerce的豐富功能。 它包含雲端基礎結構命令上的指令碼和Adobe Commerce，旨在協助管理您的程式碼並自動建置和部署您的專案。 請參閱 [`ece-tools` 封裝概述](../dev-tools/package-overview.md).
- **廠商/magento/product-enterprise-edition** — 此中繼資料需要應用程式元件，包括模組、架構、主題等。
- **vendor/fastly2/magento2** — 此模組管理Pro測試環境、生產環境和入門生產環境的Fastly CDN和服務。 另請參閱 [Fastly服務](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
- **vendor/magento/module-paypal-on-boarding** — 此模組會連線至您的PayPal商家帳戶，以提供PayPal付款閘道結帳。 另請參閱 [PayPal上線工具](../store/paypal.md).

>[!TIP]
>
>另請參閱 [適用於Adobe Commerce的雲端套件](/help/cloud-guide/release-notes/cloud-packages.md) 在 _Commerce發行說明_ 以取得相依性和第三方授權清單。

## Docker環境

您可以使用Cloud Docker for Commerce工具在本地開發的雲端基礎結構生產和開發環境中模擬Adobe Commerce。 Cloud Docker for Commerce不需要在本機安裝PHP和Composer。

- [使用Cloud Docker進行本機開發](https://developer.adobe.com/commerce/cloud-tools/docker/setup/) 在Adobe Developer網站中
- [Docker架構和常用命令](../dev-tools/cloud-docker.md)
- [Cloud Docker發行說明](../release-notes/cloud-docker.md)

>[!TIP]
>
>如需在雲端基礎結構上搭配Adobe Commerce使用Git型託管服務的相關資訊，請參閱 [整合](../integrations/overview.md).
