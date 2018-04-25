---
title: Set-CsVoicemailReroutingConfiguration
TOCTitle: Set-CsVoicemailReroutingConfiguration
ms:assetid: c16a0d47-318b-46e4-991c-e4842403dbe3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412948(v=OCS.15)
ms:contentKeyID: 49292204
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoicemailReroutingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改提供存取 Exchange UM 使用者存取與自動語音應答功能所需之公共交換電話網路 (PSTN) 電話號碼的設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsVoicemailReroutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoicemailReroutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AutoAttendantNumber <String>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-SubscriberAccessNumber <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例可啟用 Redmond1 網站的語音信箱重新路由傳送組態設定。

    Set-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -Enabled $True

## 範例 2

此範例可修改套用至 Redmond1 網站的語音信箱重新路由傳送設定，將「使用者存取」的電話號碼設為 +14255551213。

    Set-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -SubscriberAccessNumber "+14255551213"

## 詳細描述

這個 Cmdlet 可讓您修改當和 Exchange UM 伺服器之間的 IP 連線中斷時，判斷應重新路由傳送「自動語音應答」和「使用者存取」通話之位置的設定。

「自動語音應答」和「使用者存取」是 Exchange UM 的功能。自動語音應答功能會提供語音辨識與按鍵觸控 (DTMF) 功能供外部來電者導覽公司的電話系統，以連絡到所需的部門或員工，或在留言模式中接受使用者留言(建議以使用留言模式重新路由語音)。使用者存取允許內部使用者使用電話存取 Microsoft Outlook 信箱。這些設定提供的號碼允許來電者在語音信箱留言，讓 Enterprise Voice 使用者 (AutoAttendantNumber 設定) 和這些使用者能夠擷取語音信箱，即使從遠端網站的 Lync Server 部署到資料中心的 Exchange UM 之間沒有 IP 連線可用 (SubscriberAccessNumber 設定) 也一樣。

請注意，Enabled 屬性必須設為 True，才能夠使用這些設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsVoicemailReroutingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoicemailReroutingConfiguration"}

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
<td><p><em>AutoAttendantNumber</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>語音信箱儲放嘗試應重新路由至哪一個自動語音應答的電話號碼。</p>
<p>提供給此參數的號碼必須是現有連絡人物件的 LineUri。</p>
<p>值的開頭必須是 1 到 9 的數字，前面可選擇性地加上加號 (+)，後面再加上任何數目的數字。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出當失去 IP 連線時，是否應透過 PSTN 重新路由存取語音信箱的嘗試。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsIdentity</p></td>
<td><p>您要修改之設定的唯一識別碼。針對這個 Cmdlet，Identity 可以是 Global 或 Site:&lt;網站名稱&gt;，其中，&lt;網站名稱&gt; 是設定套用所在之網站的名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>VoicemailReroutingConfiguration</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p>
<p>這個物件必須屬於 Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration 類型 (可呼叫 <strong>Get-CsVoicemailReroutingConfiguration</strong> Cmdlet 來擷取)。</p></td>
</tr>
<tr class="odd">
<td><p><em>SubscriberAccessNumber</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>應將語音信箱擷取嘗試重新路由至哪一個使用者存取號碼。</p>
<p>提供給此參數的號碼必須是現有連絡人物件的 LineUri。</p>
<p>值的開頭必須是 1 到 9 的數字，前面可選擇性地加上加號 (+)，後面再加上任何數目的數字。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration 物件。受語音信箱重新路由組態物件的管線傳送資料。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration 類型的物件。

## 請參閱

#### 其他資源

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Get-CsVoicemailReroutingConfiguration](get-csvoicemailreroutingconfiguration.md)

