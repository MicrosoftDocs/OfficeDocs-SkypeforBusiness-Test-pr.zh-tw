---
title: New-CsVoicemailReroutingConfiguration
TOCTitle: New-CsVoicemailReroutingConfiguration
ms:assetid: 37750c6d-9b75-4dde-aa52-79210afe34c2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425849(v=OCS.15)
ms:contentKeyID: 49290587
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoicemailReroutingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立設定提供電話號碼。如有啟用這些設定，當從分支網站之 Lync Server 到資料中心之 Lync Server Server 之間沒有可用的 IP 連線時，可以 Exchange UM 可以利用公用交換電話網路 (PSTN) 路由到這些電話號碼。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsVoicemailReroutingConfiguration -Identity <XdsIdentity> [-AutoAttendantNumber <String>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-SubscriberAccessNumber <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會建立套用到 Redmond1 網站的新語音信箱重新路由設定。Enabled 參數會設為 True 以開啟此組態，並提供電話號碼 (+14255551212) 以指定要將來電重新路由至哪一個自動語音應答。

    New-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -Enabled $True -AutoAttendantNumber "+14255551212"

## 範例 2

此範例會建立套用到 Redmond1 網站的新語音信箱重新路由設定。系統會提供電話號碼 (+14255551213) 以指定要將來電重新路由至哪一個使用者存取號碼。請注意，Enabled 參數尚未設定。Enabled 預設值為 False，所以 Enabled 屬性必須先設為 True，才會將使用者存取來電重新路由到這個號碼。

    New-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -SubscriberAccessNumber "+14255551213"

## 詳細描述

此 Cmdlet 可讓您建立在全域層級或網站層級套用的設定，這些設定可以決定當失去 IP 連線時，會透過 PSTN 將自動語音應答與使用者存取來電路由到哪一個位置。

「自動語音應答」與「使用者存取」是 Exchange UM 的功能。「自動語音應答」功能會提供語音辨識與按鍵觸控 (雙音多頻 (DTMF)) 功能供外部來電者導覽公司的電話系統，以連絡到所需的部門或員工，或在「留言模式」中接受使用者留言 (建議以使用「留言模式」重新路由語音)。「使用者存取」允許內部使用者使用電話存取 Microsoft Outlook 信箱。這些設定提供的號碼允許來電者在語音信箱留言，讓 Enterprise Voice 使用者 (AutoAttendantNumber 設定) 和這些使用者能夠擷取語音信箱，即使從遠端網站的 Lync Server 部署到資料中心的 Exchange UM 之間沒有 IP 連線可用 (SubscriberAccessNumber 設定) 也一樣。

請注意，Enabled 屬性必須設為 True，才能夠使用這些設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsVoicemailReroutingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoicemailReroutingConfiguration"}

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
<td><p>此參數包含一個唯一識別碼，該識別碼指定將此組態套用至哪個範圍。新的語音信箱重新路由組態只會在網站層級建立，因為 Identity 的格式是 Site:&lt;網站名稱&gt;，其中 &lt;網站名稱&gt; 是套用設定的網站名稱。由於全域語音信箱重新傳送組態為預設業已存在的組態，因此無法藉由呼叫 <strong>New-CsVoicemailReroutingConfiguration</strong> Cmdlet 來重新建立。</p></td>
</tr>
<tr class="even">
<td><p><em>AutoAttendantNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>語音信箱儲放嘗試應重新路由至哪一個自動語音應答的電話號碼。</p>
<p>提供給此參數的號碼必須是現有連絡人物件的 LineUri。</p>
<p>值的開頭必須是 1 到 9 的數字，前面可選擇性地加上加號 (+)，後面再加上任何數目的數字。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出當失去 IP 連線時，是否應透過 PSTN 重新路由存取語音信箱的嘗試。</p>
<p>預設值：False</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>SubscriberAccessNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>應將語音信箱擷取嘗試重新路由至哪一個使用者存取號碼。</p>
<p>提供給此參數的號碼必須是現有連絡人物件的 LineUri。</p>
<p>值的開頭必須是 1 到 9 的數字，前面可選擇性地加上加號 (+)，後面再加上任何數目的數字。</p></td>
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

無。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Set-CsVoicemailReroutingConfiguration](set-csvoicemailreroutingconfiguration.md)  
[Get-CsVoicemailReroutingConfiguration](get-csvoicemailreroutingconfiguration.md)

