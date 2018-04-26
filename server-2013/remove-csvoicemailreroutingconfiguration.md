---
title: Remove-CsVoicemailReroutingConfiguration
TOCTitle: Remove-CsVoicemailReroutingConfiguration
ms:assetid: 758cea84-5979-417c-a0cd-c76748e0da79
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398573(v=OCS.15)
ms:contentKeyID: 49291340
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoicemailReroutingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除提供存取 Exchange UM 使用者存取與自動語音應答功能所需之公共交換電話網路 (PSTN) 電話號碼的設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsVoicemailReroutingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除 Redmond1 網站的語音信箱重新路由組態設定。

    Remove-CsVoicemailReroutingConfiguration -Identity site:Redmond1

## 範例 2

此範例會移除此 Lync Server 部署的所有語音信箱重新路由設定。命令會先呼叫 **Get-CsVoicemailReroutingConfiguration** Cmdlet，以擷取所有語音信箱重新路由組態設定。然後再將此呼叫所擷取的設定管線傳送到 **Remove-CsVoicemailReroutingConfiguration** Cmdlet，以刪除每個設定。

    Get-CsVoicemailReroutingConfiguration | Remove-CsVoicemailReroutingConfiguration

## 詳細描述

此 Cmdlet 可讓您移除當失去 IP 連線時，決定透過 PSTN 將自動語音應答與使用者存取來電重新路由到哪一個位置的設定。

「自動語音應答」與「使用者存取」是 Exchange UM 的功能。「自動語音應答」功能會提供語音辨識與按鍵觸控 (雙音多頻 (DTMF)) 功能供外部來電者導覽公司的電話系統，以連絡到所需的部門或員工，或在「留言模式」中接受使用者留言 (建議以使用「留言模式」重新路由語音)。「使用者存取」允許內部使用者使用電話存取 Microsoft Outlook 信箱。這些設定提供的號碼允許來電者在語音信箱留言，讓 Enterprise Voice 使用者 (AutoAttendantNumber 設定) 和這些使用者能夠擷取語音信箱，即使從遠端網站的 Lync Server 部署到資料中心的 Exchange UM 之間沒有 IP 連線可用 (SubscriberAccessNumber 設定) 也一樣。

請注意，如果您呼叫此 Cmdlet 以移除全域設定，那些設定只會重設為預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsVoicemailReroutingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoicemailReroutingConfiguration"}

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
<td><p>您要移除之組態的唯一識別碼。針對這個 Cmdlet，Identity 可以是 Global 或 Site:&lt;網站名稱&gt;，其中，&lt;網站名稱&gt; 是設定套用所在之網站的名稱。</p></td>
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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration 物件。受語音信箱重新路由組態物件的管線傳送資料。

## 傳回類型

移除 Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration 類型的物件。

## 請參閱

#### 其他資源

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Set-CsVoicemailReroutingConfiguration](set-csvoicemailreroutingconfiguration.md)  
[Get-CsVoicemailReroutingConfiguration](get-csvoicemailreroutingconfiguration.md)

