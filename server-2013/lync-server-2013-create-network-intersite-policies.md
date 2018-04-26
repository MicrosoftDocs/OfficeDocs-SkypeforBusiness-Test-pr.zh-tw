---
title: 在 Lync Server 2013 中建立網路站間原則
TOCTitle: 在 Lync Server 2013 中建立網路站間原則
ms:assetid: b0714aae-55dc-4587-b718-34a03f596b22
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412844(v=OCS.15)
ms:contentKeyID: 49292032
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立網路站間原則

 

_**上次修改主題的時間：** 2012-10-19_

*「網站間原則」*(Network Intersite Policy) 會定義網站間的頻寬限制，這些網站之間有直接的 WAN 連結。

如需詳細資訊，請參閱 Lync Server 管理命令介面文件中關於下列 Cmdlet 的部分：

  - [New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)

  - [Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)

  - [Set-CsNetworkInterSitePolicy](set-csnetworkintersitepolicy.md)

  - [Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>只有</em>當兩個網站之間有直接的交叉連結時，才需要網站間原則。</td>
</tr>
</tbody>
</table>


在範例拓撲北美地區中，Reno 和 Albuquerque 網站之間有直接連結。這兩個網站需要網站間原則，以套用適當的頻寬原則設定檔。下列範例會套用 20Mb\_Link 設定檔。

## 若要建立網站間原則

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 New-CsNetworkInterSitePolicy Cmdlet 以建立網站間原則，並為兩個具有直接交叉連結的網站，套用適當的頻寬原則設定檔。例如，執行：
    
        New-CsNetworkInterSitePolicy -InterNetworkSitePolicyID Reno_Albuquerque -NetworkSiteID1 Reno -NetworkSiteID2 Albuquerque -BWPolicyProfileID 20Mb_Link

3.  視需要重複步驟 2，為所有具有直接交叉連結的網站配對建立網站間原則。

