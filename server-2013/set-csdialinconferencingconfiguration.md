---
title: Set-CsDialInConferencingConfiguration
TOCTitle: Set-CsDialInConferencingConfiguration
ms:assetid: 3300343f-c075-4b4f-aaa4-091dbf1fcd90
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425825(v=OCS.15)
ms:contentKeyID: 49290526
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDialInConferencingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改用以指定使用者加入或離開電話撥入式會議時，Lync Server 之回應方式的設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsDialInConferencingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsDialInConferencingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableNameRecording <$true | $false>] [-EntryExitAnnouncementsEnabledByDefault <$true | $false>] [-EntryExitAnnouncementsType <UseNames | ToneOnly>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改 Identity 為 site:Redmond 之電話撥入式會議組態設定的 EntryExitAnnoucements 屬性。在此範例中，EntryExitAnnouncementsType 屬性設為 ToneOnly。

    Set-CsDialInConferencingConfiguration -Identity site:Redmond -EntryExitAnnouncementsType "ToneOnly"

## 範例 2

範例 2 修改用於組織的所有電話撥入式會議組態設定。為達成此目的，命令會先使用 **Get-CsDialInConferencingConfiguration** Cmdlet 傳回所有電話撥入式會議設定的所有集合。然後再將這些集合管線傳送到 **Set-CsDialInConferencingConfiguration** Cmdlet，以將集合中每個項目的 EnableNameRecording 屬性設為 True ($True)。

    Get-CsDialInConferencingConfiguration | Set-CsDialInConferencingConfiguration -EnableNameRecording $True

## 範例 3

範例 3 會修改所有已在網站範圍設定的電話撥入式會議設定。為了執行此工作，命令會先使用 **Get-CsDialInConferencingConfiguration** Cmdlet 搭配 Filter 參數，以傳回在網站範圍設定之所有設定的集合；篩選值 "site:\*" 可將傳回的資料限制在 Identity 開頭為 "site:" 字串值的設定。接著將篩選後的集合管線傳送到 **Set-CsDialInConferencingConfiguration** Cmdlet，以修改集合中每個項目的 EnableNameRecording 屬性和 EntryExitAnnouncementsType 屬性。當命令執行完成時，所有在網站範圍設定的電話撥入式會議設定會將 EnableNameRecording 屬性設為 True，將 EntryExitAnnoucements 屬性設為 "UseNames"。

    Get-CsDialInConferencingConfiguration -Filter "site:*" | Set-CsDialInConferencingConfiguration -EnableNameRecording $True -EntryExitAnnouncementsType "UseNames"

## 詳細描述

當使用者加入 (或離開) 電話撥入式會議時，Lync Server 可以有不同的回應方式。例如，參與者在進入會議本身前，可能會被要求記錄他們的姓名。同樣的，系統管理員可決定他們是否要讓 Lync Server 宣告電話撥入式參與者已離開或加入會議。

您可以使用電話撥入式會議組態設定來管理這些會議的「加入行為」；這些設定可在全域範圍或網站範圍設定。當您首次安裝 Lync Server 時，唯一的電話撥入式會議組態設定是在全域範圍中；但您可以使用 **New-CsDialInConferencingConfiguration** Cmdlet 在網站範圍建立新的設定。此外，您可以使用 **Set-CsDialInConferencingConfiguration** Cmdlet 來修改任何這些組態設定 (全域範圍或網站範圍)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsDialInConferencingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDialInConferencingConfiguration"}

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
<td><p><em>EnableNameRecording</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定是否要求使用者在進入會議前要先記錄姓名。設為 True 可啟用姓名記錄；設為 False 則會略過姓名記錄。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>EntryExitAnnouncementsEnabledByDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，則每次參與者進入或離開會議時，都會播放宣告。如果設為 False (預設值)，則不會播放進入與離開宣告。</p></td>
</tr>
<tr class="even">
<td><p><em>EntryExitAnnouncementsType</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.EntryExitAnnouncementsType</p></td>
<td><p>指出當參與者進入或離開會議時，系統會採取的動件。(僅當 EntryExitAnnouncementsEnabledByDefault 已設為 True 時才會播放宣告)。有效值為：</p>
<p>UseNames。每當人員進入或離開會議時宣告該名人員的姓名 (例如「Ken Myer 正離開會議」)。</p>
<p>ToneOnly。每當參與者進入或離開會議時會播放聲音。</p>
<p>預設值是 UseNames。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指出要修改之電話撥入式會議組態設定的 Identity。若要參照全域設定，請使用下列語法：-Identity global。若要參照網站設定，請使用類似下列的語法：-Identity site:Redmond。請注意，如有指定 Identity，即無法使用萬用字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration 物件。**Set-CSDialInConferencingConfiguration** Cmdlet 接受電話撥入式會議組態物件的管線傳送執行個體。

## 傳回類型

**Set-CSDialInConferencingConfiguration** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsDialInConferencingConfiguration](get-csdialinconferencingconfiguration.md)  
[New-CsDialInConferencingConfiguration](new-csdialinconferencingconfiguration.md)  
[Remove-CsDialInConferencingConfiguration](remove-csdialinconferencingconfiguration.md)

