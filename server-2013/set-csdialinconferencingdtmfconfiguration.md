---
title: Set-CsDialInConferencingDtmfConfiguration
TOCTitle: Set-CsDialInConferencingDtmfConfiguration
ms:assetid: cc22353e-6c14-49b1-bf23-f952c100bfd8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398860(v=OCS.15)
ms:contentKeyID: 49292335
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDialInConferencingDtmfConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改電話撥入式會議所要使用的複頻式 (DTMF) 訊號設定。TMF 可讓撥電話參與會議的使用者使用其電話鍵盤控制會議設定 (例如自行設定靜音和解除靜音，或鎖定和解除鎖定會議)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsDialInConferencingDtmfConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsDialInConferencingDtmfConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AdmitAll <String>] [-AudienceMuteCommand <String>] [-CommandCharacter <String>] [-Confirm [<SwitchParameter>]] [-EnableDisableAnnouncementsCommand <String>] [-Force <SwitchParameter>] [-HelpCommand <String>] [-LockUnlockConferenceCommand <String>] [-MuteUnmuteCommand <String>] [-OperatorLineUri <String>] [-PrivateRollCallCommand <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令切換指派給啟用及停用宣告之命令的按鍵 (預設值為 9)，以及使其他參與者靜音及解除靜音之命令的鍵盤按鍵 (預設值為4) 適用於全域 DTMF 設定。為達此目的，會使用下列兩個不同的參數：EnableDisableAnnoucementsCommand (指定參數值 4) 和 AudienceMuteCommand (指定參數值 9)。由於未指定 Identity，因此這些變更將會影響全域 DTMF 設定。

    Set-CsDialInConferencingDtmfConfiguration -Identity global -EnableDisableAnnouncementsCommand 4 -AudienceMuteCommand 9

## 範例 2

範例 2 所示的命令是第一個範例之命令的變化。不過在這個案例中，變更會影響 Identity 為 site:Redmond 的 DTMF 設定。

    Set-CsDialInConferencingDtmfConfiguration -Identity site:Redmond -EnableDisableAnnouncementsCommand 4 -AudienceMuteCommand 9

## 範例 3

範例 3 所示的命令會停用 Redmond 網站的通話名單命令 (這是可播放所有參與會議之人員清單的功能)。若要停用此命令，請加入 PrivateRollCallCommand 參數並將參數值設為 $Null。這表示沒有任何鍵盤按鍵和此命令相關聯，而使用者也無法使用此命令。

    Set-CsDialInConferencingDtmfConfiguration -Identity "site:Redmond" -PrivateRollCallCommand $Null

## 範例 4

範例 4 是範例 3 的變化：此範例會停用在網站範圍設定之所有 DTMF 設定的點名命令。為達成此目的，命令會先使用 **Get-CsDialInConferencingDtmfConfiguration** Cmdlet 搭配 Filter 參數，以傳回在網站範圍設定的所有設定集合；篩選值 "site:\*" 可將傳回的資料限制在 Identity 開頭為字元 "site:" 的設定。然後將此篩選後的集合管線傳送到 **Set-CsDialInConferencingDtmfConfiguration** Cmdlet，以將 PrivateRollCallCommand 屬性的值設為 Null ($Null)。

    Get-CsDialInConferencingDtmfConfiguration -Filter "site:*" | Set-CsDialInConferencingDtmfConfiguration -PrivateRollCallCommand $Null

## 詳細描述

Lync Server 可讓使用者透過撥入電話以參與會議。撥入的使用者無法檢視視訊或與其他會議出席者交換立即訊息，但他們可以完整參與會議的音訊部分。

除了可以參與會議，使用者還可以使用其電話按鍵來管理選取的會議部分。(使用者所能管理的特定會議設定會取決於使用者是否為簡報者)。例如，根據預設使用者可以按其鍵盤上的數字鍵 6，自行設定靜音或解除靜音。參與者可以私下播放參與會議的所有其他人員名字，而簡報者可對所有會議出席者設定靜音或解除靜音，以及隨時有某人加入或離開會議時啟用或停用宣告播放。

像這些使用電話鍵盤來做選擇的功能稱為複頻式 (DTMF) 訊號：如果您曾經撥打電話號碼，並且接受指示，依照「英語請按 1，或西班牙語請按 2」的順序執行某些動作，即表示您已用過 DTMF 訊號。

**Set-CsDialInConferencingDtmfConfiguration** Cmdlet 讓您修改用來觸發 Lync Server 電話撥入式會議支援之命令的按鍵。

在修改 DTMF 命令時，請記住兩件事。第一，您只能使用數字鍵 0 到 9 等按鍵，鍵盤中的其他按鍵 (如 \# 鍵) 都不能使用。該規則存在一項例外狀況：CommandCharacter 參數僅允許使用星號鍵 (\*) 或井字鍵 (\#)，您不能將數值指派給 CommandCharacter 參數。不過，所有其他命令參數將只會接收數值。

第二，必須為命令指派專用鍵；例如按鍵 4 不可同時用於靜音/解除靜音以及鎖定/解除鎖定會議。意思是說，在修改指派給命令的按鍵時，您可能需要更換兩個不同命令所使用的按鍵。例如，如果要將按鍵 4 指派給 EnableDisableAnnouncementsCommand (預設值：9) 在同一命令中，應該將按鍵 9 指派給 AudienceMuteCommand。

若要停用命令，請將其值設為 Null ($Null)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsDialInConferencingDtmfConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDialInConferencingDtmfConfiguration"}

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
<td><p><em>AdmitAll</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出允許在大廳中等候的所有使用者立即加入會議要按的按鍵。預設值為 8。</p></td>
</tr>
<tr class="even">
<td><p><em>AudienceMuteCommand</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出會議主持人使會議中的其他人靜音時可以按的按鍵 (亦即，將主持人以外的任一個人設為靜音)。預設按鍵為 4。</p></td>
</tr>
<tr class="odd">
<td><p><em>CommandCharacter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出在命令一開始時要按的按鍵。預設的按鍵為星號鍵 (*)，其他唯一允許的值為井字鍵 (#)。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDisableAnnouncementsCommand</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出要按哪一個鍵來啟用或停用每次有人加入或離開會議時的宣告。預設按鍵為 9。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>HelpCommand</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出要按哪一個鍵才能私下播放所有 DTMF 命令的說明。預設按鍵為 1。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示要修改之 DTMF 設定集合的唯一識別碼。若要參考全域設定，請使用下列語法：-Identity global。若要參照在此網站範圍設定的集合，請使用如下語法：-Identity site:Redmond。請注意，如有指定 Identity，即無法使用萬用字元。</p>
<p>如果未指定此參數，則 <strong>Set-CsDialInConferencingDtmfConfiguration</strong> Cmdlet 將會修改全域 DTMF 設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DialInConferencingDtmfConfiguration 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>LockUnlockConferenceCommand</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出要按哪一個鍵來鎖定或解除鎖定會議。如果會議已鎖定，便不允許新的參與者加入會議，至少到會議解除鎖定前都不行。預設按鍵為 7。</p></td>
</tr>
<tr class="odd">
<td><p><em>MuteUnmuteCommand</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出您自己設為靜音或解除靜音時要按的按鍵；使用同一按鍵反覆切換靜音和解除靜音。預設按鍵為 6。</p></td>
</tr>
<tr class="even">
<td><p><em>OperatorLineUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>在使用者按下電話鍵盤上的 *0 時，撥入式會議自動語音應答即會將 PSTN 使用者連線至該電話號碼。按下 *0 的操作可將撥入式會議使用者連線至總機服務。</p></td>
</tr>
<tr class="odd">
<td><p><em>PrivateRollCallCommand</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出要私下播放會議每一個參與者的名稱時要按的按鍵。預設按鍵為 3。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingDtmfConfiguration 物件。**Set-CsDialInConferencingDtmfConfiguration** Cmdlet 接受電話撥入式會議 DTMF 組態物件管線傳送的執行個體。

## 傳回類型

**Set-CsDialInConferencingDtmfConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingDtmfConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsDialInConferencingDtmfConfiguration](get-csdialinconferencingdtmfconfiguration.md)  
[New-CsDialInConferencingDtmfConfiguration](new-csdialinconferencingdtmfconfiguration.md)  
[Remove-CsDialInConferencingDtmfConfiguration](remove-csdialinconferencingdtmfconfiguration.md)

