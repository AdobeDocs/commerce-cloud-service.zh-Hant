---
title: GitLab整合
description: 瞭解如何將雲端基礎結構專案上的Adobe Commerce與GitLab整合。
feature: Cloud, Integration
exl-id: 37fda8a0-7274-422f-9049-243f2e409f26
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# GitLab整合

您可以設定GitLab存放庫，以便在推送程式碼變更時自動建置和部署環境。 這項整合會在雲端基礎結構帳戶上，將您的GitLab存放庫與Adobe Commerce同步。

{{private-repository}}

此整合可讓您：

- 建立分支時建立環境
- 合併提取請求時重新部署環境
- 刪除分支時刪除環境

您必須取得GitLab權杖和webhook才能繼續此程式。

## 必要條件

- 雲端基礎結構專案上Adobe Commerce的管理員存取權
- [`magento-cloud` CLI](../dev-tools/cloud-cli-overview.md) 本機環境中的工具
- GitLab帳戶
- GitLab個人存取權杖具有GitLab存放庫的寫入存取權，選取的範圍必須至少為： `api` 和 `read_repository`.

## 準備您的存放庫

從現有環境複製雲端基礎結構專案上的Adobe Commerce，並將專案分支移轉至新的空GitLab存放庫，保留相同的分支名稱。 它是 **關鍵** 以保留相同的Git樹狀結構，這樣您就不會遺失雲端基礎結構專案中Adobe Commerce的任何現有環境或分支。

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
   magento-cloud project:get <project-id>
   ```

1. 將您的GitLab存放庫新增為遠端（假設在其SaaS版本中使用GitLab）。

   ```bash
   git remote add origin git@gitlab.com:<user-name>/<repo-name>.git
   ```

   遠端連線的預設名稱可能是 `origin` 或 `magento`. 如果 `origin` 存在，您可以選擇不同的名稱，也可以重新命名或刪除現有的參照。 另請參閱 [git-remote檔案](https://git-scm.com/docs/git-remote).

1. 確認您已正確新增GitLab遠端。

   ```bash
   git remote -v
   ```

   預期回應：

   ```terminal
   origin git@gitlab.com:<user-name>/<repo-name>.git (fetch)
   origin git@gitlab.com:<user-name>/<repo-name>.git (push)
   ```

1. 將專案檔案推送至新的GitLab存放庫。 請記得保持所有分支名稱相同。

   ```bash
   git push -u origin master
   ```

   如果您從新的GitLab存放庫開始，您可能需要使用 `-f` 選項，因為遠端存放庫不符合您的本機復本。

1. 確認您的GitLab存放庫包含所有專案檔案。

## 啟用GitLab整合

使用 `magento-cloud integration` 命令以啟用GitLab整合，並取得GitLab webhook的裝載URL，以將更新從GitLab傳送至雲端基礎結構專案上的Adobe Commerce。

```bash
magento-cloud integration:add --type=gitlab --project=<project-ID> --token=<your-GitLab-token> [--base-url=<GitLab-url> --server-project=<GitLab-project> --build-merge-requests={true|false} --merge-requests-clone-parent-data={true|false} --fetch-branches={true|false} --prune-branches={true|false}]
```

| 選項 | 說明 |
| ------ | ----------- |
| `<project-ID>` | 雲端基礎結構專案ID上的Adobe Commerce |
| `<your-GitLab-token>` | 您為GitLab產生的個人存取權杖 |
| `--base-url` | GitLab的URL (`https://gitlab.com/` （如果GitLab在其SaaS版本中使用） |
| `--server-project` | GitLab中的專案名稱（基底URL之後的部分） |
| `--build-merge-requests` | 一個 _可選_ 此引數會指示Adobe Commerce在雲端基礎結構上為每個合併請求建立新的環境(`true` 預設值) |
| `--merge-requests-clone-parent-data` | 一個 _可選_ 指示雲端基礎結構上的Adobe Commerce為合併請求複製父級環境的資料的引數(`true` 預設值) |
| `--fetch-branches` | 一個 _可選_ 導致雲端基礎結構上的Adobe Commerce從遠端（以非使用中環境的形式）擷取所有分支的引數(`true` 預設值) |
| `--prune-branches` | 一個 _可選_ 指示雲端基礎結構上的Adobe Commerce刪除不存在於遠端的分支的引數(`true` 預設值) |

