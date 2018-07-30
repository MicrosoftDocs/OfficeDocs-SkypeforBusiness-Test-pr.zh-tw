---
title: 在 Lync Server 2013 中設定 CAC 的網路區域
TOCTitle: 在 Lync Server 2013 中設定 CAC 的網路區域
ms:assetid: ea3ff988-dd5a-4bc4-bec5-39a0fb09793a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399051(v=OCS.15)
ms:contentKeyID: 49292694
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 CAC 的網路區域

 

_**上次修改主題的時間：** 2012-09-21_

> [!IMPORTANT]  
> 如果您已經為 E9-1-1 或媒體旁路建立網路地區，您可使用 <strong>Set-CsNetworkRegion</strong> Cmdlet 來新增通話許可控制 (CAC) 特有的設定，以修改現有的網路地區。有關如何修改網路地區的範例，請參閱＜<a href="lync-server-2013-create-or-modify-a-network-region.md">在 Lync Server 2013 中建立或修改網路地區</a>＞。



*「網路地區」*(Network Region) 是用於設定 CAC、E9-1-1 和媒體旁路的網路集線器或骨幹。利用下列程序即可建立符合 CAC 網路拓撲範例所述之網路地區的網路地區。若要檢視網路拓撲範例，請參閱規劃文件中的＜[範例：在 Lync Server 2013 中收集通話許可控制服務需求](lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md)＞。

CAC 網路拓撲範例有三個地區：北美地區、EMEA 與 APAC。每個地區各有指定的中央網站。針對北美洲地區，指定的中央網站名稱為 CHICAGO。下列程序顯示的範例說明如何使用 **New-CsNetworkRegion** Cmdlet 建立北美地區。

> [!NOTE]  
> 在下列程序中，Lync Server 管理命令介面會用來建立網路地區。如需使用 Lync Server 控制台建立網路地區的詳細資訊，請參閱＜<a href="lync-server-2013-create-or-modify-a-network-region.md">在 Lync Server 2013 中建立或修改網路地區</a>＞。



## 若要建立通話許可控制的網路地區

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  針對每個需要建立的地區，執行 **New-CsNetworkRegion** Cmdlet。例如，若要建立北美地區，請執行：
    
        New-CsNetworkRegion -Identity NorthAmerica -CentralSite CHICAGO -Description "All North America Locations"

3.  重複步驟 2 以建立網路地區 (EMEA 和 APAC)。

