---
title: Set-CsTenantPublicProvider
TOCTitle: Set-CsTenantPublicProvider
ms:assetid: 8341d801-bfa1-4c5b-9b80-5d503deebaf7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994047(v=OCS.15)
ms:contentKeyID: 52056157
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantPublicProvider

 

_**上次修改主題的時間：** 2015-03-09_

啟用和停用與協力廠商 IM 和目前狀態提供者 Windows Live、AOL 和 Yahoo 的通訊。啟用後，Microsoft Lync Online 使用者將可以與在指定的公用提供者上擁有帳戶的使用者交換 IM 和目前狀態資訊。

**Set-CsTenantPublicProvider** Cmdlet 僅可與 商務用 Skype Online 搭配使用。

## 語法

    Set-CsTenantPublicProvider -Tenant <String> [-Provider <String[]>] [-Verbose] [-WhatIf] [-Confirm]

## 範例

## 範例 1

範例 1 所示的命令會針對租用戶識別碼為 bf19b7db-6960-41e5-a139-2aa373474354 的租用戶，啟用與 Windows Live 的同盟。由於 Windows Live 是唯一指定的提供者，因此在執行命令後會停用 AOL 和 Yahoo 提供者。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

## 範例 2

範例 2 會啟用兩個公用提供者：Windows Live 和 AOL。這表示只會針對指定的租用戶停用 Yahoo 公用提供者。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive","AOL"

## 範例 3

範例 3 會示範如何針對指定租用戶停用所有公用提供者。若要達到此目的，只要將 Provider 屬性設定為空白字串 ("") 即可。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider ""

## 範例 4

範例 4 所示的命令會停用所有 Lync Online 租用戶的所有公用提供者。為了完成此工作，命令會先使用 **Get-CsTenant** Cmdlet 來傳回所有租用戶的集合。接著，此集合會以管道方式傳送到 **ForEach-Object** Cmdlet，以取得集合中的每個租用戶，再針對每個租用戶呼叫 **Set-CsTenantPublicProvider** Cmdlet，然後停用所有公用提供者。最後一項工作的作法是將 Provider 屬性設為空白字串 ("")。

    Get-CsTenant | ForEach-Object {Set-CsTenantPublicProvider -Tenant $_.TenantId -Provider ""}

## 詳細描述

公用提供者是為大眾提供 SIP 通訊服務的組織。當您與公用提供者建立同盟關係時，實際上是與擁有該提供者所提供帳戶的所有使用者建立同盟。例如，如果您與 Windows Live 結盟，您的使用者便能夠與任何具有 Windows Live 立即訊息帳戶的使用者交換立即訊息和目前狀態資訊。

Lync Online 可讓系統管理員選擇與下列一或多個公用 IM 和目前狀態提供者設定同盟：

  -   
    Windows Live

  -   
    AOL

  -   
    Yahoo\!

**Set-CsTenantPublicProvider** Cmdlet 可用於啟用或停用與其中任何公用提供者的同盟。使用此 Cmdlet 時，請注意，每當您執行 **Set-CsTenantPublicProvider** Cmdlet 時，必須指定應啟用的所有提供者。例如，假設已停用全部三個提供者，而且您執行此命令：

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

如您的般期，這將啟用 Windows Live，並維持停用 AOL 和 Yahoo。

現在，假設您接下來會執行下列命令：

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL"

該命令將啟用 AOL，但也會停用 Windows Live，因為您未將 Windows Live 指定為參數值的一部分來提供給 Provider 參數。若要啟用 AOL 並同時啟用 Windows Live，必須在呼叫 Set-CsTenantPublicProvider 時指定 AOL 和 Windows Live 二者：

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL","WindowsLive"

若要停用全部三個提供者的同盟，請將 Provider 屬性設為空白字串 ("")：

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider ""

請注意，若僅啟用公用提供者的狀態，不代表使用者就可與在該提供者上擁有帳戶的使用者交換立即訊息和目前狀態資訊。除了要與提供者本身締結同盟外，系統管理員也必須將同盟組態設定的 AllowPublicUsers 屬性設為 True。若將此屬性設為 False，則不論公用提供者的組態設定為何，您都無法與任何公用提供者通訊。

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>必要</p></td>
<td><p>System.Guid</p></td>
<td><p>要修改公用提供者設定之租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令以傳回每個租用戶的租用戶識別碼：</p>
<pre><code>Get-CsTenant | Select-Object DisplayName, TenantID</code></pre>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Provider</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>指出將允許使用者通訊的一或多個公用提供者。有效值為：</p>
<p>* AOL</p>
<p>* WindowsLive</p>
<p>* Yahoo</p>
<p>請注意，設定公用提供者時，將啟用 Provider 參數值中包含的任何提供者，並將停用參數值不包含的任何提供者。例如，此語法只會啟用 Yahoo，同時停用 Windows Live 和 AOL：</p>
<p>-Provider &quot;AOL&quot;</p>
<p>您可使用逗號分隔提供者名稱來啟用多個提供者：</p>
<p>-Provider &quot;AOL&quot;,&quot;WindowsLive&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Set-CsTenantPublicProvider** Cmdlet 接受以管道方式傳送的 Microsoft.Rtc.Management.Hosted.TenantPICStatus 物件執行個體。

## 傳回類型

無。反之，**Set-CsTenantPublicProvider** Cmdlet 會修改 Microsoft.Rtc.Management.Hosted.TenantPICStatus 物件的現有執行個體。

## 請參閱

#### 其他資源

[Get-CsTenantPublicProvider](get-cstenantpublicprovider.md)

