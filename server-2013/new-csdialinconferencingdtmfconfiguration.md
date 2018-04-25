---
title: New-CsDialInConferencingDtmfConfiguration
TOCTitle: New-CsDialInConferencingDtmfConfiguration
ms:assetid: 2e373bab-fc4c-4b8b-96e7-fc23ac3bcf47
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425792(v=OCS.15)
ms:contentKeyID: 49290461
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDialInConferencingDtmfConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的雙音多頻 (DTMF) 訊號設定集合，供電話撥入式會議使用。DTMF 可讓撥電話參與會議的使用者使用其電話鍵盤控制會議設定 (例如自行設定靜音和解除靜音，或鎖定和解除鎖定會議)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsDialInConferencingDtmfConfiguration -Identity <XdsIdentity> [-AdmitAll <String>] [-AudienceMuteCommand <String>] [-CommandCharacter <String>] [-Confirm [<SwitchParameter>]] [-EnableDisableAnnouncementsCommand <String>] [-Force <SwitchParameter>] [-HelpCommand <String>] [-InMemory <SwitchParameter>] [-LockUnlockConferenceCommand <String>] [-MuteUnmuteCommand <String>] [-OperatorLineUri <String>] [-PrivateRollCallCommand <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會為 Redmond 網站建立一組新的 DTMF 組態設定。在此範例中，將 MuteUnmuteCommand 屬性設為 4，將 AudienceMuteCommand 屬性設為 6。

    New-CSDialInConferencingDtmfConfiguration -Identity site:Redmond -MuteUnmuteCommand 4 -AudienceMuteCommand 6

## 範例 2

範例 2 會為 Redmond 網站建立一組新的 DTMF 組態設定。在此範例中停用了 AdmitAll 屬性；作法是使用 AdmitAll 參數並將參數值設為 Null。

    New-CSDialInConferencingDtmfConfiguration -Identity site:Redmond -AdmitAll $Null

## 範例 3

範例 3 示範如何使用 InMemory 參數建立僅存在記憶體中的 DTMF 組態設定集合執行個體，修改這些設定，然後使用 **Set-CSDialInConferencingDtmfConfiguration** Cmdlet 建立實際集合 (Identity 為 site:Redmond)。為達成此目的，範例中的第一個命令會建立 DTMF 組態設定集合只存在於記憶體中的新執行個體，並將該執行個體儲存於名為 $x 的變數中。這些設定只存在於記憶體中；如果關閉 Windows PowerShell 或刪除變數 $x，這些設定會消失，因此絕不會套用到 Redmond 網站。

接下來的 3 個命令修改此「虛擬」DTMF 設定集合的屬性：命令 2、3、4 分別指派新的值給 AdmitAll、MuteUnmuteCommand、AudienceMuteCommand。然後，最後一個命令使用 **Set-CSDialInConferencingDtmfConfiguration** Cmdlet 和參數 Instance，將儲存於 $x 的虛擬設定轉換為已為 Redmond 網站設定的實際設定集合。

    $x = New-CSDialInConferencingDtmfConfiguration -Identity site:Redmond -InMemory
    $x.AdmitAll = $Null
    $x.MuteUnmuteCommand = 4 
    $x.AudienceMuteCommand = 6
    Set-CSDialInConferencingDtmfConfiguration -Instance $x

## 詳細描述

Lync Server 可讓使用者透過撥打電話來參與會議。撥入的使用者無法檢視視訊或與其他會議出席者交換立即訊息，但他們可以完整參與會議的音訊部分。

除了可以參與會議，使用者還可以使用其電話按鍵來管理選取的會議部分。(使用者所能管理的特定會議設定會取決於使用者是否為簡報者)。例如，根據預設，使用者可以按其鍵盤上的數字鍵 6，自行設定靜音或解除靜音。參與者可以私下播放參與會議的所有其他人員名字，而簡報者可對所有會議出席者設定靜音或解除靜音，以及隨時有某人加入或離開會議時啟用或停用宣告播放。

像這些使用電話鍵盤來做選擇的功能稱為複頻式 (DTMF) 訊號：如果您曾經撥打電話號碼，並且接受指示，依照「英語請按 1，或西班牙語請按 2」的順序執行某些動作，即表示您已用過 DTMF 訊號。

當您安裝 Lync Server，會為您建立全域的 DTMF 設定集合。除了這些全域設定外，您可以使用 **New-CSDialInConferencingDtmfConfiguration** Cmdlet 逐一建立各個網站的自訂設定。例如，您可以為 Redmond 網站建立新的設定集合 (且只用於 Redmond 網站)，改用按鍵 4 代替按鍵 6 做為靜音/解除靜音鍵。請注意，任何在網站範圍進行的設定，其優先順序高於在全域範圍進行的設定。因此，雖然全域設定使用按鍵 6 做為靜音/解除靜音鍵，Redmond 網站的使用者將使用按鍵 4 做為靜音/解除靜音鍵。

每個網站只能有一個 DTMF 設定集合與一個全域集合。例如，假設您已經有一個 Identity 為 site:Redmond 的集合，而您想執行這個命令：

New- CSDialInConferencingDtmfConfiguration –Identity site:Redmond

此命令將失敗，因為 site:Redmond 集合已存在。如果您想修改 Redmond 網站的設定，可使用 **Set-CSDialInConferencingDtmfConfiguration** Cmdlet，或是先移除現有的集合，然後使用 Identity site:Redmond 建立新集合。

在設定 DTMF 命令的值時，請記住兩件事。第一，您只能使用數字鍵 0 到 9 和星號 (\*)，鍵盤上的任何其他按鍵 (如 \# 鍵) 都不能使用。(該規則有一項例外狀況：CommandCharacter 鍵只接受 \* 鍵或 \# 鍵。)第二，必須為命令指派專用鍵；例如按鍵 4 不可同時用於靜音/解除靜音以及鎖定/解除鎖定會議。也就是說，在修改指派給命令的按鍵時，您可能需要更換兩個不同命令所使用的按鍵。例如，如果要將按鍵 4 指派給 EnableDisableAnnouncementsCommand (預設值：9)，在同一命令中，應該將按鍵 9 指派給 MuteUnmuteAllCommand。

若要停用命令，請將其值設為 Null ($Null)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsDialInConferencingDtmfConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDialInConferencingDtmfConfiguration"}

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
<td><p>要指派給新的 DTMT 組態設定集合的唯一識別碼。由於您只能在網站範圍建立新集合，因此，Identity 一律是首碼 &quot;site:&quot; 加上網站名稱，例如 &quot;site:Redmond&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>AdmitAll</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出允許在大廳中等候的所有使用者立即加入會議要按的按鍵。預設值為 8。</p></td>
</tr>
<tr class="odd">
<td><p><em>AudienceMuteCommand</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出會議主持人可以按哪一個按鍵，將會議中的其他人設為靜音或解除靜音 (亦即，將主持人以外的任何人設為靜音或解除靜音)。預設按鍵為 4。</p></td>
</tr>
<tr class="even">
<td><p><em>CommandCharacter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出在命令一開始時要按的按鍵。預設按鍵是星號 (*)。其他唯一允許的值是 #。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDisableAnnouncementsCommand</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出要按哪一個鍵來啟用或停用每次有人加入或離開會議時的宣告。預設按鍵為 9。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>HelpCommand</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出要按哪一個鍵才能私下播放所有 DTMF 命令的說明。預設按鍵為 1。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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
<td><p>指出要私下播放每一個會議參與者的名稱時要按的按鍵。預設按鍵為 3。</p></td>
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

無。**New-CsDialInConferencingDtmfConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingDtmfConfiguration 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsDialInConferencingDtmfConfiguration](get-csdialinconferencingdtmfconfiguration.md)  
[Remove-CsDialInConferencingDtmfConfiguration](remove-csdialinconferencingdtmfconfiguration.md)  
[Set-CsDialInConferencingDtmfConfiguration](set-csdialinconferencingdtmfconfiguration.md)

