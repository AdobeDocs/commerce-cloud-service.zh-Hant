---
title: GitHub整合
description: 瞭解如何在雲端基礎結構專案上將Adobe Commerce與GitHub整合。
feature: Cloud, Integration
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: 5305452f-4c8d-438c-ac78-e2e1ec2f8cd9
source-git-commit: 4d32fc596064f01eaefe3ee509a655837fa846de
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# GitHub整合

GitHub整合可讓您直接從GitHub存放庫在雲端基礎結構環境中管理Adobe Commerce。 此整合可管理GitHub中的內容，並在雲端基礎結構程式碼存放庫上與您的Adobe Commerce同步。 本質上，程式碼存放庫會成為GitHub存放庫的映象。

{{private-repository}}

此整合可讓您：

- 建立分支時建立環境
- 合併提取請求時重新部署環境
- 刪除分支時刪除環境

您必須取得GitHub權杖和webhook才能繼續此程式。

## 必要條件

- 雲端基礎結構專案上Adobe Commerce的管理員存取權
- GitHub存放庫
- GitHub個人存取權杖

## 產生GitHub代號

在GitHub開發人員設定中建立傳統個人存取權杖。 您必須是具有寫入GitHub存放庫存取權的群組的成員，這樣您才可以 _推播_ 至存放庫。 建立您的Token時包含下列範圍：

- `admin:repo_hook` — 建立Web鉤點
- `repo` — 與存放庫整合
- `read:org` — 與您的組織存放庫整合

