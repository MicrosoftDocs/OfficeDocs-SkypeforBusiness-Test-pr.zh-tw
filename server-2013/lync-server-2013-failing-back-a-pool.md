---
title: Lync Server 2013：容錯回復集區
TOCTitle: 容錯回復集區
ms:assetid: 6232b644-ef57-4c9c-abec-14ff8ffc9fe7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204945(v=OCS.15)
ms:contentKeyID: 49291112
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中容錯回復集區

 

_**上次修改主題的時間：** 2012-11-01_

在發生災難的集區重新連線後 (如此範例中的 Pool1)，請採取下列步驟將部署還原至正常運作狀態。

請注意，容錯回復程序需要數分鐘才能完成。僅供參考：對於有 20,000 個使用者的集區，預計會花上 60 分鐘。

1.  若要容錯回復原來位於 Pool1 而容錯移轉至 Pool2 的使用者，請鍵入下列 Cmdlet：
    
        Invoke-CsPoolFailback -PoolFQDN <Pool1 FQDN> -Verbose

無需其他步驟。如果已容錯移轉 中央管理伺服器，可以將它留在 Pool2。

