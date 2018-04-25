---
title: Remove-CsPresenceProvider
TOCTitle: Remove-CsPresenceProvider
ms:assetid: 7e8b540e-484f-4003-8665-18e2b3974f33
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205036(v=OCS.15)
ms:contentKeyID: 49291453
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPresenceProvider

 

_**上次修改主題的時間：** 2015-03-09_

移除設定供組織使用的目前狀態提供者。目前狀態提供者代表 User Services 組態設定集合的 PresenceProviders 屬性。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsPresenceProvider -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除 Identity 為 "global/fabrikam.com" 的目前狀態提供者。

    Remove-CsPresenceProvider -Identity "global/fabrikam.com"

## 範例 2

範例 2 會移除設定供組織使用的所有目前狀態提供者。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsPresenceProvider** Cmdlet，以傳回所有設定之目前狀態提供者的集合。然後，此集合會管線傳送到 **Remove-CsPresenceProvider** Cmdlet，以刪除集合中的每個項目 (也就是每個提供者)。

    Get-CsPresenceProvider | Remove-CsPresenceProvider

## 範例 3

範例 3 顯示如何刪除 Fqdn 中包含 "fabrikam.com" 字串值的所有目前狀態提供者。為了執行此工作，命令會先使用 **Get-CsPresenceProvider** Cmdlet 傳回所有可用之目前狀態提供者的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Fqdn 屬性包含 (-match) "fabrikam.com" 字串值的提供者。接著將篩選後的集合管線傳送到 **Remove-CsPresenceProvider** Cmdlet，以刪除篩選後之集合中的每個提供者。

    Get-CsPresenceProvider | Where-Object {$_.Fqdn -match "fabrikam.com"} | Remove-CsPresenceProvider

## 詳細描述

**CsPresenceProvider** Cmdlet 可用於管理 User Services 組態設定中的 PresenceProviders 屬性。 此外，這些設定會用於維護目前狀態資訊，包括授權之目前狀態提供者的集合。 該集合會儲存在 PresenceProviders 屬性中。

**Remove-CsPresenceProvider** Cmdlet 可讓您從一或多個 User Services 組態設定集合的 PresenceProviders 屬性移除目前狀態提供者。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPresenceProvider"}

**Lync Server 控制台：** **Remove-CsPresenceProvider** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>所要移除之目前狀態提供者的唯一識別碼。若要移除單一提供者，請使用該提供者的實際 Identity，其中包含範圍和提供者 Fqdn：</p>
<p>-Identity &quot;global/fabrikam.com&quot;</p>
<p>若要移除在特定範圍設定的所有目前狀態提供者，直接將範圍用做 Identity 即可。此語法會移除在全域範圍設定的所有提供者：</p>
<p>-Identity &quot;global&quot;</p></td>
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
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

**Remove-CsPresenceProvider** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PresenceProvider\#Decorated 物件執行個體。

## 傳回類型

無。反之， **Remove-CsPresenceProvider** Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PresenceProvider\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsPresenceProvider](get-cspresenceprovider.md)  
[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[New-CsPresenceProvider](new-cspresenceprovider.md)  
[Set-CsPresenceProvider](set-cspresenceprovider.md)

