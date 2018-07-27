---
title: Lync Server 2013：安裝 Windows PowerShell 3.0
TOCTitle: 安裝 Windows PowerShell 3.0
ms:assetid: d87bf21e-0a43-41cb-8fdc-626cedec8538
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205328(v=OCS.15)
ms:contentKeyID: 49292497
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 安裝 Windows PowerShell 3.0

 

_**上次修改主題的時間：** 2014-06-27_

若要成功部署 Lync Server 2013，您的 Lync Server 拓撲所包含的每部電腦均需安裝 Windows PowerShell 3.0。

此時，對於執行 Windows Server 2012 或 Windows Server 2012 R2 的系統，您無需執行任何操作，並可直接移至下個部署階段，因為 PowerShell 3.0 已包含在這些作業系統中。

> [!IMPORTANT]  
> 然而，如果是執行 Windows Server 2008 R2 SP1 的系統，您必須先安裝 PowerShell 3.0，然後才能安裝 Lync Server 2013，否則將無法運作。若要安裝 PowerShell 3.0，請參閱 <a href="http://go.microsoft.com/fwlink/p/?linkid=329800">Windows Management Framework 3.0</a>，直接連結至 PowerShell 3.0 下載頁面，並取得如何成功安裝的相關資訊。



完成安裝後，或是在繼續部署 Lync Server 前想要檢查並確認伺服器已有安裝 PowerShell 3.0，可直接執行下列操作：

1.  在所要檢查的伺服器上，選擇 \[開始\]，依序按一下 \[所有程式\]、\[附屬應用程式\] 及 \[Windows PowerShell\]，然後按一下 \[Windows PowerShell\]。

2.  在 Windows PowerShell 主控台中，於命令提示字元處輸入下列命令，然後按 ENTER：
    
        Get-Host | Select-Object Version

3.  如果已安裝 Windows PowerShell 3.0，您會看到以下輸出：
    
        Version
        -------
        3.0

