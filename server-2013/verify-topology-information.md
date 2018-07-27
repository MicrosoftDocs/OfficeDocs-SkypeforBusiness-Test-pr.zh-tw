---
title: 驗證拓撲資訊
TOCTitle: 驗證拓撲資訊
ms:assetid: aa4c424e-f87c-4be6-8df6-a0cd193b11fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205151(v=OCS.15)
ms:contentKeyID: 49291949
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 驗證拓撲資訊

 

_**上次修改主題的時間：** 2012-09-26_

驗證已順利完成合併的第一個步驟是，檢視與 Office Communications Server 2007 R2 合併的 Lync Server 2013 拓撲資訊。在拓撲產生器中，\[BackCompatSite\] 節點會顯示所合併的每個 Office Communications Server 2007 R2 集區與伺服器的完整網域名稱 (FQDN)。

## 在拓撲產生器中檢視 BackCompatSite

1.  在您的 Office Communications Server 2007 R2 環境中開啟 Office Communications Server 2007 R2 系統管理工具，並記下舊版集區與伺服器的 FQDN。

2.  在 Lync Server 2013 環境中開啟拓撲產生器，然後展開 \[BackCompatSite\] 節點。

3.  確認所合併之集區與伺服器的 FQDN 均會顯示。
    
    > [!NOTE]  
    > [BackCompatSite] 中將不會出現任何在前端伺服器或 Standard Edition 伺服器上組合之伺服器角色的資訊。只有 Office Communications Server 2007 R2 與 Lync Server 2013 之間交互操作所需的伺服器角色才會出現。
    


![拓撲產生器的 \[BackCompatSite\] 對話方塊](images/JJ205243.62751c76-f018-4c6d-bb48-c61ef8974d31(OCS.15).jpg "拓撲產生器的 [BackCompatSite] 對話方塊")

您也可以使用 Lync Server 2013 控制台 檢視合併後的拓撲。在 Lync Server 2013 控制台中，您可以見到每部伺服器的 FQDN、集區的 FQDN，以及合併後之拓撲的網站名稱。合併後之伺服器的 \[站台\] 名稱為 **BackCompatSite** 。

## 在 Lync Server 2013 控制台中檢視合併後的拓撲

1.  開啟 Lync Server 2013 控制台。

2.  按一下 \[拓撲\] 。

3.  查看 \[站台\] 欄中的 **BackCompatSite** ，確認您所合併的伺服器與集區出現在 \[狀態\] 索引標籤上。

![顯示合併拓撲的 Lync Server 控制台](images/JJ205151.f986ddd4-2040-454d-9389-7f6154b59cc9(OCS.15).jpg "顯示合併拓撲的 Lync Server 控制台")

如需合併後集區的詳細資料，可使用 **Get-CsPool** Cmdlet。除了拓撲產生器和 Lync Server 2013 控制台所提供的資訊之外，此 Cmdlet 還會顯示在 Lync Server 2013 集區上執行的服務。

> [!NOTE]  
> 當您在執行拓撲產生器的 [合併精靈] 之後發行拓撲時，會將會議目錄合併到 Lync Server 2013。您可以執行 <strong>Get-CsConferenceDirectory</strong> Cmdlet 驗證會議目錄。



## 檢視合併後集區中的服務

1.  開啟 Lync Server 2013 管理命令介面。

2.  在命令列輸入下列命令：
    
        Get-CsPool [-Identity <FQDN of the pool>]
    
    例如：
    
        Get-CsPool -Identity pool02.contoso.net

## 驗證合併後的會議目錄

1.  開啟 Lync Server 2013 管理命令介面。

2.  在命令列輸入下列命令：
    
        Get-CsConferenceDirectory

3.  確認您要合併之所有集區或伺服器的會議目錄皆已在 Lync Server 2013 中。

