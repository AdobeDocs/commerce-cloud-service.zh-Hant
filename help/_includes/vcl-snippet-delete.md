---
source-git-commit: 8f1ed3067f6daed897151052c8b9f987d3df3a50
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---
# 包含用於刪除Fastly自訂VCL的檔案

## 刪除自訂VCL片段

1. [登入](/help/get-started/onboarding.md#access-your-admin-panel) 傳送給管理員。

1. 按一下 **商店** > **設定** > **設定** > **進階** > **系統**.

1. 展開 **完整頁面快取** > **Fastly設定** > **自訂VCL程式碼片段**.

   ![管理自訂VCL片段](/help/assets/cdn/fastly-manage-snippets.png)

1. 在 _動作_ 欄，按一下要刪除的程式碼片段旁的垃圾桶圖示。

1. 在下一個強制回應視窗中，按一下 **DELETE** 並啟用新版本。

>[!WARNING]
>
>此 _自訂VCL片段_ UI選項只會顯示透過Adobe Commerce管理員新增的程式碼片段。 如果您使用Fastly API新增程式碼片段，請使用API [管理它們](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-vcl-using-the-api).
