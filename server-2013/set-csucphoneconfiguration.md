---
title: Set-CsUCPhoneConfiguration
TOCTitle: Set-CsUCPhoneConfiguration
ms:assetid: f77456aa-992a-47d2-bdc7-5e3cbbfb6926
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413042(v=OCS.15)
ms:contentKeyID: 49292850
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUCPhoneConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

可讓您修改 Lync Phone Edition 的管理選項，包括所需的安全性模式，以及電話是否應在指定的閒置時間後自動鎖定等等。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsUCPhoneConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsUCPhoneConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-CalendarPollInterval <TimeSpan>] [-Confirm [<SwitchParameter>]] [-EnforcePhoneLock <$true | $false>] [-Force <SwitchParameter>] [-LoggingLevel <Off | Low | Medium | High>] [-MinPhonePinLength <Byte>] [-PhoneLockTimeout <TimeSpan>] [-SIPSecurityMode <Low | Medium | High>] [-Voice8021p <Byte>] [-VoiceDiffServTag <Byte>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將全域 UC 電話設定的 SIP 安全性模式設定為 Medium。

    Set-CsUCPhoneConfiguration -Identity global -SIPSecurityMode "Medium"

## 範例 2

範例 2 會修改已針對 Redmond 網站設定的 UC 電話設定。在此範例中，PhoneLockTimeout 屬性設為 30 分鐘；作法是加上 PhoneLockTimeout 參數和參數值 "00:30:00" (00 小時：30 分鐘：00 秒)。

    Set-CsUCPhoneConfiguration -Identity site:Redmond -PhoneLockTimeout "00:30:00"

## 範例 3

範例 3 是範例 2 所示命令的變化。但是，這次會針對網站範圍上設定的所有 UC 電話設定來修改 PhoneLockTimeout 屬性。為達成此目的，命令會先呼叫 **Get-CsUCPhoneConfiguration** Cmdlet；Filter 參數搭配篩選值 "site:\*" 可將傳回的資料限制在網站範圍所設定的電話設定。然後再將篩選後的集合管線傳送到 **Set-CsUCPhoneConfiguration** Cmdlet，以使用 PhoneLockTimeout 參數和參數值 "00:30:00" (00 小時 : 30 分鐘 : 00 秒)，將集合中每個項目的電話鎖定逾時值設定為 30 分鐘。

    Get-CsUCPhoneConfiguration -Filter "site:*" | Set-CsUCPhoneConfiguration -PhoneLockTimeout "00:30:00"

## 範例 4

範例 4 會針對 SIP 安全性模式已設定為 Low 或 Medium 的所有 UC 電話設定，來設定 EnforcePhoneLock 和 PhoneLockTimeout 屬性。為達成此目的，此命令會先使用 **Get-CsUCPhoneConfiguration** Cmdlet 傳回組織中的所有 UC 電話組態設定。然後再將該資訊管線傳送到 **Where-Object** Cmdlet，這會只挑出 SIPSecurityMode 屬性不等於 High 的設定 (因為 SIP 安全性可以設為 Low、Medium 或 High，此子句會選取 SIPSecurityMode 設為 Low 或 Medium 的所有設定)。接著將篩選後的集合管線傳送到 **Set-CsUCPhoneConfiguration** Cmdlet，以使用 EnforcePhoneLock 和 PhoneLockTimeout 參數，以修改電話鎖定和電話鎖定逾時屬性。

    Get-CsUCPhoneConfiguration | Where-Object {$_.SIPSecurityMode -ne "High"} | Set-CsUCPhoneConfiguration -EnforcePhoneLock $True -PhoneLockTimeout "00:30:00"

## 範例 5

在範例 5 中，已針對 PhoneLockTimeout 屬性目前少於 10 分鐘的所有 UC 電話設定，將電話鎖定逾時值設定為 10 分鐘 (事實上，這樣會使得整個組織的電話鎖定逾時最小值變成 10 分鐘)。為達成此目的，命令會先使用 **Get-CsUCPhoneConfiguration** Cmdlet 傳回組織目前所使用的所有 UC 電話設定集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出符合下列條件的設定：PhoneLockTimeout 屬性小於 10 分鐘 (00 小時 : 10 分鐘 : 00 秒) 的 A/V Edge 組態設定。接著將篩選後的集合管線傳送到 **Set-CsUCPhoneConfiguration** Cmdlet，以將集合中每個項目的 PhoneLockTimeout 值設定為 10 分鐘。

    Get-CsUCPhoneConfiguration | Where-Object {$_.PhoneLockTimeout -lt "00:10:00"} | Set-CsUCPhoneConfiguration -PhoneLockTimeout "00:10:00"

## 詳細描述

Lync Phone Edition 代表電話與 Lync Server 合併。Lync Phone Edition 會使用功能如同 Voice over Internet Protocol (VoIP) 電話的特殊硬體 (亦即與 Lync 相容的電話)。此外，此硬體也會充當類似 Lync 的端點：您可以設定目前的狀態、檢查 Lync 連絡人的狀態、搜尋新的連絡人，並執行許多其他您過去使用 Lync 執行的作業。

**CsUCPhoneConfiguration** Cmdlet 能讓您使用組態設定，管理執行 Lync Server 的電話。例如，您可以控制登入電話所使用的個人識別碼 (PIN) 長度下限，並可指定在電話未使用一段時間後，是否自動將電話鎖住。

整合通訊 (UC) 電話組態設定可套用於全域範圍或網站範圍。當您首次安裝 Lync Server 時，會在全域範圍建立與套用單一的 UC 電話組態設定集。但在此之後，您便可以隨時使用 **New-CsUCPhoneConfiguration** Cmdlet 建立會在網站範圍套用的設定集合。這可讓您針對每個個別網站獨特的需求，量身設定 UC 電話管理。

除了建立 UC 電話設定的新集合之外，您可以使用 **Set-CsUCPhoneConfiguration** Cmdlet 來修改現有集合的屬性值。例如，根據預設，會針對 UC 電話停用記錄。若要在全域層級上啟用記錄，您可以使用 **Set-CsUCPhoneConfiguration** Cmdlet，將全域集合的 LoggingLevel 屬性值變更為 True。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsUCPhoneConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUCPhoneConfiguration"}

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
<td><p><em>CalendarPollInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指出 UC 裝置每隔多久會從您的 Outlook 行事曆擷取資訊。指定此值時必須使用 hours:minutes:seconds 格式；例如，若要將時間間隔設為 1 小時 (所允許的間隔上限)，請使用這個語法：-CalendarPollInterval &quot;01:00:00&quot;。預設值為 3 分鐘 (00:03:00)。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnforcePhoneLock</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定當經過 PhoneLockTimeout 指定的分鐘數後是否自動鎖住 UC 電話。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>代表要指派給 UC 電話組態設定集合的唯一識別碼。若要參照全域設定，請使用下列語法：-Identity global。若要參考在網站範圍設定的集合，請使用下列語法：-Identity site:Redmond。請注意，指定 Identity 時不能使用萬用字元。</p>
<p>如果省略此參數，則 <strong>Set-CsUCPhoneConfiguration</strong> Cmdlet 將修改全域設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>UcPhoneSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>LoggingLevel</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LoggingLevel</p></td>
<td><p>啟用 UC 裝置上的記錄功能。有效值為 Off、Low、Medium 與 High。預設值為 Off。</p></td>
</tr>
<tr class="even">
<td><p><em>MinPhonePinLength</em></p></td>
<td><p>選用</p></td>
<td><p>System.Byte</p></td>
<td><p>指定個人識別碼 (PIN) 所需的數字數目最小值。</p>
<p>最小值：4</p>
<p>最大值：15</p>
<p>預設值：6</p></td>
</tr>
<tr class="odd">
<td><p><em>PhoneLockTimeout</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指定 UC 電話在閒置多久後 (單位為分鐘) 便會自動鎖住。</p>
<p>這個值必須小於 01:00:00 (1 小時)。預設值為 00:10:00 (10 分鐘)。</p></td>
</tr>
<tr class="even">
<td><p><em>SIPSecurityMode</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.SIPSecurityMode</p></td>
<td><p>指定伺服器套用到由 UC 電話所啟動之 SIP 工作階段的安全層級。</p>
<p>有效值為：</p>
<p>Low (允許任何類型的授權或傳輸)。</p>
<p>Medium (需使用 NTLM 或 Kerberos 進行使用者驗證)。</p>
<p>High (需使用 NTLM 或 Kerberos 進行使用者驗證，並必須使用 TLS 進行 SIP 連線)。</p>
<p>預設值為 High。</p></td>
</tr>
<tr class="odd">
<td><p><em>Voice8021p</em></p></td>
<td><p>選用</p></td>
<td><p>System.Byte</p></td>
<td><p>為 Lync Server 部署內的語音流量指定使用者優先順序值 (802.1p 值)。</p>
<p>只有在使用 802.1p 支援之交換器與橋接器的網路內，此設定才會生效。這個屬性的最小值是 0，最大值是 7，預設值是 0。</p></td>
</tr>
<tr class="even">
<td><p><em>VoiceDiffServTag</em></p></td>
<td><p>選用</p></td>
<td><p>System.Byte</p></td>
<td><p>指定 6 位元差異服務代碼點 (DSCP) 優先順序標記的十進位表示式。此表示式可為由此伺服器管理的 UC 電話所傳遞的 IP 封包定義個別躍點行為 (PHB)。</p>
<p>此值必須介於 0 到 63 (含) 之間。預設值為 40。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.UcPhoneSettings 物件。**Set-CsUCPhoneConfiguration** Cmdlet 會接受 UC 電話設定物件的管線執行個體。

## 傳回類型

**Set-CsUCPhoneConfiguration** Cmdlet 不會傳回值或物件，而是會設定 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.UcPhoneSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsUCPhoneConfiguration](get-csucphoneconfiguration.md)  
[New-CsUCPhoneConfiguration](new-csucphoneconfiguration.md)  
[Remove-CsUCPhoneConfiguration](remove-csucphoneconfiguration.md)

