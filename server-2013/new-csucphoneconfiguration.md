---
title: New-CsUCPhoneConfiguration
TOCTitle: New-CsUCPhoneConfiguration
ms:assetid: 633a593e-565d-4c04-affb-589502050212
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398445(v=OCS.15)
ms:contentKeyID: 49291120
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsUCPhoneConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立用於管理 Lync Phone Edition 的新設定集合。這些設定可讓您設定所需的安全性模式，以及指定電話是否要在閒置一段時間後自動加以鎖定等等。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsUCPhoneConfiguration -Identity <XdsIdentity> [-CalendarPollInterval <TimeSpan>] [-Confirm [<SwitchParameter>]] [-EnforcePhoneLock <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-LoggingLevel <Off | Low | Medium | High>] [-MinPhonePinLength <Byte>] [-PhoneLockTimeout <TimeSpan>] [-SIPSecurityMode <Low | Medium | High>] [-Voice8021p <Byte>] [-VoiceDiffServTag <Byte>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會為 Redmond 網站建立新的 UC 電話設定集合。在此範例中，包含了兩個選用參數及一個必要參數 Identity：一個是 CalendarPollInterval，此參數會將行事曆輪詢時間設為每隔 10 分鐘 (00 小時：10 分鐘：00 秒)；另一個是 LoggingLevel，此參數會將 UC 電話記錄層次設為 Medium。只要此命令一完成，新的設定便會套用到 Redmond 網站，且該網站的使用者會讓新的設定管理其 UC 電話。請注意，如果 Redmond 網站已有 UC 電話設定的集合，則此命令會失敗。

    New-CsUCPhoneConfiguration -Identity site:Redmond -CalendarPollInterval "00:10:00" -LoggingLevel "Medium"

## 範例 2

範例 2 示範 InMemory 參數的使用方式，此參數可讓您建立僅存在於記憶體中的新 UC 電話設定集(這些設定儲存在 $x 變數中)。在建立此虛擬集合後，您可以使用類似範例中第二行與第三行的命令來修改僅於記憶體中的設定：在第二行中，CalendarPollInterval 屬性設為 10 分鐘 (00 hours:10 minutes:00 seconds)，而在第三行中，LoggingLevel 屬性會設為 Medium。

在您將屬性值修改完成後，便可以使用 **Set-CsUCPhoneConfiguration** Cmdlet，將儲存在 $x 中的虛擬設定轉變為實際套用到 Redmond 網站的設定集合。請注意，因為使用了 InMemory 參數，所以您必須呼叫 **Set-CsUCPhoneConfiguration** Cmdlet 才會實際套用設定。如果您未呼叫此 Cmdlet，當終止 Windows PowerShell 工作階段或刪除變數 $x 時，您的虛擬設定便會消失。

    $x = New-CsUCPhoneConfiguration -Identity site:Redmond -InMemory
    $x.CalendarPollInterval = "00:10:00" 
    $x.LoggingLevel = "Medium"
    Set-CsUCPhoneConfiguration -Instance $x

## 詳細描述

Lync Phone Edition 代表電話與 Lync Server 合併。Lync Phone Edition 會使用功能如同 Voice over Internet Protocol (VoIP) 電話的特殊硬體 (亦即與 Lync Phone Edition 相容的電話)。此外，此硬體也會充當類似 Lync 的端點：您可以設定目前的狀態、檢查 Lync 連絡人的狀態、搜尋新的連絡人，並執行許多其他過去使用 Lync 執行的作業。

Lync Server 隨附許多 Cmdlet 可供您管理執行 Lync Phone Edition 的電話；例如，您可以控制登入電話所使用的個人識別碼 (PIN) 長度下限，以及電話在未使用一段時間後是否會自動自行鎖住。

整合通訊 (UC) 電話組態設定可在全域範圍或網站範圍套用 (在網站範圍套用的設定優先於在全域範圍套用的設定)。當您首次安裝 Lync Server 時，會在全域範圍建立與套用單一的 UC 電話組態設定集。但在此之後，您可以隨時使用 **New-CsUCPhoneConfiguration** Cmdlet 建立會在網站範圍套用的設定集合。這可讓您針對每個個別網站獨特的需求，量身設定 UC 電話管理。

**New-CsUCPhoneConfiguration** Cmdlet 可讓您在網站範圍建立新的 UC 電話設定。請注意，每個網站只能有一個設定集合。例如，如果您嘗試建立 Identity 為 site:Redmond 的設定集合，但是已經有一組 UC 電話設定指派給 Redmond 網站。在這種情況下，您的命令會失敗。您必須採取以下兩個步驟之一：移除現有設定，然後使用 **New-CsUCPhoneConfiguration** Cmdlet 建立新的設定集合；或者單單使用 **Set-CsUCPhoneConfiguration** Cmdlet 修改現有的設定。

您無法在全域範圍建立新的設定集合。您在全域範圍唯一能做的動作就是使用 **Set-CsUCPhoneConfiguration** Cmdlet 修改現有的設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsUCPhoneConfiguration** Cmdlet：RTCUniversalServerAdmins。執行 Windows PowerShell 提示字元提供的下列命令，即可傳回指派給此 Cmdlet (包括您自行建立的任何自訂 RBAC 角色) 的所有角色型存取控制 (RBAC) 角色清單：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsUCPhoneConfiguration"}

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
<td><p>代表指派給新 UC 電話組態設定集合的唯一識別碼。由於您只能在網站範圍建立新集合，因此，Identity 一律是首碼 &quot;site:&quot; 加上網站名稱，例如 &quot;site:Redmond&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>CalendarPollInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指出 UC 裝置每隔多久會從您的 Outlook 行事曆擷取資訊。指定此值時必須使用 hours:minutes:seconds 格式；例如，若要將時間間隔設為 1 小時 (所允許的間隔上限)，請使用這個語法：-CalendarPollInterval &quot;01:00:00&quot;。預設值為 3 分鐘 (00:03:00)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>EnforcePhoneLock</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定當經過 PhoneLockTimeout 指定的分鐘數後是否自動鎖住 UC 電話。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>LoggingLevel</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LoggingLevel</p></td>
<td><p>啟用 UC 裝置上的記錄功能。有效值為 Off、Low、Medium 與 High。預設值為 Off。</p>
<p></p></td>
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
<td><p>說明執行命令時若不實際執行命令的後果。</p>
<p></p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsUCPhoneConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.UcPhoneSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsUCPhoneConfiguration](get-csucphoneconfiguration.md)  
[Remove-CsUCPhoneConfiguration](remove-csucphoneconfiguration.md)  
[Set-CsUCPhoneConfiguration](set-csucphoneconfiguration.md)

