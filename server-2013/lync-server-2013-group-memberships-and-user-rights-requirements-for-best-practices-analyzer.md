---
title: 最佳做法分析程式的群組成員資格及使用者權限需求
TOCTitle: 最佳做法分析程式的群組成員資格及使用者權限需求
ms:assetid: f812e343-8f75-454e-b7a8-1b404e32071a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg591354(v=OCS.15)
ms:contentKeyID: 49292857
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 最佳做法分析程式的群組成員資格及使用者權限需求

 

_**上次修改主題的時間：** 2012-10-21_

若要成功執行「最佳做法分析程式」最佳做法分析程式，您用於登入的使用者帳戶必須是本機電腦「系統管理員」群組的成員。此外，若要掃描您的環境，使用者帳戶必須是下列群組的成員：

  - **Domain Admins**   以列舉「Active Directory 網域服務」資訊，以及呼叫網域控制器與全域目錄伺服器上的 Windows Management Instrumentation (WMI) 提供者。

  - **Administrators**   每部 Lync Server 2013 內部電腦與每部 Edge Server 均必須使用，以呼叫 Windows Management Instrumentation (WMI) 提供者及存取登錄。

  - **RTCUniversalReadOnlyAdmins**   高權限或委派的唯讀 Lync Server 2013 系統管理權限。

  - **Exchange 僅檢視管理**   Microsoft Exchange 組織中的高權限或委派的 Exchange 僅檢視管理。

如果您的使用者沒有足夠的使用權限，您有兩種選擇：

  - 開啟命令提示字元，在沒有足夠使用者權限的帳戶下使用 **runas** 命令來執行工具。語法如下：
    
        runas /netonly /user:<domain>\<userName> rtcbpa.exe

  - 在 \[連接到 Active Directory\] 頁面中，設定規劃用於執行「最佳做法分析程式」之帳戶的憑證。按一下 \[顯示進階登入選項\]可輸入三個帳戶；一個用於連接至 「Active Directory 網域服務」，一個用於連接至 Lync Server 2013Edge Server，另一個用於連接至 Exchange 伺服器。如果您未指定這三個帳戶其中之一，則會使用登入與執行「最佳做法分析程式」所使用的帳戶。

