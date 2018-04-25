---
title: Lync Server 2013 中的結構描述變更
TOCTitle: Lync Server 2013 中的結構描述變更
ms:assetid: d760cb93-77d4-4d64-adb7-416b808f36f8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398944(v=OCS.15)
ms:contentKeyID: 49292451
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的結構描述變更

 

_**上次修改主題的時間：** 2015-03-09_

在部署和操作 Lync Server 2013 之前，您必須先延伸架構以準備好 Active Directory 網域服務。架構延伸會新增 Lync Server 2013 所需的類別和屬性。

Lync Server 2013 需要幾個新的類別和屬性，並修改一些現有的類別和屬性。此外，大部分的 Lync Server 2013 設定資訊是儲存在中央管理存放區中，不像舊版是儲存在 AD DS 中。Lync Server 2013 中的下列資訊仍儲存在 AD DS 中：

  - **架構延伸：**
    
      - 使用者物件延伸
    
      - Office Communications Server 2007 和 Office Communications Server 2007 R2 類別的延伸可維持與支援之舊版的回溯相容性

<!-- end list -->

  - **資料** (儲存在 Lync Server 延伸架構和現有的架構類別中)：
    
      - 使用者 SIP 統一資源識別項 (URI) 及其他使用者設定
    
      - 回應群組與會議服務員等應用程式的連絡人物件
    
      - 中央管理存放區的指標
    
      - Kerberos 驗證帳戶 (選用的電腦物件)

本主題描述 Lync Server 2013 所需的 Active Directory 架構變更。它並未描述舊版 Office Communications Server 引進的架構變更。如需類別及其描述的清單，請參閱＜[Lync Server 2013 中的架構類別和描述](lync-server-2013-schema-classes-and-descriptions.md)＞。如需屬性及其描述的清單，請參閱＜[Lync Server 2013 中的架構屬性和描述](lync-server-2013-schema-attributes-and-descriptions.md)＞。如需類別及其中可能包含之屬性的清單，請參閱＜[Lync Server 2013 中的架構屬性 (按類別)](lync-server-2013-schema-attributes-by-class.md)＞。

msRTCSIP 前置詞會識別 Lync Server 特有的類別和屬性。

## 新的 Active Directory 屬性

下表描述由 Lync Server 2013 新增的 Active Directory 類別。

### 由 Lync Server 2013 新增的屬性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>msExchUserHoldPolicies</p></td>
<td><p>此多重值屬性保留使用者套用之保留原則的識別碼。保留原則會在保留期間保留使用者的信箱項目。這是與 Exchange 2013 共用的屬性。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UserRoutingGroupId</p></td>
<td><p>這是 SIP 路由群組識別碼。相同群組中的使用者將登錄至同一部前端伺服器。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MirrorBackEndServer</p></td>
<td><p>此屬性是用來儲存前端集區使用的鏡像 SQL Server 後端。</p></td>
</tr>
</tbody>
</table>


## 已修改的 Active Directory 類別

下表描述由 Lync Server 2013 修改的 Active Directory 類別。

### 由 Lync Server 2013 修改的類別

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>類別</th>
<th>變更</th>
<th>類別或屬性</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用者</p></td>
<td><p>新增：mayContain</p>
<p>新增：mayContain</p></td>
<td><p>ProxyAddresses</p>
<p>msRTCSIP-UserRoutingGroupId</p></td>
</tr>
<tr class="even">
<td><p>Contact</p></td>
<td><p>新增：mayContain</p>
<p>新增：mayContain</p></td>
<td><p>ProxyAddresses</p>
<p>msRTCSIP-UserRoutingGroupId</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>新增：mayContain</p></td>
<td><p>msExchUserHoldPolicies</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-GlobalTopologySetting</p></td>
<td><p>新增：mayContain</p></td>
<td><p>msRTCSIP-MirrorBackEndServer</p></td>
</tr>
</tbody>
</table>

