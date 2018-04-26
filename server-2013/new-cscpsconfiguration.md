---
title: New-CsCpsConfiguration
TOCTitle: New-CsCpsConfiguration
ms:assetid: bc740858-0e00-48ae-883e-67b3b7a03528
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412919(v=OCS.15)
ms:contentKeyID: 49292133
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsCpsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的通話駐留服務設定集合。通話駐留是可以讓使用者「駐留」來電的服務。駐留通話會將來電轉接到指定範圍或軌道內的號碼，然後立即將來電設為保留。任何人 (不只是原來接聽電話的人) 只要輸入正確的號碼，即可從任何電話回復通話。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsCpsConfiguration -Identity <XdsIdentity> [-CallPickupTimeoutThreshold <TimeSpan>] [-Confirm [<SwitchParameter>]] [-EnableMusicOnHold <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxCallPickupAttempts <Int32>] [-OnTimeoutURI <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會使用 **New-CsCpsConfiguration** Cmdlet 為網站 Redmond 建立通話駐留服務組態。這個組態將使用預設值建立 (除了 EnableMusicOnHold 以外)。這個命令將此屬性設定為 False，表示已駐留其通話的來電者在等待時不會聽到任何內容 (EnableMusicOnHold 預設為 True，假設已部署通話駐留服務)。

    New-CsCpsConfiguration -Identity site:Redmond -EnableMusicOnHold $False

## 範例 2

範例 2 所示的命令會使用 **New-CsCpsConfiguration** Cmdlet 為網站 Redmond1 建立通話駐留服務組態。預設不會提供 OnTimeoutURI，因此這個範例會新增該參數的值。在此範例中，OnTimeoutURI 設定為 sip:kenmyer@litwareinc.com。傳遞到此參數的值必須以字串 "sip:" 為開頭，而且應指向在指定的響鈴嘗試次數後要接到未接聽之保留通話的使用者或「回應群組」。

    New-CsCpsConfiguration -Identity site:Redmond -OnTimeoutURI sip:kenmyer@litwareinc.com

## 範例 3

這個命令使用 **New-CsCpsConfiguration** Cmdlet 為網站 Redmond1 建立通話駐留服務組態。將這個網站的 MaxCallPickupAttempts 設定為 2，表示來電最多撥回兩次。

    New-CsCpsConfiguration -Identity site:Redmond -MaxCallPickupAttempts 2

## 詳細描述

使用這個 Cmdlet 建立新的通話駐留服務組態。安裝通話保留服務時，預設會設定全域設定，可更新但無法移除 (「移除」全域設定只會將其重設為預設值)。因此這個 Cmdlet 用來只建立特定網站的設定。

通話駐留服務組態會指定駐留通話後的動作。例如，如果保留通話在一段時間內沒有回應，則可自動轉接其他人 (例如系統管理員) 或回應群組。可以設定來電在一段期間後響鈴，以確保不會忘掉來電。此外，可以設定通話駐留服務在駐留通話時，向等待的來電者播放的等候音樂。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsCpsConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsCpsConfiguration"}

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
<td><p>套用設定的網站。必須使用 site:&lt;網站名稱&gt; 的格式輸入，例如 site:Redmond。組態一律會存在於全域範圍且無法移除，如此便無法利用此 Cmdlet 重新建立全域組態。</p></td>
</tr>
<tr class="even">
<td><p><em>CallPickupTimeoutThreshold</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>從保留通話之後到回撥原先接聽來電的電話之前所經過的時間長度。</p>
<p>這必須使用 hh:mm:ss 的格式輸入 (hh = 小時、mm = 分鐘、ss = 秒)</p>
<p>預設值：00:01:30 (90 秒)；最小值：10 秒 (00:00:10)；最大值：10 分鐘 (00:10:00)</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMusicOnHold</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定保留通話時是否對來電者播放音樂。</p>
<p>Lync Server 隨附預設的等候音樂檔。您可以使用 <strong>Set-CsCallParkServiceMusicOnHoldFile</strong> Cmdlet 來變更此檔案 (進而變更在保留通話時來電者所聽到的音樂)。</p>
<p>預設值：True</p></td>
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
<td><p><em>MaxCallPickupAttempts</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>在放棄保留通話並轉接至遞補統一資源識別元 (URI) 之前，回撥接聽電話的次數。遞補 URI 會以 OnTimeoutURI 參數設定。</p>
<p>預設值：1；最大值：1; 最大值：10</p></td>
</tr>
<tr class="even">
<td><p><em>OnTimeoutURI</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>未接聽的保留通話將轉接的使用者或回應群組的 SIP 位址。在超過 MaxCallPickupAttempts 參數所定義的回撥次數之後，將轉接保留通話。如果該參數設為 Null，將忽略 OnTimeoutURI，且在嘗試響鈴失敗後保留的通話將斷線。</p>
<p>值必須是以字串 sip: 開頭的 SIP URI。例如，sip:rgs1@litwareinc.com。</p></td>
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

此 Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

