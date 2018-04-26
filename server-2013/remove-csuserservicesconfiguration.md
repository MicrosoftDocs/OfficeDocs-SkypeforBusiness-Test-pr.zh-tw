---
title: Remove-CsUserServicesConfiguration
TOCTitle: Remove-CsUserServicesConfiguration
ms:assetid: 8eed6091-ab96-49d4-a0c0-d1f9180a0b90
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398722(v=OCS.15)
ms:contentKeyID: 49291629
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUserServicesConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的 User Services 組態設定集合。User Services 可用於維護目前狀態資訊及管理會議。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsUserServicesConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除 Redmond 網站的 User Services 組態設定 (-identity site:Redmond)。

    Remove-CsUserServicesConfiguration -Identity site:Redmond

## 範例 2

範例 2 會刪除服務範圍所套用的所有 User Services 組態設定。為達成此目的，命令會呼叫 **Get-CsUserServicesConfiguration** Cmdlet 並搭配 Filter 參數。篩選值 "service:\*" 可將傳回的資料限制在服務範圍中的設定 (亦即，Identity 開頭為字元 "service:" 的設定)。然後再將篩選後的集合管線傳送到 **Remove-CsUserServicesConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsUserServicesConfiguration -Filter "service:*:" | Remove-CsUserServicesConfiguration

## 範例 3

範例 3 會移除允許使用者能有超過 250 位連絡人的所有 User Services 組態設定。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsUserServicesConfiguration** Cmdlet，以傳回目前使用之所有 User Services 組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 MaxContacts 屬性的值大於 250 的設定。接著將那些設定管線傳送到 **Remove-CsUserServicesConfiguration** Cmdlet 加以移除。

    Get-CsUserServicesConfiguration | Where-Object {$_.MaxContacts -gt 250} | Remove-CsUserServicesConfiguration

## 詳細描述

Lync Server 依賴 User Services 協助維護使用者的目前狀態資訊，以及管理會議。然後，**CsUserServicesConfiguration** Cmdlet 用於管理全域範圍、網站範圍和服務範圍的 User Services 組態設定 (請注意，可主控 User Services 組態設定的唯一服務為 User Services 本身)。這些設定有助於決定使用者可擁有的連絡人數目、使用者可在任何一個時間中排程的會議數，以及所指定的會議可保持為作用中的時間長度等作業。

**Remove-CsUserServicesConfiguration** Cmdlet 可讓您刪除已在網站或服務範圍套用的 User Services 組態設定。此 Cmdlet 也可以針對全域集合執行。不過，在該情況下，將不會刪除全域設定；因為您無法刪除全域設定，而是會將全域集合內的所有屬性都重設為預設值。例如，如果您已將全域設定中 MaxContacts 的值變更為 500，然後執行 **Remove-CsUserServicesConfiguration** Cmdlet，則 MaxContacts 將會重設為預設值 250。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsUserServicesConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUserServicesConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要移除之 User Services 組態設定的唯一識別碼。若要移除在網站範圍設定的設定，請使用類似下列的語法：-Identity site:Redmond。若要刪除服務層級的設定，請使用類似下列的語法：-Identity service:UserServer:atl-cs-001.litwareinc.com。</p>
<p>您也可以針對全域集合執行 <strong>Remove-CsUserServicesConfiguration</strong> Cmdlet。不過，在該情況下，將不會刪除全域集合，而是將該集合中的所有屬性重設為預設值。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>抑制顯示執行命令時可能引起的任何非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.UserServicesSettings 物件。**Remove-CsUserServicesConfiguration** Cmdlet 接受管線傳送的 User Services 設定物件執行個體。

## 傳回類型

無。反之，**Remove-CsUserServicesConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.UserServicesSettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[New-CsUserServicesConfiguration](new-csuserservicesconfiguration.md)  
[Set-CsUserServicesConfiguration](set-csuserservicesconfiguration.md)

