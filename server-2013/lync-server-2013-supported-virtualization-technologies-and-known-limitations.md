---
title: Lync Server 2013：受支援的虛擬化技術與已知限制
TOCTitle: 受支援的虛擬化技術與已知限制
ms:assetid: 6d3d749d-e840-4c05-afae-d6e69e7616aa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204982(v=OCS.15)
ms:contentKeyID: 49291249
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中受支援的虛擬化技術與已知限制

 

_**上次修改主題的時間：** 2015-01-26_

Lync VDI 外掛程式可讓您針對支援的虛擬化技術進行音訊和視訊通話。這延伸了 [Microsoft Lync 2010 中的用戶端虛擬化](http://go.microsoft.com/fwlink/?linkid=330447) 白皮書中概述的 Microsoft Lync Server 2010 功能。為遵循標準電話法規，同時也包括支援 E911。以下章節說明 Lync VDI 外掛程式支援的虛擬化技術，以及已知的功能限制。

## 對虛擬化技術的支援

Lync VDI 外掛程式支援個人虛擬桌面案例中的完整桌面遠端功能，但不支援遠端桌面工作階段案例。這些案例的說明如下：

  - **支援：個人化虛擬桌面或虛擬桌面基礎結構 (VDI)。**   在這個案例中，每位使用者登入自訂的虛擬桌面，並且能儲存在所有工作階段均會顯示的桌面上的檔案。Microsoft 遠端桌面服務、VMware Horizon View 和 Citrix XenDesktop 都是經過測試且能用於 Lync 的實作範例。如需廠商專用的 VDI 環境和通過 Microsoft 測試的用戶端硬體的相關資訊，請參閱 [Microsoft Lync 的合格基礎結構](http://go.microsoft.com/fwlink/?linkid=313435) (英文)。

  - **不支援：遠端桌面工作階段。**   在這個案例中，每位使用者登入一般、無法自訂的虛擬桌面工作階段。實作範例包括 Microsoft 遠端桌面工作階段 (RDSH) 和結合 Citrix 接收器的 Citrix XenApp。

Lync VDI 外掛程式不支援其他虛擬化技術，(例如應用程式虛擬化，此技術允許我們在沒有本機完整安裝的情況下使用應用程式)。實作範例包括 Citrix XenApp 和 Microsoft Application Virtualization (App-V)。應用程式串流、應用程式遠端處理和混合虛擬化模式 (例如完整桌面遠端中的應用程式遠端) 也不受支援。

為能擁有擴充性， Lync VDI 外掛程式經特別設計，能使用不需倚賴平台的 API (稱為動態虛擬通道 (DVC))。如想瞭解 Lync 未明確提供支援的案例，請參閱 VDI 解決方案供應者的支援說明。

## 已知的功能限制

以下為在 VDI 環境中使用 Lync 2013 時的已知限制：

  - 僅能有限支援通話委派及 回應群組代理人匿名功能。

  - 不支援以下功能：
    
      - 整合式音訊裝置及視訊裝置調整頁面。
    
      - 多重檢視視訊。
    
      - 錄製交談。
    
      - 以匿名方式加入會議 (換言之，加入由未與您組織建立同盟之組織所主持的 Lync 會議)。
    
      - 搭配 Lync Phone Edition 裝置使用 Lync VDI 外掛程式。
    
      - 在網路中斷連線的情況下延續通話。
    
      - 自訂鈴聲及通話保留音樂功能。

  - Lync VDI 外掛程式在 Office 365 環境中不受支援。

