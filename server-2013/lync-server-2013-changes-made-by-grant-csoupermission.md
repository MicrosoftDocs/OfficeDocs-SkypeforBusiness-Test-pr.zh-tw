---
title: Lync Server 2013 中 Grant-CsOUPermission 進行的變更
TOCTitle: Lync Server 2013 中 Grant-CsOUPermission 進行的變更
ms:assetid: d744d352-1ad9-4447-8e2b-28e768d2ed1b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205310(v=OCS.15)
ms:contentKeyID: 49292447
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 Grant-CsOUPermission 進行的變更

 

_**上次修改主題的時間：** 2015-03-09_

若要委派 Lync Server 2013 管理工作，您可以對指定的組織單位 (OU) 新增權限，以便讓進行樹系準備時建立的 RTC 萬用群組成員，不需要成為 Domain Admins 群組的成員也能夠存取 OU。

**Grant-CsOuPermission** Cmdlet 可將權限授與所指定 OU 中的物件，如下表所示。

## 授與 User 物件的權限

當您針對 OU 的 User 物件執行 **Grant-CsOuPermission** Cmdlet 時，會將權限授與群組，如下表所示。

### User 物件的授與權限

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>群組</th>
<th>權限</th>
<th>適用對象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCHSUniversalServices</p></td>
<td><p>複寫目錄變更</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalServerReadOnlyGroup</p></td>
<td><p>列出內容</p>
<p>讀取所有屬性</p>
<p>讀取權限</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>列出內容</p>
<p>讀取所有屬性</p>
<p>讀取權限</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>讀取 RTCUserSearchPropertySet</p>
<p>Read RTCUserProvisioningPropertySet</p>
<p>讀取 RTCPropertySet</p>
<p>讀取 Public-Information</p>
<p>讀取 General-Information</p>
<p>讀取 User-Account-Restrictions</p></td>
<td><p>子系 User 物件</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>寫入 RTCUserSearchPropertySet</p>
<p>寫入 msExchUCVoiceMailSettings</p>
<p>寫入 RTCUserProvisioningPropertySet</p>
<p>寫入 RTCPropertySet</p>
<p>寫入 proxyAddresses</p></td>
<td><p>子系 User 物件</p></td>
</tr>
</tbody>
</table>


## 授與 Computer 物件的權限

當您針對 OU 的 Computer 物件執行 **Grant-CsOuPermission** Cmdlet 時，會將權限授與群組，如下表所示。

### Computer 物件的授與權限

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>群組</th>
<th>權限</th>
<th>適用對象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCHSUniversalServices</p></td>
<td><p>複寫目錄變更</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalServerReadOnlyGroup</p></td>
<td><p>列出內容</p>
<p>讀取所有屬性</p>
<p>讀取權限</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>列出內容</p>
<p>讀取所有屬性</p>
<p>讀取權限</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>讀取 Public-Information</p>
<p>讀取 Validated-DNS-Host-Name</p></td>
<td><p>子系 Computer 物件</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>讀取 Public-Information</p>
<p>讀取 Validated-DNS-Host-Name</p></td>
<td><p>子系 Computer 物件</p></td>
</tr>
</tbody>
</table>


## 授與 Contact 或 AppContact 物件的權限

當您針對 OU 的 Contact 或 AppContact 物件執行 **Grant-CsOuPermission** Cmdlet 時，會將權限授與群組，如下表所示。