另請參閱 [GitHub：建立](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

## 準備您的存放庫

從現有環境複製雲端基礎結構專案上的Adobe Commerce，並將專案分支移轉至新的空GitHub存放庫，保留相同的分支名稱。 它是 **關鍵** 以保留相同的Git樹狀結構，這樣您就不會遺失雲端基礎結構專案中Adobe Commerce的任何現有環境或分支。

1. 從終端機，在雲端基礎結構專案上登入您的Adobe Commerce。

   ```bash
   magento-cloud login
   ```

1. 列出您的專案並複製專案ID。

   ```bash
   magento-cloud project:list
   ```

1. 將專案複製到您的本機環境。

   ```bash
   magento-cloud project:get <project-ID>
   ```

1. 將您的GitHub存放庫新增為遠端。

   ```bash
   git remote add origin git@github.com:<user-name>/<repo-name>.git
   ```

   遠端連線的預設名稱可能是 `origin` 或 `magento`. 如果 `origin` 存在，您可以選擇不同的名稱，也可以重新命名或刪除現有的參照。 另請參閱 [git-remote檔案](https://git-scm.com/docs/git-remote).

1. 確認您已正確新增GitHub遠端。

   ```bash
   git remote -v
   ```

   預期回應：

   ```terminal
   origin git@github.com:<user-name>/<repo-name>.git (fetch)
   origin git@github.com:<user-name>/<repo-name>.git (push)
   ```

1. 將專案檔案推送至新的GitHub存放庫。 請記得保持所有分支名稱相同。

   ```bash
   git push -u origin master
   ```

   如果您正從新的GitHub存放庫開始，您可能必須使用 `-f` 選項，因為遠端存放庫不符合您的本機復本。

1. 確認您的GitHub存放庫包含所有專案檔案。

## 啟用GitHub整合

開始之前，您的專案程式碼和環境必須在GitHub存放庫中。 啟用整合後，GitHub存放庫會成為程式碼來源。 如果您推送程式碼變更至原始程式碼 `magento` 存放庫，當您將程式碼變更推送到GitHub存放庫時，整合會覆寫該程式碼。

以下內容會啟用GitHub整合，並提供要在建立webhook時使用的裝載URL。

>[!WARNING]
>
>下列命令會覆寫 _全部_ 使用您GitHub存放庫中的程式碼，在雲端基礎結構專案的Adobe Commerce中建立程式碼，其中包括所有分支，包括 `production` 分支。 此動作會立即發生且無法還原。 依據最佳做法的要求，請在雲端基礎結構專案上從Adobe Commerce複製所有分支，並將它們推送到GitHub存放庫 **早於** 新增GitHub整合。

您可以選擇使用逐步執行CLI提示 `magento-cloud integration:add` 或者，您可以使用以下選項建置整合指令：

| 選項 | 必填？ | 說明 |
| ----------------------- | --------- | --------------------------------- |
| `--base-url` | 是 | 伺服器安裝的基底URL，可能是 `https://github.com/` 或自訂。 如果您的存放庫是透過公開Github託管，請忽略此選項。 |
| `--token` | 是 | 您為GitHub產生的個人存取權杖 |
| `--repository` | 是 | 存放庫名稱： `owner-or-organisation/repository` |
| `--build-pull-requests` | 可選 | Adobe Commerce在合併提取請求(`true` 預設值) |
| `--fetch-branches` | 可選 | 促使雲端基礎結構上的Adobe Commerce追蹤分支，並在您更新分支後進行部署(`true` 預設值) |
| `--prune-branches` | 可選 | 刪除遠端上不存在的分支(`true` 預設值) |

還有許多選項，您可以使用說明選項檢視它們：

```bash
magento-cloud integration:add --help
```

**啟用GitHub整合的方式**：

1. 啟用整合。

   ```bash
   magento-cloud integration:add --type=github --project=<project-ID> --token=<your-GitHub-token> {--repository=USER/REPOSITORY | --repository=ORGANIZATION/REPOSITORY} [--build-pull-requests={true|false} --fetch-branches={true|false}
   ```

   **範例1**：為個人私人存放庫啟用GitHub整合：

   ```bash
   magento-cloud integration:add --type=github --project=ov58dlacU2e --base-url=https://github.com --token=<token> --repository=myUserName/myrepo
   ```

   **範例2**：為組織存放庫啟用GitHub整合：

   ```bash
   magento-cloud integration:add --type=github --project=ov58dlacU2e --base-url=https://github.com --token=<token> --repository=Magento/teamrepo
   ```

1. 出現提示時，輸入必要資訊。

1. 複製 **裝載URL** 由傳回輸出顯示。

   ```terminal
   Created integration <integration-ID> (type: github)
   Repository: myUserName/myrepo
   Build PRs: yes
   Fetch branches: yes
   Payload URL: https://us.magento.cloud/api/projects/<project-id>/integrations/wO8a0eoamxwcg/hook
   ```

## 在GitHub中新增webhook

若要與Cloud Git伺服器通訊事件（例如推播），您必須為GitHub存放庫建立webhook：

1. 在您的GitHub存放庫中，按一下 **設定** 標籤。

1. 在左側導覽列中，按一下 **Webhooks**.

1. 在 _Webhooks_ 窗格，按一下 **新增webhook**.

1. 在 _Webhook/新增webhook_ 表單，編輯下列欄位：

   - **裝載URL**：輸入啟用GitHub整合時傳回的URL。
   - **內容型別**：選擇 **application/json** 從清單中。
   - **密碼**：輸入驗證密碼。
   - **您想要觸發此webhook的哪些事件？**：選取 **傳送所有資料給我**.
   - 選取 **作用中** 核取方塊。

1. 按一下 **新增webhook**.

## 測試整合

設定GitHub整合後，您可以使用驗證整合運作正常 `magento-cloud` CLI：

```bash
magento-cloud integration:validate
```

或者，您也可以推送簡單的變更至您的GitHub存放庫以進行測試。

1. 建立測試檔案。

   ```bash
   touch test.md
   ```

1. 提交變更並將其推播至您的GitHub存放庫。

   ```bash
   git add . && git commit -m "Testing GitHub integration" && git push
   ```

1. 登入 [[!DNL Cloud Console]](../project/overview.md) 並確認您的認可訊息已顯示，且您的專案已部署。

## 移除整合

您可以安全地從專案移除GitHub整合，而不會影響程式碼。

**移除GitHub整合的方式**：

1. 從終端機，在雲端基礎結構專案上登入您的Adobe Commerce。

1. 列出您的整合。 您需要GitHub整合ID才能完成下一步。

   ```bash
   magento-cloud integration:list
   ```

1. 刪除整合。

   ```bash
   magento-cloud integration:delete <int-ID>
   ```

此外，您也可以登入您的GitHub帳戶，並移除中的網頁勾點來移除GitHub整合 _Webhooks_ 存放庫索引標籤 _設定_.
