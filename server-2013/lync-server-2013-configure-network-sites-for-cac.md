---
title: 在 Lync Server 2013 中設定 CAC 的網站
TOCTitle: 在 Lync Server 2013 中設定 CAC 的網站
ms:assetid: afcea38f-5789-45ec-97af-c6e38364950c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412840(v=OCS.15)
ms:contentKeyID: 49292024
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 CAC 的網站

 

_**上次修改主題的時間：** 2012-09-05_

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您已建立 E9-1-1 或媒體旁路的網站，您可以使用 <strong>Set-CsNetworkSite</strong> Cmdlet 修改現有網站以套用頻寬原則設定檔。如需如何修改網站的範例，請參閱 <a href="lync-server-2013-create-or-modify-a-network-site.md">在 Lync Server 2013 中建立或修改網站</a>。</td>
</tr>
</tbody>
</table>


「網站」是指通話許可控制 (CAC)、E9-1-1 和媒體旁路部署的每一個網路地區內的辦公室或位置。利用下列程序即可建立與 CAC 範例網路拓撲中的網站相符的網站。這些程序會顯示如何建立和設定受限於 WAN 頻寬，因此需要頻寬原則來限制即時音訊或視訊流量的網站。

在範例 CAC 部署中，北美地區擁有六個網站。其中三個網站受限於 WAN 頻寬：雷諾、波特蘭和阿布奎基。另外三個*未*受限於 WAN 頻寬的網站：紐約、芝加哥與底特律。如需如何建立或修改這另外三個網站的範例，請參閱[在 Lync Server 2013 中建立或修改網站](lync-server-2013-create-or-modify-a-network-site.md)。

若要檢視範例網路拓撲，請參閱規劃文件中的[範例：在 Lync Server 2013 中收集通話許可控制服務需求](lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在下列程序中，Lync Server 管理命令介面會用來建立網站。如需關於使用 Lync Server 控制台建立網站的詳細資訊，請參閱<a href="lync-server-2013-create-or-modify-a-network-site.md">在 Lync Server 2013 中建立或修改網站</a>。</td>
</tr>
</tbody>
</table>


## 若要建立通話許可控制的網站

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 **New-CsNetworkSite** Cmdlet 建立網站，並且將適當的頻寬原則設定檔套用至每一個網站。例如，執行：
    
        New-CsNetworkSite -NetworkSiteID Reno -Description "NA:Branch office for sales force" -NetworkRegionID NorthAmerica -BWPolicyProfileID 10MB_Link
    
        New-CsNetworkSite -NetworkSiteID Portland -Description "NA:Branch office for marketing force" -NetworkRegionID NorthAmerica -BWPolicyProfileID 5MB_Link
    
        New-CsNetworkSite -NetworkSiteID Albuquerque -Description "NA:Branch office for SouthWest sales" -NetworkRegionID EMEA -BWPolicyProfileID 10MB_Link

3.  若要完成建立整個範例拓撲的網站，請針對 EMEA 和 APAC 地區中受頻寬限制的網站重複步驟 2。