### Contact 或 AppContact 物件的授與權限

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>群組</th>
<th>權限</th>
<th>適用對象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCHSUniversalServices</p></td>
<td><p>複寫目錄變更</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalServerReadOnlyGroup</p></td>
<td><p>列出內容</p>
<p>讀取所有屬性</p>
<p>讀取權限</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>列出內容</p>
<p>讀取所有屬性</p>
<p>讀取權限</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>讀取 RTCUserSearchPropertySet</p>
<p>讀取 RTCUserProvisioningPropertySet</p>
<p>讀取 RTCPropertySet</p>
<p>讀取 Public-Information</p>
<p>讀取 General-Information</p>
<p>讀取 Personal-Information</p>
<p>讀取 User-Account-Restrictions</p></td>
<td><p>子系 Contact 物件</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>寫入 RTCUserSearchPropertySet</p>
<p>寫入 otherIpPhone</p>
<p>寫入 displayName</p>
<p>寫入 description</p>
<p>寫入 telephoneNumber</p>
<p>寫入 msExchUCVoiceMailSettings</p>
<p>寫入 RTCUserProvisioningPropertySet</p>
<p>寫入 RTCPropertySet</p>
<p>寫入 proxyAddresses</p></td>
<td><p>子系 Contact 物件</p></td>
</tr>
</tbody>
</table>


## 授與 Device 物件的權限

當您針對 OU 的 Device 物件執行 **Grant-CsOuPermission** Cmdlet 時，會將權限授與群組，如下表所示。

### Device 物件的授與權限

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>群組</th>
<th>權限</th>
<th>適用對象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCHSUniversalServices</p></td>
<td><p>複寫目錄變更</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalServerReadOnlyGroup</p></td>
<td><p>列出內容</p>
<p>讀取所有屬性</p>
<p>讀取權限</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>列出內容</p>
<p>讀取所有屬性</p>
<p>讀取權限</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>讀取 RTCUserSearchPropertySet</p>
<p>讀取 RTCUserProvisioningPropertySet</p>
<p>讀取 RTCPropertySet</p>
<p>讀取 Public-Information</p>
<p>讀取 Personal-Information</p>
<p>讀取 General-Information</p>
<p>讀取 User-Account-Restrictions</p></td>
<td><p>子系 Contact 物件</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>建立子系</p>
<p>刪除子系</p>
<p>刪除樹狀目錄</p></td>
<td><p>Contact</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>寫入 displayName</p>
<p>寫入 description</p>
<p>寫入 telephoneNumber</p></td>
<td><p>子系 User 物件</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>寫入 RTCUserSearchPropertySet</p>
<p>寫入 otherIpPhone</p>
<p>寫入 displayName</p>
<p>寫入 description</p>
<p>寫入 telephoneNumber</p>
<p>寫入 msExchUCVoiceMailSettings</p>
<p>寫入 RTCUserProvisioningPropertySet</p>
<p>寫入 RTCPropertySet</p>
<p>寫入 proxyAddresses</p></td>
<td><p>子系 Contact 物件</p></td>
</tr>
</tbody>
</table>


## 授與 InetOrgPerson 物件的權限

當您針對 OU 的 InetOrgPerson 物件執行 **Grant-CsOuPermission** Cmdlet 時，會將權限授與群組，如下表所示。

### InetOrgPerson 物件的授與權限

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>群組</th>
<th>權限</th>
<th>適用對象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCHSUniversalServices</p></td>
<td><p>複寫目錄變更</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalServerReadOnlyGroup</p></td>
<td><p>列出內容</p>
<p>讀取所有屬性</p>
<p>讀取權限</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>列出內容</p>
<p>讀取所有屬性</p>
<p>讀取權限</p></td>
<td><p>只有此物件</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>讀取 RTCUserSearchPropertySet</p>
<p>讀取 RTCUserProvisioningPropertySet</p>
<p>讀取 RTCPropertySet</p>
<p>讀取 Personal-Information</p>
<p>讀取 Public-Information</p>
<p>讀取 General-Information</p>
<p>讀取 User-Account-Restrictions</p></td>
<td><p>子系 inetOrgPerson 物件</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>寫入 RTCUserSearchPropertySet</p>
<p>寫入 RTCUserProvisioningPropertySet</p>
<p>寫入 RTCPropertySet</p>
<p>寫入 proxyAddresses</p></td>
<td><p>子系 inetOrgPerson 物件</p></td>
</tr>
</tbody>
</table>

