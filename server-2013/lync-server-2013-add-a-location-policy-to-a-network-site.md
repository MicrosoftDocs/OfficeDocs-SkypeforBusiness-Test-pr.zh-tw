---
title: 在 Lync Server 2013 中將位置原則新增到網站
TOCTitle: 在 Lync Server 2013 中將位置原則新增到網站
ms:assetid: 43bfab8a-3d6b-4ca4-8425-879fd910502e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425936(v=OCS.15)
ms:contentKeyID: 49290751
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將位置原則新增到網站

 

_**上次修改主題的時間：** 2013-02-24_

下列範例顯示如何將在＜[在 Lync Server 2013 中建立位置原則](lync-server-2013-create-location-policies.md)＞中定義的 **Redmond** 位置原則新增至現有的網路網站，以及如何建立使用 **Redmond** 位置原則的新網路網站。

如需使用網路網站的詳細資訊，請參閱 Lync Server 管理命令介面文件中關於下列 Cmdlet 的部分：

  - **New-CsNetworkSite**

  - **Get-CsNetworkSite**

  - **Set-CsNetworkSite**

  - **Remove-CsNetworkSite**

## 若要指派位置原則給現有網路網站

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行下列 Cmdlet 來修改現有的網路網站。
    
    將具有 **Redmond** 標記的位置原則指派給名為 **Redmond** 的現有網路網站。
    
        Set-CsNetworkSite -Identity "Redmond" -NetworkRegionID "NorthAmerica" -LocationPolicy "Redmond"

## 若要指派位置原則給新的網路網站

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行下列 Cmdlet 來建立新的網路網站。
    
    在網路地區中建立新的網路網站，並指派具有 **Redmond** 標記的位置原則。
    
        New-CsNetworkSite -Identity "Redmond" -NetworkRegionID "NorthAmerica" -LocationPolicy "Redmond"

