---
title: Remove-CsDialInConferencingDtmfConfiguration
TOCTitle: Remove-CsDialInConferencingDtmfConfiguration
ms:assetid: 3cd6313c-fd0a-4fb2-bacd-b1bdf2a59430
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425894(v=OCS.15)
ms:contentKeyID: 49290662
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDialInConferencingDtmfConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除電話撥入式會議目前所使用之雙音多頻 (DTMF) 訊號設定的集合。DTMF 可讓撥電話參與會議的使用者使用其電話鍵盤控制會議設定 (例如自行設定靜音和解除靜音，或鎖定和解除鎖定會議)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsDialInConferencingDtmfConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會刪除 Identity 為 site:Redmond 之 DTMF 組態設定的集合。

    Remove-CSDialInConferencingDtmfConfiguration -Identity site:Redmond

## 範例 2

範例 2 所示的命令會刪除已在網站範圍設定的所有 DTMF 設定。若要執行此工作，此命令會先使用 **Get-CSDialInConferencingDtmfConfiguration** Cmdlet 和 Filter 參數，傳回已在網站範圍設定之所有 DTMF 設定的集合；篩選值 "site:\*" 可確保只會傳回 Identity 開頭為字串值 "site:" 的設定。才會傳回。接著，這個篩選過的集合會管線傳送到 **Remove-CSDialInConferencingConfiguration** Cmdlet，這會移除該集合中的每一個項目。

    Get-CSDialInConferencingDtmfConfiguration -Filter "site:*" | Remove-CSDialInConferencingDtmfConfiguration

## 範例 3

在範例 3 中，**Remove-CSDialInConferencingDtmfConfiguration** Cmdlet 是用於刪除 PrivateRollCallCommand 屬性等於 Null 值的所有 DTMF 設定。(亦即，已停用私人通話名單命令)。為達成此目的，命令會先使用 **Get-CSDialInConferencingDtmfConfiguration** Cmdlet 傳回組織目前所使用之所有 DTMF 設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 PrivateRollCallCommand 等於 Null 值的設定。接著將篩選後的集合管線管線傳送到 **Remove-CSDialInConferencingDtmfConfiguration** Cmdlet，以刪除集合中的每一個項目。

    Get-CSDialInConferencingDtmfConfiguration | Where-Object {$_.PrivateRollCallCommand -eq $Null} | Remove-CSDialInConferencingDtmfConfiguration

## 詳細描述

Lync Server 可讓使用者透過撥打電話來參與會議。撥入的使用者無法檢視視訊或與其他會議出席者交換立即訊息，但他們可以完整參與會議的音訊部分。

除了可以參與會議，使用者還可以使用其電話按鍵來管理選取的會議部分。(使用者所能管理的特定會議設定會取決於使用者是否為簡報者)。例如，根據預設，使用者可以按其鍵盤上的數字鍵 6，自行設定靜音或解除靜音。參與者可以私下播放參與會議的所有其他人員名字，而簡報者可對所有會議出席者設定靜音或解除靜音，以及隨時有某人加入或離開會議時啟用/停用宣告播放。

像這些使用電話鍵盤來做選擇的功能稱為雙音多頻 (DTMF) 訊號：如果您曾經撥打電話號碼，並且接受指示，依照「英語請按 1，或西班牙語請按 2」的順序執行某些動作，即表示您已用過 DTMF 訊號。

當您安裝 Lync Server 時，會為您建立全域的 DTMF 設定集合。除了這些全域設定外，您可以使用 **New-CSDialInConferencingDtmfConfiguration** Cmdlet 逐一建立各個網站的自訂設定。您在網站範圍建立的設定稍後可以使用 **Remove-CSDialInConferencingDtmfConfiguration** Cmdlet 移除。當您移除在網站範圍套用的 DTMF 設定時，受影響之網站的使用者會自動由全域 DTMF 組態設定管轄。

您也可以針對全域設定執行 **Remove-CSDialInConferencingDtmfConfiguration** Cmdlet。不過，如果您這樣做，將不會移除全域設定；那是因為您無法移除全域 DTMF 設定。而是將全域設定中的屬性重設為其預設值。例如，假設您已修改全域設定，將鍵 4 設為靜音/解除靜音鍵。此時，如果您對該全域設定執行 **Remove-CSDialInConferencingDtmfConfiguration** Cmdlet，則靜音/解除靜音鍵的值會重設為預設值 6。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsDialInConferencingDtmfConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDialInConferencingDtmfConfiguration"}

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
<td><p>要移除之 DTMF 設定集合的唯一識別碼。若要「移除」全域設定，請使用下列語法：-Identity global。(如前所述，您無法實際移除全域設定；您只能將屬性重設為其預設值)。若要修改在網站範圍設定的集合，請使用類似下列的語法：-Identity site:Redmond。您無法在指定 Identity 時使用萬用字元</p></td>
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
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingDtmfConfiguration 物件。**Remove-CsDialInConferencingDtmfConfiguration** Cmdlet 接受管線傳送的電話撥入式會議 DTMF 組態物件執行個體。

## 傳回類型

無。反之，**Remove-CSDialInConferencingDtmfConfiguration** Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingDtmfConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsDialInConferencingDtmfConfiguration](get-csdialinconferencingdtmfconfiguration.md)  
[New-CsDialInConferencingDtmfConfiguration](new-csdialinconferencingdtmfconfiguration.md)  
[Set-CsDialInConferencingDtmfConfiguration](set-csdialinconferencingdtmfconfiguration.md)

