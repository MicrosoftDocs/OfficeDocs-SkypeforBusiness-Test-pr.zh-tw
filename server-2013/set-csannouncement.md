---
title: Set-CsAnnouncement
TOCTitle: Set-CsAnnouncement
ms:assetid: 286cb990-844e-4b87-bdaf-4a75456d8c60
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425752(v=OCS.15)
ms:contentKeyID: 49290393
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAnnouncement

 

_**上次修改主題的時間：** 2015-03-09_

修改現有 Lync Server 宣告的屬性值。宣告會在使用者撥打有效但未經指派的電話號碼時播放，其可以是訊息 (例如 "This number is temporarily out of service" (此號碼暫時無法提供服務)) 或忙線訊號。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsAnnouncement [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsAnnouncement [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioFilePrompt <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Language <String>] [-Name <String>] [-TargetUri <String>] [-TextToSpeechPrompt <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令指派新音訊檔至服務台宣告。為了執行此工作，命令先使用不含任何參數的 **Get-CsAnnouncement** Cmdlet，以傳回所有目前可用宣告的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以挑出 Name 等於 (-eq) "Help Desk Announcement" 的宣告。接著將該宣告管線傳送到 **Set-CsAnnouncement** Cmdlet，以將 AudioFilePrompt 屬性值設定為 helpdesk.wav。

請注意，如果已指派 TextToSpeechPrompt 值給此宣告，則這個命令會產生將略過 TextToSpeechPrompt 值的警告。

    Get-CsAnnouncement | Where-Object {$_.Name -eq "Help Desk Announcement"} | Set-CsAnnouncement -AudioFilePrompt "helpdesk.wav"

## 範例 2

在範例 2 中，Help Desk Announcement 宣告的 TextToSpeechPrompt 屬性設為 Null 值；實際上這會清除屬性值。為達成此目的，命令會先使用 **Get-CsAnnouncement** Cmdlet 傳回目前可用的所有宣告集合。然後再將該管線傳送到 **Where-Object** Cmdlet，以選取 Name 等於 (-eq) "Help Desk Announcement" 的宣告。接著將該宣告管線傳送到 **Set-CsAnnouncement** Cmdlet，以將 TextToSpeechPrompt 屬性設為 Null 值 ($Null)。

    Get-CsAnnouncement | Where-Object {$_.Name -eq "Help Desk Announcement"} | Set-CsAnnouncement -TextToSpeechPrompt $Null

## 範例 3

此範例會更新宣告名稱為 Help Desk Announcement 的 TargetUri。命令會先使用 **Get-CsAnnouncement** Cmdlet 傳回目前可用的所有宣告集合。然後將此集合以管線傳送到 **Where-Object** Cmdlet，以選取 Name 等於 (-eq) "Help Desk Announcement" 的宣告。接著將此宣告以管線傳送到 **Set-CsAnnouncement** Cmdlet，以將 TargetUri 屬性設定為語音信箱位置 (sip:kmyer@litwareinc.com;opaque=app:voicemail)。

    Get-CsAnnouncement | Where-Object {$_.Name -eq "Help Desk Announcement"} | Set-CsAnnouncement -TargetUri "sip:kmyer@litwareinc.com;opaque=app:voicemail"

## 詳細描述

組織可擁有未指派給使用者或話機的電話號碼，但它仍然是可撥打的有效號碼。根據預設，當某人撥打其中一個電話號碼，該來電者會收到忙線訊號，且來電可能會導致傳回 SIP 用戶端的錯誤。透過將宣告設定套用至未指派的號碼，系統管理員可播放訊息、傳回忙線訊號或將來電重新導向。此 Cmdlet 會修改這些宣告設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsAnnouncement** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAnnouncement"}

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
<td><p><em>AudioFilePrompt</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>宣告將播放之音訊檔的名稱。音訊檔會儲存在 檔案存放區 中。若要將音訊檔儲存到 檔案存放區，請使用 <strong>Import-CsAnnouncementFile</strong> Cmdlet。</p>
<p>有效的檔案類型：WAV 和 WMA</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsIdentity</p></td>
<td><p>宣告的唯一識別碼。這個值的格式始終為 &lt;serviceID&gt;/&lt;GUID&gt;，其中 serviceID 為執行宣告服務的識別，GUID 為與這些宣告設定相關聯的全域唯一識別碼。例如：ApplicationServer:redmond.litwareinc.com/bef5fa3b-3c97-4af0-abe7-611deee7616c.</p>
<p>因為很難在命令列正確輸入 GUID，您較可能使用 <strong>Get-CsAnnouncement</strong> Cmdlet 擷取宣告，然後將它們傳送到 <strong>Set-CsAnnouncement</strong> Cmdlet 進行修改(如需詳細資訊，請參閱〈範例〉區段)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>宣告</p></td>
<td><p>您要變更之 Announcement 物件的參考。這個物件的類型必須是 Microsoft.Rtc.Management.WritableConfig.Settings.AnnouncementServiceSettings.Announcement，可透過呼叫 <strong>Get-CsAnnouncement</strong> Cmdlet 來擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Language</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>播放 TTS 提示將使用的語言。如果已為 TextToSpeechPrompt 輸入值，則需要此參數。</p>
<p>這些值是以字串格式輸入，代表要使用的語言和地區設定。下列為有效值的清單，並在後面加上以括弧括住的語言和地區設定：ca-ES (卡達隆尼亞文，西班牙)；da-DK (丹麥文，丹麥)；de-DE (德文，德國)；en-AU (英文，澳大利亞)；en-CA (英文，加拿大)；en-GB (英文，英國)；en-IN (英文，印度)；en-US (英文，美國)；es-ES (西班牙文，西班牙)；es-MX (西班牙文，墨西哥)；fi-FI (芬蘭文，芬蘭)；fr-CA (法文，加拿大)；fr-FR (法文，法國)；it-IT (義大利文，義大利)；ja-JP (日文，日本)；ko-KR (韓文，韓國)；nb-NO (挪威文，巴克摩，挪威)；nl-NL (荷蘭文，荷蘭)；pl-PL (波蘭文，波蘭)；pt-BR (葡萄牙文，巴西)；pt-PT (葡萄牙文，葡萄牙)；ru-RU (俄文，俄羅斯)；sv-SE (瑞典文，瑞典)；zh-CN (中文，中華人民共和國)；zh-HK (中文，香港特別行政區)；zh-TW (中文，台灣)</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>輸入此參數值以變更宣告的名稱。服務內的名稱必須為唯一。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>宣告播放後會將來電者轉接至的 URI。此值必須是 SIP 位址，輸入格式為 sip:後面再接著 SIP 位址。例如 sip:kmyer@litwareinc.com。請注意，SIP 位址也可以是電話號碼或語音信箱，例如 sip:+14255551212@litwareinc.com;user=phone 表示電話號碼，或 sip:kmyer@litwareinc.com;opaque=app:voicemail 表示語音信箱。</p></td>
</tr>
<tr class="odd">
<td><p><em>TextToSpeechPrompt</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>文字轉換語音 (TTS) 提示。這是一個將轉換為音訊並當做宣告播放的字串。</p>
<p>如果同時針對單一宣告指定了 AudioFilePrompt 和 TextToSpeechPrompt，您會收到一個警告，告知您將優先使用音訊檔，而 TTS 提示將會被忽略。</p>
<p></p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.AnnouncementServiceSettings.Announcement 物件。接受宣告物件的管線傳送資料。

## 傳回類型

**Set-CsAnnouncement** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.AnnouncementServiceSettings.Announcement 物件執行個體。

## 請參閱

#### 其他資源

[New-CsAnnouncement](new-csannouncement.md)  
[Remove-CsAnnouncement](remove-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Import-CsAnnouncementFile](import-csannouncementfile.md)

