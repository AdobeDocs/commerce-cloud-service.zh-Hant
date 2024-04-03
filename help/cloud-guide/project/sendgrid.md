---
title: SendGrid電子郵件服務
description: 瞭解雲端基礎結構上適用於Adobe Commerce的SendGrid電子郵件服務，以及如何測試您的DNS設定。
exl-id: 30d3c780-603d-4cde-ab65-44f73c04f34d
source-git-commit: 7c22dc3b0e736043a3e176d2b7ae6c9dcbbf1eb5
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# SendGrid電子郵件服務

SendGrid簡單郵件傳輸通訊協定(SMTP) Proxy服務提供輸出電子郵件驗證和信譽監視服務，包括支援：

* 所有傳出異動電子郵件
* 專用IP位址
* 網域註冊、用於電子郵件網域驗證的DomainKeys Indified Mail (DKIM)簽名（僅適用於Pro測試和生產環境）
* 自訂網域註冊（僅適用於Pro）
* 簡易與專業整合環境的自動化整合。 Pro生產和測試環境需要在基礎建設即服務(IaaS)硬體布建程式期間手動布建和設定

SendGrid SMTP Proxy並非旨在作為一般用途電子郵件伺服器來接收傳入電子郵件，或是用於電子郵件行銷活動。

>[!TIP]
>
>您可以在以下位置找到您帳戶的SendGrid詳細資料： [入門UI](https://cloud.magento.com) 並選取 **專案詳細資訊** > **託管資訊** 標籤。

## 啟用或停用電子郵件

預設情況下，在Pro生產和測試環境中會啟用傳出電子郵件。 此 [!UICONTROL Outgoing emails] 在您設定「 」之前，無論狀態為何，都會在「環境」設定中顯示「 」 `enable_smtp` 屬性。 您可以為其他環境啟用傳出電子郵件，以傳送雙因素驗證電子郵件給Cloud專案使用者。 另請參閱 [設定電子郵件以進行測試](outgoing-emails.md).

## SendGrid控制面板

所有雲端專案都可在中央帳戶下管理，因此只有「支援人員」可以存取SendGrid儀表板。 SendGrid不提供附屬帳戶限制功能。

若要檢閱活動記錄檔的傳送狀態或退回、拒絕或封鎖的電子郵件地址清單， [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). 支援團隊 **無法** 擷取超過30天的活動記錄。

可能的話，請在請求中加入下列資訊：

* 受影響的電子郵件地址
* 有問題的時間範圍（僅限過去30天內）
* 電子郵件的主旨

## DomainKeys識別的郵件(DKIM)

DKIM是一種電子郵件驗證技術，可讓網際網路服務提供者(ISP)識別合法和虛假的寄件者地址，此技術常用於網路釣魚和電子郵件詐騙。 DKIM仰賴管理DNS記錄的網域擁有者。 使用DKIM時，傳送者伺服器會使用私密金鑰來簽署郵件。 此外，網域擁有者會新增經過修改的DKIM記錄 `TXT` 記錄，至傳送者網域的DNS記錄。 這個 `TXT` 記錄包含收件者郵件伺服器用來驗證郵件簽章的公開金鑰。 DKIM公開金鑰加密程式可讓收件者驗證傳送者的真實性。 另請參閱 [說明DKIM記錄](https://docs.sendgrid.com/ui/account-and-settings/dkim-records).

>[!WARNING]
>
>SendGrid DKIM簽章和網域驗證支援僅適用於Pro專案而非Starter。 因此，傳出異動電子郵件可能會被垃圾郵件篩選器標幟。 使用DKIM可改善已驗證電子郵件寄件者的傳送率。 若要改善郵件傳送率，您可以從Starter升級為Pro，或使用您自己的SMTP伺服器或電子郵件傳送服務提供者。 另請參閱 [設定電子郵件連線](https://experienceleague.adobe.com/docs/commerce-admin/systems/communications/email-communications.html) 在 _管理系統指南_.

### 傳送者與網域驗證

若要讓SendGrid代表您從Pro Production或Staging環境傳送交易式電子郵件，您必須設定DNS設定以包含三個SendGrid子網域DNS專案。 每個SendGrid帳戶都會被指派一個唯一 `TXT` 用來驗證傳出電子郵件的記錄。

**若要啟用網域驗證**：

1. 提交 [支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 要求為特定網域啟用DKIM (**僅限Pro測試和生產環境**)。
1. 更新您的DNS設定，使用 `TXT` 和 `CNAME` 支援票證中提供給您的記錄。

**範例 `TXT` 具有帳戶ID的記錄**：

```text
v=spf1 include:u17504801.wl.sendgrid.net -all
```

**範例 `CNAME` 記錄**：

| 網域 | 指向 | 記錄型別 |
| ---------- | ---------- | ------------- |
| em.emaildomain.com | uxxxxxx.wl.sendgrid.net | CNAME |
| s1。_domainkey.emaildomain.com | s1.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |
| s2。_domainkey.emaildomain.com | s2.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |

### DKIM簽名和自動化安全性

設定已驗證的網域時，您可以在自動和手動安全性之間選擇。 如果您選擇自動安全性，SendGrid會自動管理您的DKIM和SPF記錄。 當您新增專屬傳送IP位址至帳戶時，SendGrid會立即更新您的DNS設定和DKIM簽章。 如果您關閉自動安全性，則您有責任在您變更傳送網域時更新DKIM簽名。

**已啟用自動化安全性的範例**：

```text
subdomain.mydomain.com. | CNAME | uxxxxxx.wl.sendgrid.net
s1._domainkey.mydomain.com. | CNAME | s1.domainkey.uxxxxxx.wl.sendgrid.net
s2._domainkey.mydomain.com. | CNAME | s2.domainkey.uxxxxxx.wl.sendgrid.net
```

**已停用自動化安全性的範例**：

```text
me12345.mydomain.com | MX | mx.sendgrid.net
me12345.mydomain.com | TXT | v=spf1 include:sendgrid.net ~all
m1._mydomain.com | TXT | k=rsa; t=s; p=<public-key>
```

設定網域驗證後，SendGrid會自動為您處理安全性原則架構(SPF)和DKIM記錄。 在SendGrid提供 `CNAME` 記錄若要新增至您的DNS記錄，您可以新增專用的IP位址並進行其他帳戶更新，而無需手動管理您的SPF記錄。 另請參閱 [自動化安全性和您的DKIM簽名](https://docs.sendgrid.com/ui/account-and-settings/dkim-records#automated-security-and-your-dkim-signature).

若要測試您的DNS設定：

```terminal
dig CNAME em.domain_name
dig CNAME s1._domainkey.domain_name
dig CNAME s2._domainkey.domain_name
```

## 異動電子郵件臨界值

交易式電子郵件臨界值是指在特定時段內您可從Pro環境傳送的交易式電子郵件訊息數量，例如每月從非生產環境傳送12,000封電子郵件。 此臨界值旨在防止傳送垃圾郵件，並防止可能對您的電子郵件信譽造成損害。

只要寄件者信譽分數超過95%，生產環境中可傳送的電子郵件數量就沒有嚴格限制。 信譽受退回或拒絕的電子郵件數量以及基於DNS的垃圾郵件註冊是否將您的網域標籤為潛在垃圾郵件來源的影響。 另請參閱 [Adobe Commerce上超過SendGrid點數時未傳送電子郵件](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/emails-not-being-sent-sendgrid-credits-exceeded.html) 在 _Commerce支援知識庫_.

**若要檢查是否已超過最大信用額度**：

1. 在本機工作站上，變更至專案目錄。

1. 使用SSH登入遠端環境。

   ```bash
   magento-cloud ssh
   ```

1. 檢查 `/var/log/mail.log` 的 `authentication failed : Maxium credits exceeded` 個專案。

   如果您看到任何 `authentication failed` 記錄專案和 **電子郵件傳送信譽** 最少95個，您可以 [提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 以要求信用額度額度增加。

### 電子郵件傳送信譽

電子郵件傳送信譽是由網際網路服務提供者(ISP)指派給傳送電子郵件訊息之公司的分數。 分數越高，ISP將訊息傳送到收件者收件匣的可能性就越大。 如果分數低於特定等級，ISP可能會將郵件路由到收件者的垃圾郵件資料夾，或甚至完全拒絕郵件。 信譽分數由數個因素決定，例如您的IP位址排名與其他IP位址的30天平均值和垃圾郵件投訴率。 另請參閱 [檢查您傳送信譽的5種方法](https://sendgrid.com/blog/5-ways-check-sending-reputation/).
