---
title: 安裝 Lync Server 2013 核心檔案與 RTCLocal 資料庫
TOCTitle: 安裝 Lync Server 2013 核心檔案與 RTCLocal 資料庫
ms:assetid: 206f0c1d-40f7-45b6-aa62-88aaef6cf7f6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204734(v=OCS.15)
ms:contentKeyID: 49290316
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝 Lync Server 2013 核心檔案與 RTCLocal 資料庫

 

_**上次修改主題的時間：** 2012-10-20_

若要在電腦上安裝 Lync Server 2013 核心檔案，請完成下列程序。安裝核心檔案時，會自動安裝 RTCLocal 資料庫。請注意，您不需要在監看員節點上安裝 SQL Server，而會自動為您安裝 SQL Server Express。

若要安裝 Lync Server 2013 核心檔案和 RTCLocal 資料庫：

1.  在監看員節點電腦上，依序按一下 \[開始\]、\[所有程式\] 及 \[附屬應用程式\]，再以滑鼠右鍵按一下 \[命令提示字元\]，然後按一下 \[以系統管理員身分執行\]。

2.  在主控台視窗中，使用適當的 Lync Server 安裝檔案路徑，輸入下列命令，然後按 ENTER 鍵：
    
        D:\Setup.exe /BootstrapLocalMgmt

若要驗證是否成功安裝好 Lync Server 元件，請依序按一下\[開始\]、\[所有程式\]、\[Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。在 Lync Server 2013 管理命令介面中輸入下列 Windows PowerShell 命令，然後按 ENTER 鍵：

    Get-CsWatcherNodeConfiguration

第一次執行此命令時，由於您尚未設定任何監看員節點電腦，因此不會傳回任何資料。只要此命令執行時沒有傳回任何錯誤，您就可以假設 Lync Server 安裝已成功完成。

若您的監看員節點電腦是位於周邊網路內，則可以執行下列命令以驗證 Lync Server 2013 安裝：

    Get-CsPinPolicy

依據您組織中設定使用的個人識別碼 (PIN) 原則數量而定，您會收到類似下列的資訊：

    Identity             : Global
    Description          :
    MinPasswordLength    : 5
    PINHistoryCount      : 0
    AllowCommonPatterns  : False
    PINLifetime          : 0
    MaximumLogonAttempts :

若您看到 PIN 原則的相關資訊，就表示已成功安裝核心元件。

