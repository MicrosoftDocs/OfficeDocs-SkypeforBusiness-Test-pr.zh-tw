---
title: New-CsMcxConfiguration
TOCTitle: New-CsMcxConfiguration
ms:assetid: 9eebea4a-64a3-424c-9b05-0579c4e8111e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690035(v=OCS.15)
ms:contentKeyID: 49291823
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsMcxConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

在網站範圍或服務範圍建立新的 Lync Server 2013 Mobility Service 組態設定集合。Mobility Service 可讓行動電話使用者 (例如 iPhone 和 Windows Phone) 交換立即訊息與目前狀態資訊；從內部儲存及擷取語音信箱，而不使用無線提供者；以及利用 \[從公司撥號\] 和 \[電話撥出式會議\] 等 Lync Server 功能。 Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    New-CsMcxConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-ExposedWebURL <External | Internal>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-PushNotificationProxyUri <String>] [-SessionExpirationInterval <UInt32>] [-SessionShortExpirationInterval <UInt32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會為 Redmond 網站建立新的 Mobility Service 組態設定集合 (並將集合自動指派給該網站)。此範例會對預設的 Mobility Service 組態設定進行兩項變更：將 ExposedWebURL 屬性設為 Internal，以及將 SessionShortExpirationInterval 屬性設為 7200 秒。

    New-CsMcxConfiguration -Identity "site:Redmond" -ExposedWebURL Internal -SessionShortExpirationInterval 7200

## 範例 2

範例 2 會為組織目前所使用之每部網頁伺服器建立一組相同的 Mobility Service 組態設定。為了執行此工作，會使用 **Get-CsService** Cmdlet 並搭配 WebServer 參數，傳回所有現有網頁伺服器的集合；然後再將該集合管線傳送給 **For-Each** Cmdlet。 **ForEach-Object** Cmdlet 會針對集合中每部伺服器依序執行 **New-CsMcxConfiguration** Cmdlet，以在該伺服器上建立新的 Mobility Service 組態設定。

    Get-CsService -WebServer | ForEach-Object {New-CsMcxConfiguration -Identity $_.Identity -ExposedWebURL Internal -SessionShortExpirationInterval 7200}

## 範例 3

範例 3 示範 InMemory 參數如何讓您在記憶體中建立新的 Mobility Service 組態設定集合、修改該集合的屬性值，然後再將集合儲存至 Lync Server。為達此目的，集合中的第一個命令會建立 Identity 為 site:Redmond 的新 Mobility Service 組態設定集合。但是，這些設定只會在記憶體中建立 (由於 InMemory 參數)，再以名稱為 $x 的變數儲存，而不會自動建立並指派給 Redmond 網站。

範例中的命令 2 和 3 顯示如何修改此虛擬 Mobility Service 組態集合的屬性值。在您完成修改屬性值後，便可以使用 **Set-CsMcxConfiguration** Cmdlet 和 Instance 參數，將虛擬設定轉變為指派給 Redmond 網站的實際 Mobility Service 組態設定集合。請注意，如果您沒有呼叫 **Set-CsMcxConfiguration** Cmdlet，則不會將任何設定指派給 Redmond 網站，而且只要您結束 Windows PowerShell 工作階段或刪除變數 $x，虛擬集合即會消失。

    $x = New-CsMcxConfiguration -Identity "site:Redmond" -InMemory
    $x.ExposedWebURL = "Internal"
    $x.SessionShortExpirationInterval = 7200
    Set-CsMcxConfiguration -Instance $x

## 詳細描述

Mobility Service 將 Lync Server 的許多功能擴充至 Apple iPhone、Windows Phone、Android 電話及 Nokia 電話等行動裝置。使用者可以使用這些電話交換立即訊息和目前狀態資訊、接收新語音信箱的通知，以及執行其他功能。多虧有推入通知服務 (Apple Push Notification Service 和 Microsoft Push Notification Service)，iPhone 或 Windows Phone 使用者可以接收這些通知，即使 Lync 在背景執行亦然。Mobility Service 也讓組織有機會啟用 \[從公司撥號\]。利用 \[從公司撥號\]，使用者可以從其行動電話撥打電話，並將此通話顯示為從公司電話撥出的通話；例如，來電顯示系統會顯示使用者的公司電話號碼，而不是使用者的行動電話號碼。

Mobility Service 本身是透過可套用至全域範圍、網站範圍或服務範圍 (僅限網頁伺服器服務) 的 Mobility Service 組態設定來管理。這些設定控制下列項目：Mobility Service 工作階段的時間長度上限；從組織防火牆外部登入的使用者是否可以使用 Lync Server Autodiscovery Service (引導 Mobility Service 使用者至適當的登錄器集區)；以及推入通知服務提供者的位置。

當您安裝 Lync Server 時，系統會在全域範圍建立一個 Mobility Service 組態設定集合；但是，系統管理員可以使用 **New-CsMcxConfiguration** Cmdlet 在網站範圍或服務範圍建立自訂組態設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsMcxConfiguration** Cmdlet：RTCUniversalServerAdmins。

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
<td><p>要建立之 Mobility Service 組態設定集合的唯一識別碼。若要在網站範圍建立設定，請使用首碼 &quot;site:&quot; 加上網站名稱。例如：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要建立在服務範圍設定的設定，請使用類似下列的語法：</p>
<p>-Identity service:WebServer:atl-cs-001.litwareinc.com</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExposedWebURL</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.McxConfiguration.ExposedWebURL</p></td>
<td><p>表示組織防火牆內部及外部的使用者都可以存取 Autodiscovery Service 所使用的 URL (External)，還是只有防火牆內部的使用者才可以存取 (Internal)。</p>
<p>允許的值為：Internal 或 External。預設值為 External。</p></td>
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
<td><p><em>PushNotificationProxyUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可將推入通知要求轉送至 Apple Push Notification Service 和 Microsoft Push Notification Service 的服務提供者 URI。PushNotificationProxyUri 必須是 SIP 位址的格式；例如：</p>
<p>-PushNotificationProxyUri &quot;sip:push@push.lync.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>SessionExpirationInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>iPhone 或 Widows Phone 使用者之行動裝置工作階段的時間長度 (秒)。如果 Lync 在這些電話的背景執行，只要工作階段到期間隔未到期，使用者仍會收到推入通知。</p>
<p>行動裝置必須傳送通知給伺服器，表示工作階段逾時前，裝置仍在使用中。若未執行此作業，裝置會列為非使用中，且使用者必須重新登入系統。</p>
<p>此屬性可以設為 120 和 4294967295 (含) 之間的任何整數值。預設值為 259200 秒 (3 天)。請注意，SessionExpirationInterval 屬性值必須大於 SessionShortExpirationInterval 屬性值。</p></td>
</tr>
<tr class="even">
<td><p><em>SessionShortExpirationInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>Android 或 Nokia 電話使用者之行動裝置工作階段的時間長度 (秒)。</p>
<p>行動裝置必須傳送通知給伺服器，表示工作階段逾時前，裝置仍在使用中。若未執行此作業，裝置會列為非使用中，且使用者必須重新登入系統。</p>
<p>此屬性可以設為 120 到 4294967295 (含) 之間的任何整數值。預設值為 3600 秒 (1 小時)。請注意，SessionExpirationInterval 屬性值必須大於 SessionShortExpirationInterval 屬性值。</p></td>
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

無。 **New-CsMcxConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WriteableConfig.Settings.McxConfiguration.McxConfiguration 物件的新執行個體。

