---
title: 快取
description: 瞭解如何在雲端基礎結構環境中啟用Adobe Commerce的快取。
feature: Cloud, Cache, Routes
exl-id: 4856aa94-2947-4dc8-b0d1-0960869dc39c
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# 快取

您可以在雲端基礎結構專案環境中啟用快取。 如果停用快取，Adobe Commerce會直接提供檔案。

{{route-placeholder}}

## 設定快取

若要啟用應用程式的快取，請在以下位置設定快取規則： `.magento/routes.yaml` 檔案如下所示：

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
        headers: [ "Accept", "Accept-Language", "X-Language-Locale" ]
        cookies: ["*"]
        default_ttl: 60
```

## 路由型快取

為數個路由分別設定快取規則，以啟用微調快取，如下列範例所示：

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true

http://{default}/path/:
    type: upstream
    upstream: php:php
    cache:
        enabled: false

http://{default}/path/more/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
```

上述範例快取下列路由：

- `http://{default}/`
- `http://{default}/path/more/`
- `http://{default}/path/more/etc/`

下列路由為 **非** 快取：

- `http://{default}/path/`
- `http://{default}/path/etc/`

>[!NOTE]
>
>路由中的規則運算式為 **非** 支援。

## 快取持續時間

快取持續時間由以下決定 `Cache-Control` 回應標頭值。 若否 `Cache-Control` 標題在回應中， `default_ttl` 金鑰已使用。

## 快取金鑰

為決定如何快取回應，Adobe Commerce會根據數個因素建立快取金鑰，並儲存與此金鑰相關聯的回應。 當請求帶有相同的快取金鑰時，將重複使用回應。 其用途與HTTP類似 [`Vary` 頁首](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.44).

引數 `headers` 和 `cookies` 金鑰可讓您變更此快取金鑰。

這些鍵的預設值如下：

```yaml
cache:
    enabled: true
    headers: ["Accept-Language", "Accept"]
    cookies: ["*"]
```

## 快取屬性

### `enabled`

當設定為 `true`，啟用此路由的快取。 當設定為 `false`，停用此路由的快取。

### `headers`

定義快取索引鍵必須相依的值。

例如，如果 `headers` 索引鍵如下：

```yaml
cache:
    enabled: true
    headers: ["Accept"]
```

接著Adobe Commerce會針對的每個值快取不同的回應 `Accept` HTTP標頭。

### `cookies`

此 `cookies` key會定義快取索引鍵必須相依的值。

例如：

```yaml
cache:
    enabled: true
    cookies: ["value"]
```

快取金鑰取決於 `value` 請求中的Cookie。

如果符合下列條件，則存在特殊情況： `cookies` 金鑰具有 `["*"]` 值。 此值表示任何具有Cookie的請求都會繞過快取。 這是預設值。

>[!NOTE]
>
>Cookie名稱中不能使用萬用字元。 使用精確的Cookie名稱或比對具有星號(`*`)。 例如， `SESS*` 或 `~SESS` 目前為 **非** 有效值。

Cookie有下列限制：

- 您最多可以設定 **50個Cookie** 在系統中。 否則，應用程式會擲回 `Unable to send the cookie. Maximum number of cookies would be exceeded` 例外。
- Cookie大小的上限為 **4096位元組**. 否則，應用程式會擲回 `Unable to send the cookie. Size of '%name' is %size bytes` 例外。

### `default_ttl`

如果回應沒有 `Cache-Control` 標題， `default_ttl` 索引鍵可用來定義快取持續時間（以秒為單位）。 預設值為 `0`，表示不會快取任何內容。