>[!WARNING]
>
>此 `magento-cloud integration` 命令覆寫 _全部_ 使用您GitLab存放庫中的程式碼，在雲端基礎結構專案上執行Adobe Commerce中的程式碼。 這包括全部分支，包括 `production` 分支。 此動作會立即發生且無法還原。 依據最佳做法的要求，在新增GitLab整合之前，請務必先在雲端基礎結構專案上複製Adobe Commerce中的所有分支，並將其推送至GitLab存放庫。

**啟用GitLab整合的方式**：

1. 從終端機，將GitLab整合新增到雲端基礎結構專案上的Adobe Commerce：

   ```bash
   magento-cloud integration:add --type gitlab --project=3txxjf32gtryos --token=qVUfeEn4ouze7A7JH --base-url=https://gitlab.com/ --server-project=my-agency/project-name --build-merge-requests=false --merge-requests-clone-parent-data=false --fetch-branches=true --prune-branches=true
   ```

1. 出現提示時，輸入 `y` 以新增整合。

   ```terminal
   Warning: adding a 'gitlab' integration will automatically synchronize code from the external Git repository.
   This means it can overwrite all the code in your project.
   Are you sure you want to continue? [y/N] y
   ```

1. 複製 **連結URL** 由傳回輸出顯示。

   ```terminal
   Hook URL: https://eu-3.magento.cloud/api/projects/3txxjf32gtryos/integrations/eolmpfizzg9lu/hook
   Created integration eolmpfizzg9lu (type: gitlab)
   +----------------------------------+---------------------------------------------------------------------------------------+
   | Property                         | Value                                                                                 |
   +----------------------------------+---------------------------------------------------------------------------------------+
   | id                               | <integration-id>                                                                      |
   | type                             | gitlab                                                                                |
   | token                            | ******                                                                                |
   | base_url                         | https://gitlab.com/                                                                   |
   | project                          | my-agency/project-name                                                                |
   | fetch_branches                   | true                                                                                  |
   | prune_branches                   | true                                                                                  |
   | build_merge_requests             | false                                                                                 |
   | merge_requests_clone_parent_data | false                                                                                 |
   | hook_url                         | https://eu-3.magento.cloud/api/projects/<project-id>/integrations/<integration-id>/hook |
   +----------------------------------+---------------------------------------------------------------------------------------+
   ```

### 在GitLab中新增webhook

若要與您的Cloud Git伺服器通訊事件（例如推送或合併請求），您必須 [建立webhook](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html#overview) 您的GitLab存放庫專用

1. 在您的GitLab存放庫中，按一下 **設定** 標籤。

1. 在左側導覽列中，按一下 **Webhooks**.

1. 在 _Webhooks_ 表單，編輯下列欄位：

   - **URL**：輸入 `Hook URL` 會在您啟用GitLab整合時傳回。
   - **密碼權杖**：視需要輸入驗證密碼。
   - **觸發**：檢查 `Merge request events` 和/或 `Push events` 視您的需求而定。
   - **啟用SSL驗證**：您必須選取此選項。

1. 按一下 **新增webhook**.

### 測試整合

設定GitLab整合後，您可以使用 `magento-cloud` CLI：

```bash
magento-cloud integration:validate
```

或者，您也可以推送簡單的變更至您的GitLab存放庫以進行測試。

1. 建立測試檔案。

   ```bash
   touch test.md
   ```

1. 認可變更並將其推播至您的GitLab存放庫。

   ```bash
   git add . && git commit -m "Testing GitLab integration" && git push
   ```

1. 登入 [[!DNL Cloud Console]](../project/overview.md) 並確認您的認可訊息已顯示，且您的專案已部署。

## 建立雲端分支

使用 `magento-cloud` CLI `environment:push` 命令來建立和啟動新環境。 另請參閱 [建立雲端分支](bitbucket.md#create-a-cloud-branch).

## 移除整合

使用 `magento-cloud` CLI `integration:delete` 命令以移除整合。 另請參閱 [移除整合](bitbucket.md#remove-the-integration).
