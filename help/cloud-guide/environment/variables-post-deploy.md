---
title: 部署後變數
description: 請參閱環境變數清單，這些變數可控制Adobe Commerce在雲端基礎結構部署後階段的動作。
feature: Cloud, Configuration, Cache
recommendations: noDisplay, catalog
role: Developer
exl-id: e460335f-cd2b-4c98-b1ff-32504599b33d
source-git-commit: 8b02757591c4e8f607e936de4eda74d76953d9b7
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# 部署後變數

下列專案 _部署後_ 變數可控制部署後階段的動作，並可繼承和覆寫以下專案的值： [全域變數](variables-global.md). 將這些變數插入 `post-deploy` 的階段 `.magento.env.yaml` 檔案：

```yaml
stage:
  post-deploy:
    POST-DEPLOY_VARIABLE_NAME: value
```

如需自訂建置和部署程式的詳細資訊：

- [部署設定](configure-env-yaml.md)
- [部署流程](../deploy/process.md)

## `TTFB_TESTED_PAGES`

- **預設**— `[]` （空白陣列）
- **版本**—Adobe Commerce 2.1.4和更新版本

設定 _到第一個位元組的時間_ (TTFB)測試指定頁面，以測試您的網站效能。 針對需要測試的每個頁面，指定絕對路徑參照，或具有通訊協定和主機的URL。

```yaml
stage:
  post-deploy:
    TTFB_TESTED_PAGES:
       - "index.php"
       - "index.php/customer/account/create"
       - "https://example.com/catalog/some-category"
```

指定要測試及認可變更的頁面後， _到第一個位元組的時間_ 測試會在部署後階段執行，並針對雲端記錄檔的每個路徑張貼結果：

```terminal
[2019-06-20 20:42:22] INFO: TTFB test result: 0.313s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/customer/account/create","status":200}
[2019-06-20 20:42:22] INFO: TTFB test result: 0.408s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/checkout/cart","status":200}
```

對於重新導向的路徑，記錄會報告重新導向目標的路徑，而非在環境變數中設定的路徑。 如果您指定的路徑無效，記錄會顯示警告訊息。

## `WARM_UP_CONCURRENCY`

- **預設**—_未設定_
- **版本**—Adobe Commerce 2.1.4和更新版本

指定在快取暖機作業期間要傳送的同步要求限制，以減少伺服器負載。 此值會限制平行連線的數量，對於 `WARM_UP_PAGES` post-deploy變數會指定快取預先載入的數個頁面。

```yaml
stage:
  post-deploy:
    WARM_UP_CONCURRENCY: 4
```

## `WARM_UP_PAGES`

- **預設**— `index.php`
- **版本**—Adobe Commerce 2.1.4和更新版本

自訂用來預先載入中快取的頁面清單 `post_deploy` 階段。 您必須設定部署後鉤點。 請參閱 [勾點區段](../application/hooks-property.md) 的 `.magento.app.yaml` 檔案。

- **單次頁面** — 指定要加入快取的單一頁面。 您不需要指定預設基底URL。 下列範例會快取 `BASE_URL/index.php` 頁面：

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - "index.php"
  ```

- **多個網域** — 列出多個URL。 以下範例會從兩個網域快取頁面：

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - 'http://example1.com/test'
        - 'http://example2.com/test'
  ```

- **多頁** — 使用下列格式，根據特定規則運算式模式快取多個頁面：

  ```terminal
  <entity_type>:<pattern|url|product_sku>:<store_id|store_code>
  ```

   - `entity_type`：可能的變體 `category`， `cms-page`， `product`， `store-page`
   - `pattern|url|product_sku`：使用 `regexp` 模式或完全相符 `url` 以篩選URL，或針對所有頁面使用星號(\*)。 將產品SKU用於 `product` 實體型別
   - `store_id|store_code`：使用商店的ID或程式碼或星號(\*)，在所有商店中，您可以傳遞數個以分隔的商店ID或程式碼 `|`

  以下範例快取為 `category` 和 `cms-page` 實體型別基於下列條件：
   - 具有ID之商店的所有類別頁面 `1`
   - 具有程式碼之商店的所有類別頁面 `store1` 和 `store2`
   - 類別頁面 `cars` 適用於含程式碼的存放區 `store_en`
   - cms頁面 `contact` 適用於所有商店
   - cms頁面 `contact` 適用於具有ID的商店 `1` 和 `2`
   - 任何包含 `car_` 結束於 `html` 適用於具有ID 2的商店
   - 任何包含 `tires_` 適用於含程式碼的存放區 `store_gb`

     ```yaml
     stage:
       post-deploy:
         WARM_UP_PAGES:
           - "category:*:1"
           - "category:*:store1|store2"
           - "category:cars:store_en"
           - "cms-page:contact:*"
           - "cms-page:contact:1|2"
           - "category:|car_.*?\\.html$|:2"
           - "category:|tires_.*|:store_gb"
     ```

  以下範例快取 `product` 實體型別，條件如下：
   - 所有商店的所有產品（以程式設計方式限製為每家商店100項，以避免效能問題）
   - 適用於商店的所有產品 `store1`
   - 產品與 `sku1` 適用於所有商店
   - 產品與 `sku1` 適用於具有程式碼的商店 `store1` 和 `store2`
   - 產品與 `sku1`， `sku2` 和 `sku3` 適用於具有程式碼的商店 `store1` 和 `store2`

     ```yaml
     stage:
       post-deploy:
         WARM_UP_PAGES:
           - "product:*:*"
           - "product:*:store1"
           - "product:sku1:*"
           - "product:sku1:store1|store2"
           - "product:sku1|sku2|sku3:store1|store2"
     ```

  以下範例快取 `store-page` 實體型別，條件如下：
   - 頁面 `/contact-us` 適用於所有商店
   - 頁面 `/contact-us` 適用於具有識別碼的商店 `1`
   - 頁面 `/contact-us` 適用於具有程式碼的商店 `code1` 和 `code2`

  ```yaml
        stage:
          post-deploy:
            WARM_UP_PAGES:
              - "store-page:/contact-us:*"
              - "store-page:/contact-us:1"
              - "store-page:/contact-us:code1|code2"
  ```
