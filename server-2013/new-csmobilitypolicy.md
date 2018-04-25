---
title: New-CsMobilityPolicy
TOCTitle: New-CsMobilityPolicy
ms:assetid: 1fba8c3e-087d-4ba4-918b-371f8757df7c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh689987(v=OCS.15)
ms:contentKeyID: 49290300
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsMobilityPolicy

 

_**上次修改主題的時間：** 2015-03-09_

在網站範圍或個別使用者範圍建立新的行動原則。行動原則可判斷使用者能否使用 Lync Mobile。除此之外，也能管理使用者是否可以使用 \[從公司撥號\]，在其行動電話上使用公司電話號碼，而不使用自己的行動電話號碼撥打及接聽電話。行動原則也可以在撥號或接聽來電時用來要求 Wi-Fi 連線。 Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    New-CsMobilityPolicy -Identity <XdsIdentity> [-AllowCustomerExperienceImprovementProgram <$true | $false>] [-AllowExchangeConnectivity <$true | $false>] [-AllowSaveCallLogs <$true | $false>] [-AllowSaveCredentials <$true | $false>] [-AllowSaveIMHistory <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableIPAudioVideo <$true | $false>] [-EnableMobility <$true | $false>] [-EnableOutsideVoice <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-RequireWIFIForIPAudio <$true | $false>] [-RequireWIFIForIPVideo <$true | $false>] [-RequireWiFiForSharing <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會為 Redmond 網站建立新的行動原則，並針對受該原則影響的任何使用者停用從公司撥號。作法是將 EnableOutsideVoice 參數值設為 False。

    New-CsMobilityPolicy -Identity site:Redmond -EnableOutsideVoice $False

## 範例 2

範例 2 會示範如何在記憶體中建立新的行動原則、修改該原則的屬性值，然後使用 **Set-CsMobilityPolicy** Cmdlet 將虛擬原則轉變為實際 Lync Server 行動原則。為達成此目的，命令會先使用 **New-CsMobilityPolicy** Cmdlet 和 InMemory 參數為 Redmond 網站建立新的原則。因為 InMemory 參數會讓此原則僅存在於記憶體中，因此產生的物件必須以變數 ($x) 儲存。

在命令 2 中，虛擬原則的 EnableOutsideVoice 屬性設為 False。之後，命令 3 會使用 **Set-CsMobilityPolicy** Cmdlet 和 Instance 參數將變更寫入 Lync Server，並為 Redmond 網站建立新的行動原則。若您沒有呼叫 **Set-CsMobilityPolicy** Cmdlet，就不會建立原則，而且一旦終止 Windows PowerShell 命令列介面工作階段或刪除變數 $x，原則就會消失。

    $x = New-CsMobilityPolicy -Identity site:Redmond -InMemory
    $x.EnableOutsideVoice = $False
    Set-CsMobilityPolicy -Instance $x

## 詳細描述

Lync Mobile 是可讓使用者在行動電話上執行 Lync 的用戶端應用程式。\[從公司撥號\] 可讓使用者在行動電話上撥打電話，但是將此通話顯示為從公司電話號碼 (而不是行動電話號碼) 撥出的通話。啟用 \[從公司撥號\] 的使用者可以直接從其行動電話撥號，或透過 \[電話撥出式會議\] 選項來達成此目的。透過電話撥出式會議，使用者實際上是要求 Lync Server Mobility Service 伺服器代為撥打電話。伺服器會建立通話，然後回撥給使用者的行動電話。在使用者接聽之後，伺服器會接著撥打給受話方。您可以使用行動原則來管理這兩個功能。

透過 Lync Server 2013，行動裝置可以使用標準行動電話網路或 Wi-Fi 連線來撥打或接聽電話。行動原則可用於要求 Wi-Fi 連線，以避免透過行動電話網路進行通話。

當您安裝 Lync Server 時，即會有套用到所有使用者的單一全域行動性原則。但是，系統管理員可以使用 **New-CsMobilityPolicy** Cmdlet，在網站範圍或個別使用者範圍建立自訂原則。

請注意，要使 \[從公司撥號\] 能夠運作，必須設定兩個不同的屬性。第一個是 EnableOutsideVoice，可決定是否啟用 \[從公司撥號\]；第二個是 EnableMobility，可決定是否允許使用者使用 Lync Mobile。這兩個屬性都必須設為 True，使用者才能利用 \[從公司撥號\]。如果 EnableMobility 設為 True 而 EnableOutsideVoice 設為 False，則使用者可以執行 Lync Mobile 但將無法使用「從公司撥號」。如果 EnableMobility 設為 False 而 EnableOutsideVoice 設為 True，使用者就無法執行 Lync Mobile。這表示接下來不論 EnableOutsideVoice 屬性的值為何，使用者都將無法使用 \[從公司撥號\]。

若要使用從公司撥號，使用者還必須受到允許同時響鈴之語音原則的管理。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsMobilityPolicy** Cmdlet：RTCUniversalServerAdmins。

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
<td><p>指派給原則的唯一 Identity。新的行動原則可以在網站或個別使用者範圍建立。若要建立新的網站原則，請使用首碼 &quot;site:&quot; 以及網站名稱做為您的 Identity。例如，這個語法會為 Redmond 網站建立新的原則：</p>
<p>-Identity site:Redmond</p>
<p>若要建立新的個別使用者原則，請使用類似下列的 Identity：</p>
<p>-Identity SalesDepartmentPolicy</p>
<p>請注意，您無法建立新的全域原則；如果您要對全域原則進行變更，請改用 <strong>Set-CsMobilityPolicy</strong> Cmdlet。同樣地，如果使用該 Identity 的原則已存在，您便無法建立新的網站原則或個別使用者原則。如果您需要變更現有的原則，請使用 <strong>Set-CsMobilityPolicy</strong> Cmdlet。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowCustomerExperienceImprovementProgram</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，行動使用者將可參與 Microsoft 客戶經驗改進計畫。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowExchangeConnectivity</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，使用者將可使用其行動裝置連線至 Microsoft Exchange Server 2013。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowSaveCallLogs</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，使用者將可儲存由其行動裝置所建立或接收之電話的通話記錄。</p>
<p>請注意此設定不適用於 Android 裝置。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowSaveCredentials</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，使用者可將認證資訊 (例如密碼) 儲存於其行動裝置。此資訊則可套用至自動登入的情境。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowSaveIMHistory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，使用者將可在其行動裝置上儲存 IM 與會議工作階段的文字記錄。</p></td>
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
<td><p>System.String</p></td>
<td><p>讓系統管理員能夠提供原則隨附的說明文字。例如，Description 可包含被指派原則的使用者相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableIPAudioVideo</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 False，使用者將無法用行動裝置撥打 VoIP 通話。預設值為 True，表示可以撥打 VoIP 通話。</p>
<p>Lync Server 2013中已導入此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMobility</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，使用者就可以使用 Lync Mobile。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableOutsideVoice</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，使用者即可使用從公司撥號。設為 False 時，使用者就無法使用從公司撥號。</p>
<p>預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照，但而不實際將物件認可為永久變更。如果您會將這個利用此參數呼叫之命令的輸出指派給變數，則可變更物件參照的屬性，然後呼叫此 Cmdlet 相符的 Set- Cmdlet 來認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>RequireWIFIForIPAudio</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 True，使用者可以在行動裝置連線到 Wi-Fi 網路時，在通話中使用 IP 音訊。這表示使用者僅可使用 Wi-Fi 撥打音訊通話，而無法使用標準的行動電話網路。預設值為 False。</p>
<p>Lync Server 2013中已導入此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>RequireWIFIForIPVideo</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 True，使用者在行動裝置連線到 Wi-Fi 網路時，僅可在通話中使用 IP 視訊。若是行動裝置不在 Wi-Fi 範圍內，則視訊通話將僅會以音訊通話接收。若是此屬性設為 False (預設值)，則使用者可在使用 Wi-Fi 或行動數據連線時撥打或接收 IP 視訊通話。</p>
<p>Lync Server 2013中已導入此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>RequireWiFiForSharing</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，行動使用者必須使用 WiFi 連線才能參與應用程式共用工作階段。設為 False (預設值) 時，行動使用者可使用 WiFi 連線或行動數據 (3G/4G) 連線參與應用程式共用。</p>
<p>若將此值設定為 True，使用者將無法變更其共用組態設定。若將此值設定為 False，使用者可以使用 [選項] 頁面修改其共用組態設定。</p></td>
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

無。 **New-CsMobilityPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WriteableConfig.Policy.Mobility.Mobility 物件的新執行個體。

