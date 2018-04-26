---
title: Set-CsLocationPolicy
TOCTitle: Set-CsLocationPolicy
ms:assetid: efa2840c-2e21-408e-b9fe-6f9998c81db2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412987(v=OCS.15)
ms:contentKeyID: 49292741
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLocationPolicy

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的位置原則。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsLocationPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsLocationPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ConferenceMode <oneway | twoway>] [-ConferenceUri <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EmergencyDialMask <String>] [-EmergencyDialString <String>] [-EnhancedEmergencyServiceDisclaimer <String>] [-EnhancedEmergencyServicesEnabled <$true | $false>] [-Force <SwitchParameter>] [-LocationRefreshInterval <Int64>] [-LocationRequired <yes | no | disclaimer>] [-NotificationUri <String>] [-PstnUsage <String>] [-UseLocationForE911Only <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此命令會使用 **Set-CsLocationPolicy** Cmdlet 修改 Identity 為 site:Redmond 的位置原則。(換句話說，它會修改已套用至 Redmond 網站的位置原則)。在此案例中，命令會將 EnhancedEmergencyServicesEnabled 屬性值設定為 True，這將針對所有已連線至 (在此案例中) Redmond 網站的使用者啟用 E9-1-1 功能。

    Set-CsLocationPolicy -Identity site:Redmond -EnhancedEmergencyServicesEnabled $True

## 範例 2

範例 2 會修改用於組織中已定義會議 URI 的所有位置原則，以具備雙向會議模式。為了執行此工作，命令會先使用 **Get-CsLocationPolicy** Cmdlet 來傳回目前定義之所有位置原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以將集合範圍限縮為 ConferenceUri 屬性不是空白 (不等於 Null) 的位置原則。如此將會產生內含 ConferenceUri 值的位置原則集合。接著將該集合管線傳送到 **Set-CsLocationPolicy** Cmdlet，以藉由將值設定為雙向來修改集合中每個原則的 ConferenceMode 屬性值。

    Get-CsLocationPolicy | Where-Object {$_.ConferenceUri -ne $null} | Set-CsLocationPolicy -ConferenceMode twoway

## 詳細描述

位置原則可用來套用與增強型 9-1-1 (E9-1-1) 功能和用戶端位置相關的設定。位置原則會判斷使用者是否已啟用 E9-1-1，如果是，則會決定緊急電話的行為。例如，您可以使用位置原則來定義組成緊急電話的數字 (在美國為 911)、是否應自動告知公司的安全部門，以及應如何路由傳送來電。此 Cmdlet 會修改現有的位置原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsLocationPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLocationPolicy"}

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
<td><p><em>ConferenceMode</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Location.ConferenceModeEnum</p></td>
<td><p>如果已指定 ConferenceUri 參數的值，則 ConferenceMode 參數會決定第三方是否可參與該電話，或只能聆聽。可用的值有：</p>
<p>- oneway：第三方只能聆聽來電者與公眾安全回應點 (PSAP) 接線生之間的對話。</p>
<p>- twoway：第三方可聆聽並參與來電者與 PSAP 接線生之間的通話。</p></td>
</tr>
<tr class="even">
<td><p><em>ConferenceUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>第三方的 SIP 統一資源識別元 (URI) (本案例中為電話號碼)，第三方將會加入任何所撥打緊急電話的電話會議中。例如，當有人撥打緊急電話時，公司的安全部門會接聽該電話，並聆聽電話內容或參與該電話 (取決於 ConferenceMode 屬性的值)。</p>
<p>字串長度必須為 1 到 256 字元，且開頭必須為首碼 sip:。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>此位置的詳細說明。例如，&quot;Building 30, 3rd Floor, NorthEast corner&quot; 。</p></td>
</tr>
<tr class="odd">
<td><p><em>EmergencyDialMask</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>撥打的號碼會轉譯成 EmergencyDialString 屬性的值。例如，若 EmergencyDialMask 的值為 &quot;212&quot;，而 EmergencyDialString 的值為 &quot;119&quot;，若使用者撥打 212，通話會轉接至 119。此作法一方面可以改撥替代的緊急電話號碼，一方面電話仍可轉接到緊急服務 (例如，若某個國家/地區的緊急電話號碼不同，來自該國家/地區的人會嘗試撥打該國家/地區的緊急電話號碼，而非所在國家/地區的緊急電話號碼)。您可以使用分號分隔多個值，藉此定義多組緊急撥話遮罩。例如，-EmergencyDialMask &quot;212;414&quot; 。</p>
<p>重要。確保指定的撥號遮罩值與通話保留範圍中的數字不同。通話保留路由優先於緊急撥號字串轉換。呼叫 <strong>Get-CsCallParkOrbit</strong> Cmdlet 可以查看現有的通話保留範圍。</p>
<p>字串的長度上限為 100 字元。每個字元必須是 0 到 9 的數字。</p></td>
</tr>
<tr class="even">
<td><p><em>EmergencyDialString</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>聯絡緊急服務時所撥打的號碼。此值在美國為 &quot;911&quot;。</p>
<p>字串必須由 0 到 9 的數字組成，長度可為 1 到 10 個字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnhancedEmergencyServiceDisclaimer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>當位置對應 (線路圖) 無法解析使用者的連線來源位置，而使用者選擇不手動輸入其位置時，就會對該使用者顯示包含資訊的文字值。若要從位置原則中移除服務免責聲明，請將此屬性設為 Null 值：</p>
<p>-EnhancedEmergencyServiceDisclaimer $Null</p>
<p>Lync Server 2013應使用位置原則搭配 EnhancedEmergencyServiceDisclaimer 屬性，來設定 E9-1-1 服務的免責聲明。這與 Lync Server 2010 不同，在此版本中，會使用 Set-CsEnhancedEmergencyServiceDisclaimer Cmdlet 來設定整個組織的全域免責聲明。藉由使用位置原則來設定三個免責聲明，您可以建立不同地區設定或不同使用者群組的不同免責聲明。</p></td>
</tr>
<tr class="even">
<td><p><em>EnhancedEmergencyServicesEnabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定與此原則關聯的使用者是否已啟用 E9-1-1 功能。將值設為 True 可啟用 E9-1-1，所以 Lync Server 用戶端會在登錄時擷取位置資訊，並在撥打緊急電話時包含該資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要修改之位置原則的唯一識別碼。若要修改全域位置原則，請使用 Global 值。對於在網站範圍內建立的原則，這個值的格式將為 site:&lt;網站名稱&gt;。其中網站名稱是指在 Lync Server 部署中定義之網站的名稱 (例如 site:Redmond)。對於已在個別使用者範圍內建立的原則，此值將只是原則的名稱，例如 Reno。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>LocationPolicy</p></td>
<td><p>位置原則物件的參照。此物件的類型必須是 Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy，呼叫 <strong>Get-CsLocationPolicy</strong> Cmdlet 即可擷取此物件。擷取此物件、變更記憶體中的屬性，然後將物件參照當成值傳給此參數，以更新該位置原則。</p></td>
</tr>
<tr class="even">
<td><p><em>LocationRefreshInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int64</p></td>
<td><p>指定位置資訊服務位置更新之用戶端要求的時間間隔 (小時)。LocationRefreshInterval 可以設為任何介於 1 與 12 之間的值；預設值為 4。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocationRequired</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationRequiredEnum</p></td>
<td><p>如果用戶端無法從位置組態資料庫擷取位置，則會提示使用者手動輸入位置。此參數接受下列值：</p>
<p>- no：將不會提示使用者輸入位置。當撥打的電話沒有位置資訊時，緊急服務供應商將接聽來電，並要求提供位置。</p>
<p>- yes：當用戶端在新位置登錄時，會提示使用者輸入位置資訊。使用者可以不輸入任何資訊而將提示關閉。如有輸入資訊，撥打到 119 的電話會先由緊急服務供應商接聽以確認位置，然後再路由傳送到 PSAP ( 即 119 接線生)。</p>
<p>- disclaimer：此選項與 yes 相同，但是當使用者關閉提示時，則會顯示免責聲明文字，警告使用者拒絕輸入位置資訊的後果 (免責聲明文字必須透過呼叫 <strong>Set-CsEnhancedEmergencyServiceDisclaimer</strong> Cmdlet 設定)。</p>
<p>如果 EnhancedEmergencyServicesEnabled 設為 False (預設值)，則會忽略此值。系統將不會提示使用者輸入位置資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>NotificationUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>撥打緊急電話時所通知的一或多個 SIP 統一資源識別元 (URI)。例如，每次有人撥打緊急電話時，就會透過立即訊息通知公司的安全部門。如果可以使用來電者的位置，通知中會包含該位置的資訊。</p>
<p>可以使用逗號分隔的清單包含多個 SIP URI。例如，-NotificationUri sip:security@litwareinc.com,sip:kmyer@litwareinc.com。請注意，在 Lync Server 2013版本中，現在可以將通訊群組清單設定為通知 URI。</p>
<p>字串長度必須為 1 到 256 字元，且開頭必須為首碼 sip:。</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnUsage</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>公用交換電話網路 (PSTN) 使用方式，可指定要用於路由使用此設定檔之用戶端的 119 電話的語音路由。此使用方式的相關聯路由應指向緊急電話專用的 SIP 主幹。</p>
<p>使用方式必須已存在於 PSTN 使用方式的全域清單中。呼叫 <strong>Get-CsPstnUsage</strong> Cmdlet 可擷取使用方式清單。呼叫 <strong>Set-CsPstnUsage</strong> Cmdlet 可建立新的使用方式。</p></td>
</tr>
<tr class="even">
<td><p><em>UseLocationForE911Only</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>Lync Server 用戶端使用位置資訊的原因有許多種 (例如通知組員目前的位置)。將此值設為 True 可確保位置資訊僅供搭配緊急電話使用。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy 物件。接受管線傳送的位置原則物件輸入。

## 傳回類型

這個 Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Grant-CsLocationPolicy](grant-cslocationpolicy.md)  
[Test-CsLocationPolicy](test-cslocationpolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

