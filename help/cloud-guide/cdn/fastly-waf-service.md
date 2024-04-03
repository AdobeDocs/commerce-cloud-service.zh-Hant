---
title: Web應用程式防火牆(WAF)
description: 瞭解Fastly WAF服務如何偵測、記錄並封鎖惡意請求流量，以免損害Adobe Commerce網路或網站。
feature: Cloud, Configuration, Security
exl-id: 40bfe983-7f32-4155-ae77-7cd18866f6e2
source-git-commit: 6b01bf91c3bf63ba268d0f8e10e19db4cb355997
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# Web應用程式防火牆(WAF)

雲端基礎結構上適用於Adobe Commerce的網頁應用程式防火牆(WAF)服務採用Fastly技術，可偵測、記錄並封鎖惡意要求流量，以免損害您的網站或網路。 WAF服務僅適用於生產環境。

WAF服務提供下列優點：

- **PCI法規遵循** — 啟用WAF可確保生產環境中的Adobe Commerce儲存區域符合PCI DSS 6.6安全性需求。
- **預設WAF原則** — 由Fastly設定和維護的預設WAF原則提供量身打造的安全性規則集合，可保護您的Adobe Commerce Web應用程式免受各種攻擊，包括插入攻擊、惡意輸入、跨網站指令碼、資料匯出、HTTP通訊協定違規及其他 [OWASP前十名](https://owasp.org/www-project-top-ten/) 安全性威脅。
- **WAF上線和啟用** — 在布建完成後的2至3週內，Adobe會在您的生產環境中部署並啟用預設的WAF原則。
- **營運與維護支援**—
   - Adobe和Fastly設定並管理您的WAF服務日誌和警示。
   - Adobe會分類與WAF服務問題相關的客戶支援票證，這些問題會封鎖優先順序1問題的合法流量。
   - 自動升級至WAF服務版本，確保可立即涵蓋新的或不斷發展的漏洞利用。 另請參閱 [WAF維護和升級](#waf-maintenance-and-updates).

>[!TIP]
>
>如需在雲端基礎結構存放區維護Adobe Commerce PCI法規遵循的其他資訊，請參閱 [PCI法規遵循](https://business.adobe.com/products/magento/pci-compliance.html).

## 啟用WAF

Adobe可在布建完成後的2至3週內，於新帳戶上啟用WAF服務。 WAF是透過Fastly CDN服務實作。 您不需要安裝或維護任何硬體或軟體。

>[!NOTE]
>
>在使用WAF服務之前，您必須在雲端基礎結構專案上傳送到Adobe Commerce的所有外部流量必須透過Fastly服務路由。 另請參閱 [設定Fastly](fastly-configuration.md).

## 運作方式

WAF服務與Fastly整合，並使用Fastly CDN服務中的快取邏輯來篩選Fastly全域節點的流量。 我們在您的生產環境中啟用WAF服務，預設的WAF原則是根據 [Trustwave SpiderLabs的ModSecurity規則](https://github.com/owasp-modsecurity/ModSecurity) 以及OWASP十大安全性威脅。

WAF服務會針對WAF規則集篩選HTTP和HTTPS流量(GET和POST要求)，並封鎖惡意流量或不遵守特定規則的流量。 此服務只會篩選嘗試重新整理快取的原始繫結流量。 因此，我們會在Fastly快取中停止大多數的攻擊流量，保護原始流量免受惡意攻擊。 若只處理原始流量，WAF服務會保留快取效能，只對每個非快取要求引入估計為1.5毫秒至20毫秒的延遲。

## 疑難排解封鎖的請求

WAF服務啟用時，會根據WAF規則篩選所有網頁和管理程式流量，並封鎖觸發規則的任何網頁請求。 當請求遭到封鎖時，請求者會看到預設值 `403 Forbidden` 包含封鎖事件參考ID的錯誤頁面。

![WAF錯誤頁面](../../assets/cdn/fastly-waf-403-error.png)

您可以從管理員自訂此錯誤回應頁面。 另請參閱 [自訂WAF回應頁面](fastly-custom-response.md#customize-the-waf-error-page).

如果您的Adobe Commerce管理頁面或店面傳回 `403 Forbidden` 錯誤頁面為了回應合法的URL請求，請提交 [Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). 從錯誤回應頁面複製參考ID，並將其貼到票證說明中。

## WAF維護和更新

Fastly會根據商業第三方、Fastly研究和開放來源的規則更新來維護和更新WAF規則集。 Fastly會視需要或當可從其各自的來源取得規則變更時，將發佈的規則更新為原則。 此外，Fastly可以在啟用WAF服務後，將符合規則發佈類別的規則新增到任何服務的WAF執行個體中。 這些更新可確保即時涵蓋新的或不斷演變的利用漏洞。

Adobe和Fastly管理更新流程，以確保新的或修改的WAF規則在您的生產環境中有效運作，然後再以封鎖模式部署更新。

## 限制

由Fastly支援的標準WAF服務不支援下列功能：

- 防範惡意程式碼或降低機器人風險 — 考慮使用 [存取控制清單](./fastly-vcl-allowlist.md) 或協力廠商服務。
- 速率限制 — 請參閱 [速率限制](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md) 在Fastly檔案中，或請參閱 [速率限制](https://developer.adobe.com/commerce/webapi/get-started/rate-limiting/) 在 _Commerce Web API_ 安全性區段。
- 設定客戶的記錄端點 — 請參閱 [PrivateLink服務](../development/privatelink-service.md) 作為替代方案。

雖然WAF服務不允許您根據IP位址封鎖或允許流量，但您可以新增存取控制清單(ACL)和自訂VCL片段到Fastly服務，以指定IP位址和VCL邏輯來封鎖或允許流量。 另請參閱 [自訂Fastly VCL片段](fastly-vcl-custom-snippets.md).

WAF服務不支援篩選TCP、UDP或ICMP要求。 但是，此功能由Fastly CDN服務隨附的內建DDoS保護提供。 另請參閱 [DDoS保護](fastly.md#ddos-protection).
