---
title: New-CsAnnouncement
TOCTitle: New-CsAnnouncement
ms:assetid: 6e3699c6-cd2b-4842-99bc-3cf2578fbd65
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398522(v=OCS.15)
ms:contentKeyID: 49291264
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAnnouncement

 

_**上次修改主題的時間：** 2015-03-09_

建立新的 Lync Server 宣告。宣告會在使用者撥打有效但未經指派的電話號碼時播放，其可以是訊息 (例如 "This number is temporarily out of service" (此號碼暫時無法提供服務)) 或忙線訊號。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsAnnouncement -Parent <String> <COMMON PARAMETERS>

    New-CsAnnouncement -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Name <String> [-AudioFilePrompt <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Language <String>] [-TargetUri <String>] [-TextToSpeechPrompt <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 示範如何建立以英文 (美國) 播放 TTS 提示的新宣告。指定的第一個參數是 Identity。Identity 必須位於服務範圍，後面緊接著應用程式伺服器的服務識別碼 (ApplicationServer:redmond.litwareinc.com)。接下來為宣告命名，在此範例中為 Help Desk Announcement。若要為此宣告指派一個 TTS 提示，我們使用 TextToSpeechPrompt 參數，後面緊接著一個包含宣告文字的字串。在宣告中使用 TTS 提示時，您必須指定一個語言，作法為，加入 Language 參數，後面緊接著代表美國英文 (en-US) 的字串。

請注意，宣告識別是由兩個部分組成：要儲存該宣告的服務，以及一個 36 個字元的 GUID (全域唯一識別碼)。您會在建立新宣告後看到完整的 Identity，系統會自動產生並套用 GUID。該 Identity 會類似如下：service:ApplicationServer:redmond.litwareinc.com/1951f734-c80f-4fb2-965d-51807c792b90。

    New-CsAnnouncement -Identity ApplicationServer:redmond.litwareinc.com -Name "Help Desk Announcement" -TextToSpeechPrompt "Welcome to the Help Desk." -Language "en-US"

## 範例 2

範例 2 與範例 1 類似的地方是從輸入必要的參數 Identity 和 Name 開始。不過，在此範例中，我們想要讓宣告播放音訊檔而不是 TTS 提示。為達此目的，我們會加入 AudioFilePrompt 參數，並將一個包含音訊檔名稱 (WelcomeMessage.wav) 的字串傳遞給該參數。此檔案必須位於 檔案存放區 內，才能讓此宣告播放。您可以呼叫 **Import-CsAnnouncementFile**，將音訊檔新增至 檔案存放區。

    New-CsAnnouncement -Identity ApplicationServer:redmond.litwareinc.com -Name "Welcome Announcement" -AudioFilePrompt "WelcomeMessage.wav"

## 範例 3

與範例 2 相同，此範例會建立在達到此數目時播放音訊檔的宣告。不過，在此範例中，除了 Identity、Name 以及 AudioFilePrompt 參數之外，我們還另外指定了 TargetUri 參數。我們會將此參數 (使用者或電話的 SIP URI) 傳遞給將在播放宣告後轉接至的來電者。

    New-CsAnnouncement -Identity ApplicationServer:redmond.litwareinc.com -Name "Forward Announcement" -AudioFilePrompt "WelcomeMessage.wav" -TargetUri sip:kmyer@litwareinc.com

## 範例 4

範例 4 與範例 3 相同，但不是根據使用者的 SIP 位址轉接來電，而是將來電轉接至電話號碼。

    New-CsAnnouncement -Identity ApplicationServer:redmond.litwareinc.com -Name "Forward Announcement" -AudioFilePrompt "WelcomeMessage.wav" -TargetUri "sip:+14255551212@litwareinc.com;user=phone"

## 範例 5

在此範例中，我們沒有指定提示或目標 URI，而只加入了一個 Identity 和一個 Name。也就是說，當來電者撥打至與此宣告相關聯的未指派號碼接通時，來電者將會聽到忙線訊號。

    New-CsAnnouncement -Identity ApplicationServer:redmond.litwareinc.com -Name "Busy"

## 詳細描述

組織可擁有未指派給使用者或話機的電話號碼，但它仍然是可撥打的有效號碼。根據預設，當某人撥打其中一個電話號碼，該來電者會收到忙線訊號，且來電可能會導致傳回 SIP 用戶端的錯誤。透過將宣告設定套用至未指派的號碼，系統管理員就可以選擇播放訊息、傳回忙線訊號或是將電話重新導向。此 Cmdlet 會建立這些宣告設定。

您可以呼叫 **New-CsUnassignedNumber** 或 **Set-CsUnassignedNumber** Cmdlet，將宣告指派給未指派的號碼。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsAnnouncement** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsAnnouncement"}

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
<td><p>宣告的唯一識別碼。您必須針對這個值輸入執行回應群組應用程式之應用程式伺服器的 Identity。例如 ApplicationServer:redmond.litwareinc.com。</p>
<p>您可以將一個以上的宣告指派給單一服務。因此，為了讓 Identity 成為唯一值，在您建立宣告時，將會自動產生一個全域唯一識別碼 (GUID) 並指派給該 Identity。新宣告的 Identity 格式為 service:&lt;service ID&gt;/&lt;GUID&gt;。例如：service:ApplicationServer:redmond.litwareinc.com/bef5fa3b-3c97-4af0-abe7-611deee7616c。當您呼叫此 Cmdlet 時，不需要提供 GUID。而是必須提供服務 Identity，系統會自動產生 GUID 並將它新增至 Identity。</p>
<p>雖然您不需要提供 GUID，但也可以提供。您可能想要在宣告已指派給未指派的號碼範圍，因而宣告遭到刪除時這麼做。您可以使用相符的 Identity (包括 GUID) 建立新宣告，在這種情況下，不需要更新未指派的號碼範圍。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>宣告的描述性名稱。這個名稱在服務中必須是唯一的。此名稱將在呼叫 <strong>New-CsUnassignedNumber</strong> Cmdlet 或 <strong>Set-CsUnassignedNumber</strong> Cmdlet 時使用，以指定與未指派之號碼範圍相關聯的宣告。</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>此參數與 Identity 相同，但 Identity 會接受服務 Identity 與 GUID，而 Parent 只會接受自動產生的服務 Identity 與 GUID。您無法指定 Identity 及 Parent。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioFilePrompt</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>宣告將播放之音訊檔的名稱。音訊檔會儲存在 檔案存放區 中。若要將音訊檔儲存到 檔案存放區，請使用 <strong>Import-CsAnnouncementFile</strong> Cmdlet。</p>
<p>有效的檔案類型：WAV 和 WMA</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>Language</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>播放文字轉換語音 (TTS) 提示將使用的語言。如果已為 TextToSpeechPrompt 輸入值，則需要此參數。</p>
<p>這些值是以字串格式輸入，代表要使用的語言和地區設定。下列為有效值的清單，並在後面加上以括弧括住的語言和地區設定：ca-ES (卡達隆尼亞文，西班牙)；da-DK (丹麥文，丹麥)；de-DE (德文，德國)；en-AU (英文，澳大利亞)；en-CA (英文，加拿大)；en-GB (英文，英國)；en-IN (英文，印度)；en-US (英文，美國)；es-ES (西班牙文，西班牙)；es-MX (西班牙文，墨西哥)；fi-FI (芬蘭文，芬蘭)；fr-CA (法文，加拿大)；fr-FR (法文，法國)；it-IT (義大利文，義大利)；ja-JP (日文，日本)；ko-KR (韓文，韓國)；nb-NO (挪威文，巴克摩，挪威)；nl-NL (荷蘭文，荷蘭)；pl-PL (波蘭文，波蘭)；pt-BR (葡萄牙文，巴西)；pt-PT (葡萄牙文，葡萄牙)；ru-RU (俄文，俄羅斯)；sv-SE (瑞典文，瑞典)；zh-CN (中文，中華人民共和國)；zh-HK (中文，香港特別行政區)；zh-TW (中文，台灣)</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>宣告播放後，會將來電者轉接至的統一資源識別元 (URI)。此值必須是 SIP 位址，輸入格式為 sip:後面再接著 SIP 位址。例如 sip:kmyer@litwareinc.com。請注意，SIP 位址也可以是電話號碼或語音信箱，例如 sip:+14255551212@litwareinc.com;user=phone 表示電話號碼，或 sip:kmyer@litwareinc.com;opaque=app:voicemail 表示語音信箱。</p></td>
</tr>
<tr class="even">
<td><p><em>TextToSpeechPrompt</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>文字轉換語音 (TTS) 提示。這是一個將轉換為音訊並當做宣告播放的字串。</p>
<p>如果同時針對單一宣告指定了 AudioFilePrompt 和 TextToSpeechPrompt，您會收到一個警告，告知您將優先使用音訊檔，而 TTS 提示將會被忽略。</p>
<p></p></td>
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

建立 Microsoft.Rtc.Management.WritableConfig.Settings.AnnouncementServiceSettings.Announcement 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsAnnouncement](remove-csannouncement.md)  
[Set-CsAnnouncement](set-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Import-CsAnnouncementFile](import-csannouncementfile.md)  
[New-CsUnassignedNumber](new-csunassignednumber.md)  
[Set-CsUnassignedNumber](set-csunassignednumber.md)

