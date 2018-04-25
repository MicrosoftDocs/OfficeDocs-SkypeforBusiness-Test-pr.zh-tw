---
title: New-CsDialInConferencingConfiguration
TOCTitle: New-CsDialInConferencingConfiguration
ms:assetid: ac0b6e22-3883-4884-aa94-18f4029c7f1e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412816(v=OCS.15)
ms:contentKeyID: 49291965
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDialInConferencingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的電話撥入式會議組態設定集合。這些設定可指定使用者加入或離開電話撥入式會議時，Lync Server 的回應方式。特別是傳回加入會議時，是否需要記錄參與者名稱訊，以及系統如何 (或是否需要) 宣告有人加入或離開通話。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsDialInConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableNameRecording <$true | $false>] [-EntryExitAnnouncementsEnabledByDefault <$true | $false>] [-EntryExitAnnouncementsType <UseNames | ToneOnly>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立套用到 Redmond 網站的電話撥入式會議組態設定集合。此外，為了設定 EnableNameRecording 屬性為 False，也包含了 EnableNameRecording 選用參數。

    New-CSDialInConferencingConfiguration -Identity site:Redmond -EnableNameRecording $False

## 範例 2

範例 2 的 InMemory 參數可用來建立電話撥入式會議組態設定的新集合，該設定一開始僅存於記憶體內。為達成此目的，此範例會先呼叫 **New-CSDialInConferencingConfiguration** Cmdlet 搭配 InMemory 參數，以建立儲存在變數 $x 中的虛擬設定集合 (請注意，此集合己指定 Identity 為 site:Redmond)。建立虛擬集合後，會使用第 2 行來修改 EnableNameRecording 屬性的值。最後，範例的第 3 行會呼叫 **Set-CSDialInConferencingConfiguration** Cmdlet，將儲存在 $x 中的虛擬組態設定轉換為套用到 Redmond 網站的實際設定集合。

    $x = New-CSDialInConferencingConfiguration -Identity site:Redmond -InMemory
    $x.EnableNameRecording = $False
    Set-CSDialInConferencingConfiguration -Instance $x

## 詳細描述

當使用者加入 (或離開) 電話撥入式會議時，Lync Server 可以使用不同方式回應。例如，可能會要求參與者必須在進入會議前記錄他們的名字。同樣地，系統管理員可以決定是否要讓 Lync Server 宣告電話撥入式參與者已離開或加入會議。

這些會議「參與行為」是使用電話撥入式會議組態設定來管理；這些設定可在全域範圍或網站範圍上設定(在網站範圍設定的設定優先於在全域範圍設定的設定)。當您首次安裝 Lync Server 時，唯一的電話撥入式會議組態設定是在全域範圍中；但您可以使用 **New-CSDialInConferencingConfiguration** Cmdlet 在網站範圍建立新的設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsDialInConferencingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDialInConferencingConfiguration"}

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
<td><p>XdsIdentity</p></td>
<td><p>指出要建立之電話撥入式會議組態設定的 Identity。因為這些設定只能在網站範圍上建立，所以使用類似如下含首碼 &quot;site:&quot; 的語法，後面再加上網站的名稱：-Identity site:Redmond。</p>
<p>請注意，每個網站只能有一個電話撥入式會議組態設定集合。如果已經有包含 Identity 為 site:Redmond 的設定集合存在，則範例命令會失敗。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableNameRecording</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>決定是否要求使用者在進入會議前要先記錄姓名。設為 True ($True) 會記錄姓名；設為 False ($False) 則會略過姓名記錄。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>EntryExitAnnouncementsEnabledByDefault</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>如果設為 True，則每次參與者進入或離開會議時，都會播放宣告。如果設為 False (預設值)，則不會播放進入與離開宣告。</p></td>
</tr>
<tr class="odd">
<td><p><em>EntryExitAnnouncementsType</em></p></td>
<td><p>選用</p></td>
<td><p>EntryExitAnnouncementsType</p></td>
<td><p>指出當參與者進入或離開會議時，系統會採取的動件。有效值為：</p>
<p>UseNames。每當人員進入或離開會議時宣告該名人員的姓名 (例如「Ken Myer 正離開會議」)。</p>
<p>ToneOnly。每當參與者進入或離開會議時會播放聲音。</p>
<p>預設值是 UseNames。請注意，唯有當 EntryExitAnnouncementsEnabledByDefault 內容已設定為 True 時，才會播放宣告。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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

無。**New-CsDialInConferencingConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsDialInConferencingConfiguration](get-csdialinconferencingconfiguration.md)  
[Remove-CsDialInConferencingConfiguration](remove-csdialinconferencingconfiguration.md)  
[Set-CsDialInConferencingConfiguration](set-csdialinconferencingconfiguration.md)

