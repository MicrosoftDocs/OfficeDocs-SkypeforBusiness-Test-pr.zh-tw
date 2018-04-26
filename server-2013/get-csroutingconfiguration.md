---
title: Get-CsRoutingConfiguration
TOCTitle: Get-CsRoutingConfiguration
ms:assetid: 37a1cbc9-b8b2-423c-8ebb-7947fdcad24e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425851(v=OCS.15)
ms:contentKeyID: 49290592
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRoutingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取路由組態物件，其包含了 Lync Server 部署中所定義之所有語音路由的清單。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsRoutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsRoutingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

此範例會擷取路由設定。若要擷取個別語音路由，請使用 **Get-CsVoiceRoute** Cmdlet。

    Get-CsRoutingConfiguration

## 詳細描述

語音路由所含的指示會指示 Lync Server 如何將 Enterprise Voice 使用者的來電，路由到公用交換電話網路 (PSTN) 或專用交換機 (PBX) 上的電話號碼。此 Cmdlet 用來擷取全域執行個體，此執行個體會保存 Lync Server 部署內定義的所有語音路由的清單。若要擷取個別語音路由，或以個別物件而非清單形式來擷取語音路由，請使用 **Get-CsVoiceRoute** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsRoutingConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRoutingConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此物件只能有一個執行個體，所以此參數不會進行任何動作。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之路由設定的範圍。唯一可能的值是 Global。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取路由組態，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsRoutingConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.Writable.Policy.Voice.PSTNRoutingSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsRoutingConfiguration](new-csroutingconfiguration.md)  
[Remove-CsRoutingConfiguration](remove-csroutingconfiguration.md)  
[Set-CsRoutingConfiguration](set-csroutingconfiguration.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

