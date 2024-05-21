---
title: Commerce雲端修補程式
description: 請參閱「雲端修補程式」套裝軟體的最新改良專案清單。
recommendations: noDisplay, catalog
last-substantial-update: 2024-05-21T00:00:00Z
exl-id: ae6b511b-a37d-4776-9a5e-ad7d9f9f6611
source-git-commit: 61c42a1bd1d5a28f90b8756032ee6f45be4565b2
workflow-type: tm+mt
source-wordcount: '2208'
ht-degree: 0%

---

# Commerce雲端修補程式

此 [雲端修補程式](https://github.com/magento/magento-cloud-patches) 此套件提供一組必要的修補程式，可改善所有Adobe Commerce版本與雲端環境的整合，並支援快速傳送關鍵修正。

Commerce套件的雲端修補程式相依於ECE-Tools套件，會在您安裝或更新ECE-Tools套件時安裝與更新。 您也可以使用和管理Commerce的雲端修補程式做為獨立的套件，將修補程式套用至不在雲端平台上的Adobe Commerce專案。 以下發行說明說明說明此套裝軟體的最新改善。

>[!TIP]
>
>為確保您的專案具有所有必要的修補程式，請更新至 [最新版本的ece-tools](../dev-tools/update-package.md).

>[!NOTE]
>
>另請參閱 [套用修補程式](../development/apply-patches.md) 以取得將修補程式套用至專案的指示。

此 `magento/magento-cloud-patches` 套件會使用以下版本順序： `<major>.<minor>.<patch>`

<!--Add release notes below-->

## v1.0.27 {#latest}

發行日期： 2024年5月21日

- **支援PHP 8.3** — 此修補程式解決php 8.3與composer套件版本之間的相容性錯誤。

## v1.0.26

發行日期： 2024年4月8日

- ![新圖示](../../assets/new.svg) **PHP**  — 新增對PHP 8.3的支援。

## v1.0.25

發行日期： 2024年1月16日

- **快取改善** — 此修補程式可增強Adobe Commerce 2.4.4版和更新版本的版面快取效率，大幅減少記憶體使用量。<!-- MCLOUD-11514 -->
- **CRON工作改善** — 此修補程式修正了遺失工作不必要等候Adobe Commerce 2.4.4版及更新版本之cron工作鎖定的問題。<!-- MCLOUD-11329 -->

## v1.0.24

發行日期： 2023年9月15日

- **效能提升** — 此修補程式將Adobe Commerce 2.4.6的相同部署設定載入次數減少至2.4.6-p1，藉此修正影響效能的問題<!-- MCLOUD-10604 -->

## v1.0.23

發行日期： 2023年7月31日

- **已移除修補程式MCLOUD-10604** — 此修補程式已移至QPT。<!-- MCLOUD-10736 -->

## v1.0.22

發行日期： 2023年6月19日

- **增強的QPT CLI精靈/輸出** — 在QPT CLI精靈/輸出中新增警告，提醒您確認是否有相依性的修正程式詳細資料和需求。<!-- ACP2E-1963 -->
- **已新增Commerce 2.4.6的修補程式：**
   - 已修正 `regexp cache tag` 驗證。<!-- MCLOUD-10226 -->
   - 透過減少相同部署設定載入的次數來改善效能。<!-- MCLOUD-10604 -->
- **已新增Commerce 2.3.7至2.4.6的修補程式** — 修正導致遞增隨機值，而非針對 `catalog_product_entity_*` 表格。<!-- MCLOUD-10032 -->
- **已新增Commerce 2.4.0至2.4.6的修補程式** — 修正錯誤，指出 `The file can't be deleted. Warning!unlink: No such file or directory`，從管理員排清JS/CSS快取時發生。<!-- MCLOUD-10279 -->

## v1.0.21

發行日期： 2023年3月10日

- **PHP 8.2的增強支援** — 已修正某些PHP 8.2.x版本的相容性問題，以支援Commerce 2.4.6。

## v1.0.20

發行日期： 2022年10月27日

- **新增L2快取改善修補程式** — 此修補程式修正了為Commerce 2.4.0和2.4.1版排清本機L2快取的問題。<!-- MCLOUD-7845 -->

## v1.0.19

發行日期： 2022年9月13日

- **PHP 8.1的增強支援** — 修正某些PHP 8.1.x版本的相容性問題。

## v1.0.18

發行日期： 2022年8月11日

Adobe Commerce 2.4.5的重要修補程式：

- **使用Braintree付款的訂單問題** — 此修補程式解決管理員無法下新訂單或重新訂購的重大問題。<!-- MCLOUD-9137 -->

另請參閱 [啟用Braintree付款時，管理員無法建立訂單/重新訂單](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/admin-cant-create-order-reorder-when-braintree-payment-enabled.html).

## v1.0.17

發行日期： 2022年5月24日

修正中安全性修補程式的限制 `patches.json` 檔案。

## v1.0.16

發行日期： 2022年3月31日

Adobe Commerce 2.3.3-p1及更高版本的重要修補程式：

更新修正程式以解決 **關鍵** 導致未驗證的遠端程式碼執行的漏洞。<!-- MCLOUD-8479 -->

另請參閱 [Adobe安全性公告APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.15

發行日期： 2022年3月10日

- **支援PHP 8.1** — 新增對PHP 8.1的支援，並放棄對PHP 7.0和7.1的支援。
- **新增Adobe Commerce 2.3.3的修補程式** — 修正產品頁面上顯示的貨幣。

## v1.0.14

發行日期： 2022年2月13日

Adobe Commerce 2.3.3-p1及更高版本的重要修補程式：

已新增修補程式以解決 **關鍵** 導致未驗證的遠端程式碼執行的漏洞。<!-- MCLOUD-8461 -->

另請參閱 [Adobe安全性公告APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.13

發行日期： 2021年10月25日

- **更新獨白** — 更新 `monolog` 封裝到 `^2.3`.<!-- ACMP-1263 -->
- **不相容的PHP方法** — 修正Adobe Commerce版本2.4.3和2.3.7-p1不相容的PHP方法。<!-- AC-384 -->
- **PHP錯誤** — 修正 `PHP error 'Undefined variable: errorMessage' ...` 嘗試套用修補程式時發生錯誤。<!-- ACP2E-138 -->

## v1.0.12

發行日期： 2021年8月12日

Adobe Commerce 2.4.3和2.3.7-p1的關鍵修補程式：

- **API速率限制問題** — 此修補程式會更正預設速率限制，該限制會讓Web API無法處理陣列中超過20個專案的請求。 此修補程式會提高速率限制的預設值。 請參閱Adobe Commerce [2.4.3發行說明](https://devdocs.magento.com/guides/v2.4/release-notes/commerce-2-4-3.html#apply-mc-43048__set_rate_limits__243patch-to-address-issue-with-api-rate-limiting) 和 [2.3.7發行說明](https://devdocs.magento.com/guides/v2.3/release-notes/2-3-7-p1.html#apply-mc-43048__set_rate_limits__237-p1patch-to-address-issue-with-api-rate-limiting).<!-- MC-43048 -->

## v1.0.11

發行日期： 2021年7月29日

- **修正套用B2B分層導覽修補程式所造成的問題** — 針對已套用B2B階層式導覽修補程式的客戶，此修正會解決 `Undefined offset` 切換存放區檢視後顯示在「搜尋」頁面上的錯誤。<!--MCLOUD-5287-->

- **Paypal結帳修補程式** — 修正PayPal Express顯示先前下訂單價格的Adobe Commerce 2.3.7問題。<!--MC-42674-->

- **修補程式類別支援** — 新增對處理指派給品質修補程式的修補程式類別和原始來源的支援。 類別可讓客戶使用篩選器和排序，以便在使用時更快找到修補程式 [品質修補工具](https://github.com/magento/quality-patches) 以及全網站分析工具(SWAT)。 <!--MC-38577-->

## v1.0.10

發行日期： 2021年5月10日

- **與Adobe Commerce 2.3.7的相容性** — 解決在Adobe Commerce 2.3.7上安裝的撰寫器相依性衝突。<!--MC-42131-->
- **修正多次套用隨附修補程式所造成的問題** — 多次套用隨附的修補程式（包含其他已棄用的修補程式）可還原隨附的已棄用套裝程式。 所有修補程式現在只會套用一次。 嘗試再次套用相同的套裝軟體時，會顯示已套用修補程式的訊息。<!--MC-41912-->
- **B2B分層導覽修補程式** — 修正另一個問題，該問題導致分層導覽在使用者啟用「B2B共用目錄」時無法顯示所有產品選項。<!--MCLOUD-7742-->

## v1.0.9

發行日期： 2021年2月1日

- **B2B分層導覽修補程式** — 修正啟用「B2B共用目錄」時，階層導覽無法顯示所有產品選項的問題。<!--MCLOUD-6923-->
- **與PHP 7.4的相容性** — 修正PHP 7.4的雲端修補程式相容性問題。<!--MCLOUD-7367-->
- **過時的修補程式會變為可見** — 修正雲端修正程式問題，該問題導致在套用包含已棄用修正程式全部內容的取代修正程式後，已棄用的修正程式會顯示在修正程式表格中。 如果套用的修補程式結合了數個其他修補程式，就可能發生這種情況。<!--MC-40626-->
- **套用修補程式時發生無訊息失敗** — 修正雲端修補程式的問題，此問題會導致 `git apply` 命令在某些環境中無法自動套用修補程式。<!--MC-40529-->

## v1.0.8

發行日期： 2020年10月14日

- **magento/magento-cloud-patches的相容性更新** — 已更新 `symfony` 和 `semver` 中的版本限制 `composer.json` 檔案以與Adobe Commerce 2.4.1和更新版本相容。<!--MCLOUD-7111-->

## v1.0.7

發行日期： 2020年10月14日

- **Adobe Commerce 2.3.0至2.3.5、2.4.0的Redis修補程式** — 更新Redis修補程式，支援在實作2級快取時將產品新增至類別。 <!--MCLOUD-6659-->

- **BraintreeVBE修補程式** — 修正管理員嘗試檢視Braintree結算報告時發生錯誤的問題。 <!--MCLOUD-6684-->

- 現在， `ece-patches apply` 命令使用Unix `patch` 在主機系統上無法使用Git時套用修補程式的命令。 <!--MCLOUD-7069-->

## v1.0.6

發行日期：

- **Adobe Commerce 2.3.0 - 2.3.4的Redis修補程式** — 最佳化通訊並提升效能
   - 縮小Redis和Adobe Commerce之間的網路傳輸規模
   - 修正Redis載入和寫入作業的競爭條件
   - 重寫基底快取配接器以處理儲存時的錯誤
   - 降低Redis CPU耗用量<!--MCLOUD-6139-->

- **Adobe Commerce 2.3.0 - 2.3.5的Redis修補程式** — 改善效能並修正錯誤
   - 修正快取鎖定實作以防止無限鎖定
   - 改善目前的鎖定機制
   - 實作已簽署的鎖定以防止解除鎖定並行請求
   - 修正Redis寫入作業中發生的下列錯誤： `OOM command not allowed when used memory > maxmemory`
   - 修正處理乾淨快取的方式 `cat_p` 在產品更新期間執行的標籤<!--MCLOUD-6110-->

- 修正套用必要專案時發生錯誤的問題 `amzn/amazon-pay-module` 使用Adobe Commerce v2.2.6或2.3.5的Adobe Commerce雲端基礎結構專案上的修補程式，其中不包含此模組。 現在，修補程式會略過 `amzn/amazon-pay-module` 修補程式（若未安裝模組）。<!--MCLOUD-6588-->

## v1.0.5

發行日期： 2020年6月26日

- **Redis效能改善** — 將Redis最佳化功能新增至Adobe Commerce 2.3.3和2.3.4版。這些修正包含在Adobe Commerce 2.3.5版中。 另請參閱 [效能提升](https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-5-commerce.html#performance-boosts) 在 _Adobe Commerce 2.3.5發行說明_.<!--MCLOUD-5771-->

- **New Relic記錄擴充器** — 新增必要的Monolog ProcessorInterface，以支援Commerce 1.0.4版雲端元件中引進的New Relic記錄功能改善。部署Adobe Commerce 2.1.x需要此修補程式。如果未套用修補程式，則建置會在 `di:compile` 程式。<!--MCLOUD-6029-->

## v1.0.4

發行日期： 2020年5月12日

- **Amazon Pay結帳** — 修正Amazon Pay付款Widget的問題，此問題導致客戶無法變更 _稽核與付款_ 結帳程式中的步驟。<!--MCLOUD-5930-->

- **類別頁面上的產品顯示** — 修正導致產品無法在的類別頁面上顯示的問題。 _顯示所有頁面_ 檢視。<!--MCLOUD-5684-->

- **頁面產生器影像上傳** — 修正頁面產生器介面問題，此問題有時會在將影像上傳至影像庫時導致下列錯誤： `Destination folder is not writable or does not exist`<!--MCLOUD-5837-->

- **隱藏不必要的Sitemap產生警告** — 新增在Sitemap產生期間發生錯誤時的重試嘗試，並在可自動復原錯誤的情況下略過客戶電子郵件通知。<!--MCLOUD-3025-->

- **網站效能改善** — 修正的效能問題 `Magento\Framework\App\DeploymentConfig\Reader::load` 會定期經歷影響網站效能的長時間載入。 <!--MCLOUD-5650-->

- 更新付款方式修補程式的修補程式指派，以付款模組為目標，而非Magento基礎套件(magento/magento2-base)，因此只有在付款模組存在時才套用付款修補程式。<!--MCLOUD-5666-->

- 更新修補程式以與Magento Open Source相容。<!--MCLOUD-5701-->

## v1.0.3

發行日期： 2020年4月28日

- 已針對「部署期間已停用FPC」修補程式新增修正，以支援Adobe Commerce 2.3.5。

## v1.0.2

發行日期： 2020年2月27日

此版本包含下列修補程式和重要修正：

- **magento/magento-cloud-patches的相容性更新**

   - 已更新 `symfony` 和 `semver` 中的版本限制 `composer.json` 檔案以與Adobe Commerce 2.4和更新版本相容。<!--MAGECLOUD-5127-->

   - 更新中的限制 `composer.json` 與的相容性 `ece-tools` 2002.0.22和更新版本2002.0.x。

- **PayPal Express簽出** — 此修補程式於2020年2月12日發佈，可解決影響使用PayPal Express Checkout下單的訂單的問題，其中訂單的送貨地址會指定已手動輸入文字欄位中的國家/地區區域，而非從「送貨」頁面的下拉式功能表中選取的區域。 請參閱修正程式下載頁面上的完整修正程式說明。

- **應用程式部署修正** — 已新增修補程式，以修正部署過程中停用完整頁面快取的問題。 此修補程式適用於Adobe Commerce 2.3.2和更新版本。

- **非同步/大量API的範圍引數** — 更新此修補程式，修正 `composer.json` 檔案。 此修補程式適用於Magento Open Source2.3.1和2.3.2。請參閱修正程式下載頁面上的完整修正程式說明。

## v1.0.1

發行日期： 2020年2月6日

我們已包含magento/magento-cloud-patches v1.0.1版中軟體下載頁面上的所有Magento Open Source2.x修補程式。 如果您先前將任何修補程式複製到專案中，請移除它們以避免衝突。

此版本包含下列修補程式和重要修正：

- **修正cron死鎖並改善cron鎖定**—

   - 修正由於中的狀態值不正確，導致部分cron作業無法執行的問題。 `cron_schedule` 表格。 現在，我們使用Adobe Commerce鎖定架構來檢查和更新cron工作狀態，而不是使用 `cron_schedule` 表格。 已結束並出現錯誤狀態的Cron工作會在下次Cron執行時重試，而不是等待24小時。

   - 新增 _重試_ 避免在更新中的資料時發生死結的作業 `cron_schedule` 表格。

- **已更新 `magento/magento-cloud-patches` 包含Magento Open Source2.x的所有可用修補程式** — 更新magento/magento-cloud-patches套件，加入「軟體下載」頁面上提供的所有Magento Open Source2.x修補程式。 如果您先前在雲端基礎結構專案上將任何Magento Open Source修補程式複製到Adobe Commerce，請移除它們以避免衝突。<!--MAGECLOUD-4606-->

- **Elasticsearch目錄分頁修正**  — 以更有效的修正取代magento/magento-cloud-patches v1.0提供的Elasticsearch目錄分頁修補程式。<!--MAGECLOUD-4847-->

- **Page Builder修補程式** — 在Commerce 1.0.0的雲端修補程式中，我們隨附了Page Builder修補程式，以解決已知的Page Builder遠端程式碼執行(RCE)弱點，並根據Adobe Commerce 2.3.3進行初始修正。我們已更新這些修補程式，並根據Adobe Commerce 2.3.4推出更穩定的實作，其中包括修正問題的多項最佳化措施。<!--MAGECLOUD-4884-->

  如果您有magento/magento-cloud-patches 1.0.0套件，仍可防止Page Builder RCE弱點問題。 如果您更新至1.0.1或更新版本，相同修正的實作效果會更好。

## v1.0.0

發行日期： 2019年11月14日

這是的初版 [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) 套件，此為新的相依性 `ece-tools` 套件2002.0.22版或更新版本。

此版本包含下列修補程式和重要修正：

- **2.3.1.x和2.3.2.x版本的Page Builder安全性修補程式** — 修正Page Builder預覽中，未經驗證的使用者可存取某些範本化方法的問題，這些方法可用來透過網路(RCE)觸發任意程式碼執行，進而導致全域資訊洩漏。 將不受支援的頁面產生器版本搭配Adobe Commerce版本2.3.1和2.3.2使用時，可能會發生此問題。<!--MAGECLOUD-4649-->

- **MSI修補程式** — 修正使用預設庫存設定來管理庫存時，導致索引錯誤和效能問題的問題。<!--MAGECLOUD-4428-->

- **新郵件介面的向下相容性** — 修正因下列原因造成的回溯不相容問題： `Magento\Framework\Mail\EmailMessageInterface` Adobe Commerce v2.3.3中引入的PHP介面。在此修補程式的範圍內，新的 `EmailMessageInterface` 繼承自舊的 `MessageInterface`，而Adobe Commerce核心模組將恢復為相依於 `MessageInterface`.<!--MAGECLOUD-4422-->

- **目錄分頁在Elasticsearch6.x上無法運作** — 修正搜尋結果分頁的重要問題，此問題影響使用Elasticsearch6.x做為目錄搜尋引擎的客戶。<!--MAGECLOUD-4448-->
