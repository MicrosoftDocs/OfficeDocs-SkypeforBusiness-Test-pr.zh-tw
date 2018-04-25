---
title: Set-CsCpsConfiguration
TOCTitle: Set-CsCpsConfiguration
ms:assetid: 9c2c0ad1-12f8-47b6-a7ec-60d91c9685bf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412721(v=OCS.15)
ms:contentKeyID: 49291794
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCpsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的通話駐留服務設定集合。通話駐留是可以讓使用者「駐留」來電的服務。駐留通話會將來電轉接到指定範圍或軌道內的號碼，然後立即將來電設為保留。任何人 (不只是原來接聽電話的人) 只要輸入正確的號碼，即可從任何電話回復通話。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsCpsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCpsConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-CallPickupTimeoutThreshold <TimeSpan>] [-Confirm [<SwitchParameter>]] [-EnableMusicOnHold <$true | $false>] [-Force <SwitchParameter>] [-MaxCallPickupAttempts <Int32>] [-OnTimeoutURI <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改 Identity 為 site:Redmond1 的通話保留服務組態，方法是將保留的通話將回撥給接聽電話的次數上限設為 2。作法是加入 MaxCallPickupAttempts 參數，並將該參數值設為 2。

    Set-CsCpsConfiguration -Identity site:Redmond1 -MaxCallPickupAttempts 2

## 範例 2

範例 2 是範例 1 所示命令的變化；不過在此範例中，會將所有 (並非只一個) 通話保留服務組態的 MaxCallPickupAttempts 屬性值設為 2。為達成此目的，會使用 **Get-CsCpsConfiguration** Cmdlet 擷取組織使用之所有通話保留服務設定的集合。然後，將此集合管線傳送至 **Set-CsCpsConfiguration** Cmdlet，將集合中每個項目的 MaxCallPickupAttempts 屬性值設為 2。

    Get-CsCpsConfiguration | Set-CsCpsConfiguration -MaxCallPickupAttempts 2

## 範例 3

此範例修改 Redmond 1 網站的通話駐留組態，方法是將駐留通話在回撥之前所經過的時間長度 (包含在 CallPickupTimeoutThreshold 屬性中) 設為 45 秒。

    Set-CsCpsConfiguration -Identity site:Redmond1 -CallPickupTimeoutThreshold 00:00:45

## 詳細描述

此 Cmdlet 可用來修改現有的通話駐留服務組態。通話駐留服務組態會指定駐留通話後的動作。例如，如果駐留通話在一段時間內沒有回應，則可自動轉接其他人 (例如系統管理員) 或回應群組。可以設定來電在一段期間後響鈴，以確保不會忘掉來電。此外，可以設定通話駐留服務在駐留通話時，向等待的來電者播放的等候音樂。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsCpsConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCpsConfiguration"}

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
<td><p><em>CallPickupTimeoutThreshold</em></p></td>
<td><p>選用</p></td>
<td><p>TimeSpan</p></td>
<td><p>從駐留通話之後到回撥原先接聽來電的電話之前所經過的時間長度。</p>
<p>這必須使用 hh:mm:ss 的格式輸入 (hh = 小時、mm = 分鐘、ss = 秒)</p>
<p>最小值：10 秒 (00:00:10)；最大值：10 分鐘 (00:10:00)</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMusicOnHold</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>決定駐留通話時是否對來電者播放音樂。</p>
<p>Lync Server 隨附預設的等候音樂檔。您可以使用 <strong>Set-CsCallParkServiceMusicOnHoldFile</strong> Cmdlet 來變更此檔案 (進而變更在駐留通話時來電者所聽到的音樂)。</p></td>
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
<td><p>您要修改之設定的唯一識別碼。Identity 會指定套用設定的範圍，為全域或特定網站 (格式為 site:&lt;網站名稱&gt;，例如 site:Redmond)。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>通話駐留服務設定</p></td>
<td><p>通話駐留服務組態物件的物件參考，類型為 Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings。呼叫 <strong>Get-CsCpsConfiguration</strong> Cmdlet 可以擷取此物件。將該物件以此參數傳遞回 <strong>Set-CsCpsConfiguration</strong> Cmdlet 即可變更物件並儲存變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxCallPickupAttempts</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>在放棄駐留通話並轉接至遞補統一資源識別元 (URI) 之前，回撥接聽電話的次數。遞補 URI 會以 OnTimeoutURI 參數設定。</p>
<p>最小值：1; 最大值：10</p></td>
</tr>
<tr class="even">
<td><p><em>OnTimeoutURI</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>未接聽的駐留通話將轉接的使用者或回應群組的 SIP 位址。在超過 MaxCallPickupAttempts 參數所定義的回撥次數之後，將轉接駐留通話。如果該參數設為 Null，則會忽略 OnTimeoutURI，而駐留的通話會在回電嘗試不成功後中斷。</p>
<p>值必須是以字串 sip: 開頭的 SIP URI。例如，sip:rgs1@litwareinc.com。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings 物件。接受管線傳送的通話保留服務組態物件輸入。

## 傳回類型

修改 Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings 類型的物件。

## 請參閱

#### 其他資源

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

