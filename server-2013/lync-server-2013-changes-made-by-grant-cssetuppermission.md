---
title: Lync Server 2013 中 Grant-CsSetupPermission 進行的變更
TOCTitle: Lync Server 2013 中 Grant-CsSetupPermission 進行的變更
ms:assetid: c5801f48-14e3-4fdd-8f14-d52e7af07a57
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205250(v=OCS.15)
ms:contentKeyID: 49292252
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 Grant-CsSetupPermission 進行的變更

 

_**上次修改主題的時間：** 2015-03-09_

若要委派設定，您可以將權限授與特定 Active Directory 組織單位 (OU) 的 RTCUniversalServerAdmins 萬用群組，讓該 OU 中的 RTCUniversalServerAdmins 群組成員可在指定的網域中安裝 Lync Server 2013，而不需要具備 Domain Admins 群組成員身分。

**Grant-CsSetupPermission** Cmdlet 會授與 OU 上的 RTCUniversalServerAdmins 群組權限，如下表所示：

### 對 OU 中的物件授與的權限

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>權限套用至：</th>
<th>授與的權限為：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCUniversalServerAdmins</p></td>
<td><p>特殊存取權：</p>
<ul>
<li><p>讀取 servicePrincipalName</p></li>
<li><p>寫入 servicePrincipalName</p></li>
<li><p>刪除樹狀目錄</p></li>
<li><p>複寫目錄變更</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>子系 serviceConnectionPoint 物件</p></td>
<td><p>特殊存取權：</p>
<ul>
<li><p>讀取權限</p></li>
<li><p>寫入權限</p></li>
<li><p>建立子項</p></li>
<li><p>刪除子項</p></li>
<li><p>列出內容</p></li>
<li><p>寫入屬性</p></li>
<li><p>讀取屬性</p></li>
<li><p>刪除樹狀目錄</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>子系 msRTCSIP-Server 物件</p></td>
<td><p>特殊存取權：</p>
<ul>
<li><p>寫入屬性</p></li>
<li><p>讀取屬性</p></li>
<li><p>刪除樹狀目錄</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>子系 msRTCSIP-WebComponents 物件</p></td>
<td><p>特殊存取權：</p>
<ul>
<li><p>寫入屬性</p></li>
<li><p>讀取屬性</p></li>
<li><p>刪除樹狀目錄</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>子系 msRTCSIP-MCU 物件</p></td>
<td><p>特殊存取權：</p>
<ul>
<li><p>寫入屬性</p></li>
<li><p>讀取屬性</p></li>
<li><p>刪除樹狀目錄</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>子系 msRTCSIP-MediationServer 物件</p></td>
<td><p>特殊存取權：</p>
<ul>
<li><p>寫入屬性</p></li>
<li><p>讀取屬性</p></li>
<li><p>刪除樹狀目錄</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>子系 msRTCSIP-ApplicationServer 物件</p></td>
<td><p>特殊存取權：</p>
<ul>
<li><p>寫入屬性</p></li>
<li><p>讀取屬性</p></li>
<li><p>刪除樹狀目錄</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>子系 msRTCSIP-ConnectionPoint 物件</p></td>
<td><p>特殊存取權：</p>
<ul>
<li><p>寫入屬性</p></li>
<li><p>讀取屬性</p></li>
<li><p>刪除樹狀目錄</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>子系 Computer 物件</p></td>
<td><p>serviceConnectionPoint 的特殊存取權：</p>
<ul>
<li><p>建立子物件</p></li>
<li><p>刪除子物件</p></li>
<li><p>刪除樹狀目錄</p></li>
</ul>
<p>公用資訊的特殊存取權：</p>
<ul>
<li><p>讀取屬性</p></li>
</ul>
<p>DNS 主機名稱的特殊存取權：</p>
<ul>
<li><p>讀取屬性</p></li>
</ul></td>
</tr>
</tbody>
</table>

