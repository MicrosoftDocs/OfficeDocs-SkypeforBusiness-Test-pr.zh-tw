---
title: Set-CsPresenceProvider
TOCTitle: Set-CsPresenceProvider
ms:assetid: 3f2e30d1-edb5-4839-a24f-11b77b699a1d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204833(v=OCS.15)
ms:contentKeyID: 49290699
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPresenceProvider

 

_**上次修改主題的時間：** 2015-03-09_

修改設定供組織使用的目前狀態提供者。目前狀態提供者代表 User Services 組態設定集合的 PresenceProviders 屬性。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsPresenceProvider [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPresenceProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會示範如何使用 **Set-CsPresenceProvider** Cmdlet 修改現有目前狀態提供者的 FQDN。為達成此目的，範例中的第一個命令會使用 **Get-CsPresenceProvider** Cmdlet 建立對 Identity 為 "global/contoso.com" 之目前狀態提供者的物件參照。此物件參照會儲存在名為 $x 的變數中。

第二個命令會將物件參照的 FQDN 屬性設為 contoso2.com，以做為新目前狀態提供者的 FQDN。設定 FQDN 屬性之後，會使用 **Set-CsPresenceProvider** Cmdlet 搭配 Instance 屬性，將這些變更寫入全域的 User Services 組態設定集合中。

    $x = Get-CsPresenceProvider -Identity "global/contoso.com" 
    $x.Fqdn = "contoso2.com"
    Set-CsPresenceProvider -Instance $x

## 詳細描述

**CsPresenceProvider** Cmdlet 可用於管理 User Services 組態設定中的 PresenceProviders 屬性。 此外，這些設定會用於維護目前狀態資訊，包括授權之目前狀態提供者的集合。 該集合會儲存在 PresenceProviders 屬性中。

**Set-CsPresenceProvider** Cmdlet 可用於修改目前設定供組織使用之目前狀態提供者的 FQDN。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPresenceProvider"}

**Lync Server 控制台：** **Set-CsPresenceProvider** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之目前狀態提供者的唯一識別碼。目前狀態提供者的 Identity 包含兩個部分：已套用規則的範圍 (Parent) (例如 service:UserServer:atl-cs-001.litwareinc.com)，以及 Fqdn 提供者。若要修改全域範圍的目前狀態提供者，請使用類似下列的語法：</p>
<p>-Identity &quot;global/fabrikam.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Set-CsPresenceProvider** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PresenceProvider\#Decorated 物件執行個體。

## 傳回類型

無。反之， **Set-CsPresenceProvider** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PresenceProvider\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPresenceProvider](get-cspresenceprovider.md)  
[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[New-CsPresenceProvider](new-cspresenceprovider.md)  
[Remove-CsPresenceProvider](remove-cspresenceprovider.md)

