---
title: PHP設定
description: 瞭解在雲端基礎結構中用於Commerce應用程式配置的最佳PHP設定。
feature: Cloud, Configuration, Extensions
exl-id: b4180265-f7a1-48e4-8c23-27835253e171
source-git-commit: 94c1e16a07567471d446478e3bd2a33977247ef3
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# PHP設定

您可以選擇 [PHP版本](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) 以在 `.magento.app.yaml` 檔案：

```yaml
name: mymagento
type: php:<version>
```

>[!TIP]
>
>如果升級至PHP 8.1和更新版本，請從 [`runtime: extensions:` 屬性](properties.md#runtime) 在 `.magento.app.yaml` 檔案並重新部署。 JSON擴充功能自PHP 8.0起便安裝在雲端環境中。

## 設定PHP

您可以使用自訂環境的PHP設定 `php.ini` 附加至Adobe Commerce維護之設定的檔案。

在您的存放庫中，新增 `php.ini` 檔案至應用程式的根目錄（儲存庫根目錄）。

>[!TIP]
>
>不正確設定PHP設定可能會導致問題，因此只有進階管理員才應該設定這些選項。

### 增加PHP記憶體限制

若要增加PHP記憶體限制，請將下列設定新增至 `php.ini` 檔案：

```ini
memory_limit = 1G
```

若要進行偵錯，請將值增加到2G。

### 最佳化realpath_cache設定

設定下列專案 `realpath_cache` 改善應用程式效能的設定。

```conf
;
; Increase realpath cache size
;
realpath_cache_size = 10M

;
; Increase realpath cache ttl
;
realpath_cache_ttl = 7200
```

這些設定可讓PHP處理作業快取檔案的路徑，而不是在每個頁面載入時查詢這些路徑。 另請參閱 [效能調整](https://www.php.net/manual/en/ini.core.php) 在PHP檔案中。

>[!NOTE]
>
>如需建議的PHP組態設定清單，請參閱 [必要的PHP設定](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html) 在 _安裝指南_.

### 檢查自訂PHP設定

推送 `php.ini` 雲端環境的變更，您可以檢查自訂PHP設定是否已新增至您的環境。 例如，使用SSH登入遠端環境，並使用類似下列的程式檢視檔案：

```bash
cat /etc/php/<php-version>/fpm/php.ini
```

>[!WARNING]
>
>如果您使用Cloud Docker for Commerce進行本機開發，請參閱 [Docker服務容器](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#fpm-container) 以取得關於使用自訂的資訊 `php.ini` Docker環境中的檔案。

## 啟用擴充功能

您可以在中啟用或停用PHP延伸 `runtime:extension` 區段。 此外，指定的擴展可在Docker PHP容器中使用。

>[!IMPORTANT]
>
>在啟用擴充功能之前，請務必瞭解PHP版本必須與裝載專案的作業系統相容。 您的專案環境可能需要基礎架構團隊升級作業系統，才能繼續。

中的範例 `.magento.app.yaml` 檔案：

```yaml
runtime:
    extensions:
        - sockets
        - sodium
        - ssh2
    disabled_extensions:
        - bcmath
        - bz2
        - calendar
        - exif
```

使用SSH登入環境並列出PHP擴充功能。

```bash
php -m
```

如需有關特定PHP擴充功能的詳細資訊，請參閱 [PHP延伸清單](https://www.php.net/manual/en/extensions.alphabetical.php).

下表顯示在雲端平台上部署Adobe Commerce時支援的PHP擴充功能。

{{$include /help/_includes/templated/php-extensions-cloud.md}}

PHP模組需求與Adobe Commerce版本繫結。 另請參閱 [PHP需求](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html).

### 擴充功能支援

若為Pro專案，下列擴充功能需要額外支援才能安裝：

- `sourceguardian`

例如，若要設定PHP在所有環境中僅執行SourceGuardian保護的指令碼，必須在 `php.ini` 檔案：

```ini
[SourceGuardian]
sourceguardian.restrict_unencoded = "1"
```

另請參閱 [SourceGuardian檔案的第3.5節](https://sourceguardian.com/demofiles/files/SourceGuardian%20for%20Linux%20User%20Manual.pdf). _這是PDF的連結_.

[提交Adobe Commerce支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 以取得在所有生產環境和Pro測試環境中安裝這些PHP擴充功能的協助。 包含您的更新內容 `.magento/services.yaml` 檔案， `.magento.app.yaml` 具有更新的PHP版本和任何其他PHP副檔名的檔案。 若是即時生產環境的變更，您至少必須提供48小時的通知。 雲端基礎結構團隊更新您的專案最多可能需要48小時的時間。

>[!WARNING]
>
>不支援使用偵錯編譯的PHP，而且探查可能與 [!DNL XDebug] 或 [!DNL XHProf]. 啟用Probe時停用這些擴充功能。 探查與某些PHP擴充功能衝突，例如 [!DNL Pinba] 或IonCube。
