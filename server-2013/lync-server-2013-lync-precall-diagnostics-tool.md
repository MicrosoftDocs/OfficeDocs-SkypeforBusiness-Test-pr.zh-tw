---
title: Lync PreCall Diagnostics 工具
TOCTitle: Lync PreCall Diagnostics 工具
ms:assetid: 0ff291ec-cfb4-43eb-b5d6-a7a325681e3f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn451255(v=OCS.15)
ms:contentKeyID: 59602850
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync PreCall Diagnostics 工具

 

_**上次修改主題的時間：** 2014-01-14_

Lync PreCall Diagnostics 工具 (PCD) 是以用戶端為基礎的應用程式，可讓您查看目前的網路狀態會如何影響後續企業語音通話的音訊品質。

PCD 可在 (例如使用公用 WiFi 網路的筆電或家用使用者) 上一個網路躍點品質低劣的情況下派上用場。PCD 會建立周遊該網路最後階段的小型封包資料流。此工具接著會分析封包資料流，以評估此階段沿途的抖動和損失對於通話品質的影響，然後提供報告。您可以在用戶端上持續執行 PCD，即使是通話期間亦然。封包資料流對於頻寬不會有太大的影響。

**最新發行的 PCD 版本 1.1 包含下列增強功能：**

  - 支援更長的密碼，現在最多可有 127 個字元

  - 驗證登入問題的額外診斷

  - 更完善地支援 Lync 混合部署

  - 認證挑選器更新

  - 穩定性改善

Microsoft 歡迎各位不吝提供任何意見。請將所有支援相關問題傳送至 [PCD 意見反應](mailto:pcdfb@microsoft.com) (或 <pcdfb@microsoft.com>)。

本主題涵蓋下列章節：

  - Lync PCD 版本

  - Lync PCD 系統需求

  - Lync PCD 功能

  - 執行 Lync PCD

  - 取消安裝 Lync PCD

## Lync PCD 版本

本主題說明下列可供免費下載的工具版本：

  - Windows 桌面應用程式 ([http://go.microsoft.com/fwlink/?LinkId=327914](http://go.microsoft.com/fwlink/p/?linkid=327914))

  - Windows 8 新式應用程式 ([http://go.microsoft.com/fwlink/?LinkId=322110](http://go.microsoft.com/fwlink/p/?linkid=322110))

> [!NOTE]  
> Office 365 Lync 使用者可使用兩種版本的 PCD。



若要使用舊版 PCD，請參閱下列資訊：

  - 32 位元版本的 PCD 可從 Microsoft 下載中心免費下載取得：[Office Communications Server 2007 R2, PreCallDiagnostic Resource Kit Tool (32 位元)](http://go.microsoft.com/fwlink/p/?linkid=164769) (英文)。

  - 64 位元版本的 PCD 隨附於 Office Communications Server 2007 R2 Resource Kit Tools，可從 Microsoft 下載中心免費取得：[Office Communications Server 2007 R2 Resource Kit Tools](http://go.microsoft.com/fwlink/p/?linkid=145159) (英文)。

## Lync PCD 系統需求

> [!NOTE]  
> PCD 要求安裝與設定整合通訊 Web API (UCWA) 以支援 Lync Server 部署中的行動用戶端。UCWA 會隨 Lync Server 一併安裝。



## Windows 桌面應用程式需求

  - 任何版本的 Windows 7 或 Windows 8 作業系統

  - Microsoft .NET Framework 4.5，可從下列位置取得：[http://go.microsoft.com/fwlink/?LinkId=327790](http://go.microsoft.com/fwlink/p/?linkid=327790)

## Windows 8 新式應用程式需求

  - 任何版本的 Windows 8 作業系統

  - Microsoft .NET Framework 4.5，可從下列位置取得：[http://go.microsoft.com/fwlink/?LinkId=327790](http://go.microsoft.com/fwlink/p/?linkid=327790)

## Lync PCD 功能

Lync PCD 包含下列功能：

  - 在預設的 On Demand 中執行 (2 分鐘高載速度)

  - 在一律開啟 (嵌入式檢視中可達 24 小時) 的模式中執行

  - 檢視測試執行的記錄

  - 診斷登入失敗 (僅限 Windows 8 適用的 Lync PCD)

![Lync PCD 功能登入進度螢幕擷取畫面](images/Dn451255.7e0eb891-1481-47ae-8d63-164468f69c96(OCS.15).png "Lync PCD 功能登入進度螢幕擷取畫面")

  - 網路計量的圖形檢視 – 全螢幕與嵌入式檢視的網路 MOS、封包遺失及間歇的抖動。

**全螢幕檢視**

![PreCall 診斷工具測試結果圖表](images/Dn451255.5d01fd94-9e59-4823-96c7-7a1c83dd7d31(OCS.15).png "PreCall 診斷工具測試結果圖表")

**嵌入式檢視**

![PreCall 診斷工具使用率測試結果](images/Dn451255.30501ba7-22d1-4db1-9297-56cf7dc6721c(OCS.15).png "PreCall 診斷工具使用率測試結果")

## 執行 Lync PCD

## 執行 Windows 桌面應用程式

1.  若要在 Windows 7 系統中啟動 PCD，請從 \[開始\] 功能表中選取 \[PreCall Diagnostics\]。
    
    若要在 Windows 8 系統中啟動 PCD，請從 \[開始\] 畫面中選取該圖示，或搜尋 “PreCall Diagnostics”。
    
    ![PreCall 診斷工具圖示](images/Dn451255.c9800fde-54f6-4efe-bb35-1a38064ec380(OCS.15).png "PreCall 診斷工具圖示")

2.  工具啟動後，選取偏好的認證提供方式並在 \[PreCall Diagnostics Tool Options\] (PreCall Diagnostics 工具選項) 對話方塊中選取網路作業模式，然後選取 \[OK \] (確定)：

3.  選取 \[Start Test\] (開始測試) 按鈕以開始執行診斷。
    
    若是選取 \[Use network credentials\] (使用網路認證) 選項，測試即會立即開始。
    
    若是選取 \[Let me enter my credentials\] (手動輸入認證) 選項，則 \[Windows 安全性\] 對話方塊即會開啟。輸入認證資料後，測試即會開始。


## 執行 Windows 8 最新應用程式

1.  若要啟動 PCD，請選擇 \[開始\] 畫面中的圖示，或搜尋 “PreCall Diagnostics”。
    
    ![PreCall 診斷工具圖示](images/Dn451255.c9800fde-54f6-4efe-bb35-1a38064ec380(OCS.15).png "PreCall 診斷工具圖示")

2.  工具啟動後，請提供您的 Lync 認證並選擇 \[OK\] (確定)。
    
    ![Lync PreCall Diagnostics Tool 登入](images/Dn451255.88039914-4c68-48f6-a9fa-58cb4e3f3488(OCS.15).jpg "Lync PreCall Diagnostics Tool 登入")

3.  選擇 \[Start Test\] (開始測試) 按鈕開始執行診斷。


## 解除安裝 Lync PCD

若要移除 Lync PCD，請針對您的作業系統執行下列程序：

  - 在 Windows 7 系統中，開啟 \[控制台\]，選取 \[程式和功能\]，然後連按兩下 \[Lync 2013 PreCall Diagnostics\]。

  - 在 Windows 8 系統中，以滑鼠右鍵按一下 PCD 名稱，然後從開始畫面下方的應用程式列中按下 \[解除安裝\]。

