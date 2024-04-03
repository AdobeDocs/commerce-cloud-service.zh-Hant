---
title: 適用於商務的雲端元件
description: 請參閱雲端元件套件最新改良的清單。
recommendations: noDisplay, catalog
exl-id: b4e2508a-3558-4fa8-bae0-3eb76c7b2775
source-git-commit: f9edcc85c14354a2eddacbc5219557e107a367cb
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# 適用於商務的雲端元件

此 [雲端元件](https://github.com/magento/magento-cloud-components) 套件針對雲端基礎結構上部署的網站，提供延伸的Adobe Commerce核心功能。 此套件是ECE-Tools套件的相依性。 本發行說明說明說明說明此套件的最新改善，此套件為的元件 [Cloud Tools Suite for Commerce](cloud-tools-suite.md).

此 `magento/magento-cloud-components` 套件會使用以下版本順序： `<major>.<minor>.<patch>`

發行說明包括：

- ![新圖示](../../assets/new.svg) 新功能
- ![修正圖示](../../assets/fix.svg) 修正和改良

<!--Add release notes below-->

## v1.0.13 {#latest}

發行日期： 2023年3月10日

- ![新圖示](../../assets/new.svg) **PHP 8.2的增強支援** — 已修正某些PHP 8.2.x版本的相容性問題，以支援Commerce 2.4.6。

## v1.0.12

發行日期： 2022年9月13日

- ![修正圖示](../../assets/fix.svg) **熱身時發生錯誤** — 修正嘗試 [熱身](../environment/variables-post-deploy.md#warm_up_pages) 當頁面可見度設定為 [**無法單獨顯示**](https://docs.magento.com/user-guide/system/data-attributes-product.html#simple-product-csv-file-structure) 在Admin中，導致 `ERROR: Warming up failed: <link to page>` 部署記錄檔中有錯誤。<!-- MCLOUD-9134 -->

## v1.0.11

發行日期： 2022年8月4日

- ![修正圖示](../../assets/fix.svg) **新增Symfony 5.4相容性支援** — 修正與Symfony 5.4的相容性。<!-- AC-3550 -->

## v1.0.10

發行日期： 2022年3月10日

- ![新圖示](../../assets/new.svg) **支援PHP 8.1** — 新增對PHP 8.1的支援，並放棄對PHP 7.1的支援。

## v1.0.9

發行日期： 2021年10月25日

- ![修正圖示](../../assets/fix.svg) **更新獨白** — 更新 `monolog` 封裝到 `^2.3`.<!-- ACMP-1263 -->

## v1.0.8

發行日期： 2021年7月29日

- ![修正圖示](../../assets/fix.svg) **從自動產生的URL中移除結尾斜線** — 從快取熱身期間產生的類別頁面URL中移除尾端斜線。<!--MCLOUD-7192-->

## v1.0.7

發行日期： 2020年9月9日

- ![新圖示](../../assets/new.svg) **記錄功能改善** — 縮小 `cache.log` 檔案來改善效能。<!--MCLOUD-6859-->

- ![修正圖示](../../assets/fix.svg) 修正快取設定值中的型別錯誤，此錯誤會導致 `php bin/magento cache:evict` CLI命令失敗。

## v1.0.6

發行日期： 2020年8月5日

- ![新圖示](../../assets/new.svg) **改善Redis效能** — 已新增 `./bin/magento cache:evict` 移除過期Redis金鑰的命令，可減少Redis記憶體使用量以提升效能。<!--MCLOUD-6023-->

- ![修正圖示](../../assets/fix.svg) 已移除的支援 *內容中的New Relic記錄* 修正效能問題。<!--MCLOUD-6422-->

## v1.0.5

發行日期： 2020年6月25日

- ![修正圖示](../../assets/fix.svg) 已修正magento/magento-cloud-components 1.0.4版中匯入的問題，該問題導致排清快取作業在部署階段失敗，並中斷部署流程。

## v1.0.4

發行日期： 2020年6月25日

- ![新圖示](../../assets/new.svg) **在內容中實作New Relic記錄檔**—Adobe Commerce產生的應用程式記錄現在顯示在New Relic中的追蹤中，以改善疑難排解功能。<!--MCLOUD-6029-->

- ![新圖示](../../assets/new.svg) **改善的記錄** — 新增記錄以追蹤快取失效和完整重新索引事件。<!--MCLOUD-6157-->

## v1.0.3

發行日期： 2020年2月27日

- ![修正圖示](../../assets/fix.svg) 修正支援的相容性問題 `ece-tools` 使用舊版PHP的2002.0.x發行版本。

## v1.0.2

發行日期： 2020年2月6日

- ![新圖示](../../assets/new.svg) 擴充的功能 `WARM_UP_PAGES` 環境變數，可支援特定產品頁面的快取預先載入。 請參閱 [部署後變數](../environment/variables-post-deploy.md#warm_up_pages) 主題以瞭解詳細的功能說明。<!--MAGECLOUD-4444-->

- ![修正圖示](../../assets/fix.svg) 修正無效商店URL導致部署後勾點在使用時失敗的問題。 `WARM_UP_PAGES` 填入快取的功能。 此問題僅在URL重寫停用時發生。<!-- MAGECLOUD-4094 -->

## v1.0.1

發行日期： 2019年7月23日

- ![修正圖示](../../assets/fix.svg) 已修正影響 [**WARMUP_PAGE**](../environment/variables-post-deploy.md#warm_up_pages) 使用預設商店URL的功能。 現在，如果 `config:show:default-url` 命令無法擷取基底URL，則會使用MAGENTO_CLOUD_ROUTES變數中的URL。<!-- MAGECLOUD-3866 -->

## v1.0.0

發行日期： 2019年6月12日

這是的初版 [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components) 套件，此為新的相依性 `ece-tools` 套件2002.0.20版和更新版本。

- ![新圖示](../../assets/new.svg) 新增使用規則運算式模式來設定 **WARMUP_PAGE** 環境變數來快取單一頁面、多個網域和多頁面。 另請參閱 [部署後變數](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-3258-->
