---
source-git-commit: 2d902a3926c6bbc6a9dc8afcbd667eddeaf3be7e
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---
# 包含用於修改Fastly自訂VCL的檔案

## 修改自訂VCL片段

1. [登入](/help/get-started/onboarding.md#access-your-admin-panel) 傳送給管理員。

1. 按一下 **商店** > **設定** > **設定** > **進階** > **系統**.

1. 展開 **完整頁面快取** > **Fastly設定** > **自訂VCL程式碼片段**.

   ![管理自訂VCL片段](/help/assets/cdn/fastly-manage-snippets.png)

1. 在 _動作_ 欄，按一下要編輯的程式碼片段旁的設定圖示。

1. 重新載入頁面後，按一下 **將VCL上傳到Fastly** 在 _Fastly設定_ 區段。

1. 上傳完成後，請根據頁面頂端的通知重新整理快取。

>[!WARNING]
>
>此 _自訂VCL片段_ UI選項只會顯示透過Adobe Commerce管理員新增的程式碼片段。 如果您使用Fastly API新增程式碼片段，請使用API [管理它們](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
