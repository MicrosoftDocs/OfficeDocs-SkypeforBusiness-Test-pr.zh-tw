---
title: New-CsRoutingConfiguration
TOCTitle: New-CsRoutingConfiguration
ms:assetid: ead67e35-b145-4041-ba3e-4b26c47cce1d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399056(v=OCS.15)
ms:contentKeyID: 49292697
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRoutingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

此 Cmdlet 會傳回包含路由設定物件之預設值的物件。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRoutingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Route <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個命令會建立包含預設路由設定值的物件，並將該物件指派給變數 $x。此 Cmdlet 的任何其他用法都會傳回錯誤。

    $x = New-CsRoutingConfiguration -Identity global -InMemory

## 詳細描述

路由設定是 Lync Server 部署內定義之所有語音路由的容器。若要建立新的語立路由，請使用 **New-CsVoiceRoute** Cmdlet。

路由設定只能在全域等級進行定義。此外，您不能個別為路由設定進行命名；整個 Lync Server 部署只有一份語音路由清單。在 Lync Server 的 Windows PowerShell 實作中，如果嘗試呼叫以 New 動詞開始的 Cmdlet 來建立已經存在的物件，將會收到錯誤訊息。每個 Lync Server 實作都包含預設的路由設定物件，其具有 Global Identity。這意味著，唯一可以建立的語音路由清單已經存在。因此，呼叫 **New-CsRoutingConfiguration** Cmdlet 一定會傳回錯誤訊息，且不會建立新的路由設定。

唯一的例外是，您在呼叫此 Cmdlet 時指定了 InMemory 參數。這個命令只會在記憶體中建立物件，其中包含語音路由的預設清單。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRoutingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRoutingConfiguration"}

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
<td><p>路由組態的範圍。這個值必須是 Global。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，語音路由的管理將會同時考量撥打電話與接聽電話的位置。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>Route</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>針對 Lync Server 部署定義的所有語音路由清單 (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route 物件)。</p>
<p>您可以使用 <strong>New-CsVoiceRoute</strong> Cmdlet 建立語音路由物件。這是新增語音路由到此清單的建議方式。</p></td>
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

無。

## 傳回類型

可以建立 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnRoutingSettings 類型的記憶體內物件。

## 請參閱

#### 其他資源

[Remove-CsRoutingConfiguration](remove-csroutingconfiguration.md)  
[Set-CsRoutingConfiguration](set-csroutingconfiguration.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)  
[New-CsVoiceRoute](new-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

