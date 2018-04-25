---
title: Set-CsMcxConfiguration
TOCTitle: Set-CsMcxConfiguration
ms:assetid: eaff70d9-97fa-482c-b9fb-a90263685b29
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690050(v=OCS.15)
ms:contentKeyID: 49292701
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMcxConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的 Lync Server Mobility Service 組態設定集合。Mobility Service 可讓行動電話使用者 (例如 iPhone 和 Windows Phone) 交換立即訊息與目前狀態資訊；從內部儲存及擷取語音信箱，而不使用無線提供者；以及利用 \[從公司撥號\] 和 \[電話撥出式會議\] 等 Lync 功能。 Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Set-CsMcxConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsMcxConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-ExposedWebURL <External | Internal>] [-Force <SwitchParameter>] [-PushNotificationProxyUri <String>] [-SessionExpirationInterval <UInt32>] [-SessionShortExpirationInterval <UInt32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會將指派給 Redmond 網站之 Mobility Service 組態設定的 ExposedWebURL 屬性設為 External。

    Set-CsMcxConfiguration -Identity site:Redmond -ExposedWebURL External

## 範例 2

範例 2 顯示單一命令如何將相同的屬性值指派給組織目前使用的所有 Mobility Service 組態設定。為達此目的，命令會先不指定任何參數而直接使用 **Get-CsMcxConfiguration** Cmdlet 傳回所有現有的 Mobility Service 組態設定集合。然後再將該集合傳送給 **Set-CsMcxConfiguration**，以將集合中每個項目的 ExposedWebURL 屬性設為 External。

    Get-CsMcxConfiguration | Set-CsMcxConfiguration -ExposedWebURL External

## 範例 3

在範例 3 中，會修改所有 SessionShortExpirationInterval 大於 3600 秒的 Mobility Service 組態設定，以將該屬性值設為 3600；如此可有效地將組織中所有 Mobility Service 組態設定的最大值設為 3600 秒。為達成此目的，會先呼叫 **Get-CsMcxConfiguration** Cmdlet (不含任何參數) 傳回目前所使用之所有 Mobility Service 組態設定的集合。然後，此集合會管線傳送到 Where-Object Cmdlet，這會只挑出 SessionShortExpirationInterval 屬性大於 (-gt) 3600 的設定。接著將篩選後的集合管線傳送到 **Set-CsMcxConfiguration** Cmdlet，以將集合中每個項目的 SessionShortExpirationInterval 屬性值設為 3600。

    Get-CsMcxConfiguration | Where-Object {$_.SessionShortExpirationInterval -gt 3600} | Set-CsMcxConfiguration -SessionShortExpirationInterval 3600

## 詳細描述

Lync Server Mobility Service 將 Lync 的許多功能擴充至 Apple iPhone、Windows Phone、Android 電話及 Nokia 電話等行動裝置。使用者可以使用這些電話交換立即訊息和目前狀態資訊、接收新語音信箱的通知，以及執行其他功能。多虧有推入通知服務 (Apple Push Notification Service 和 Microsoft Push Notification Service)，iPhone 或 Windows Phone 使用者可以接收這些通知，即使 Lync Server 在背景執行亦然。Mobility Service 也讓組織有機會啟用 \[從公司撥號\]。利用 \[從公司撥號\]，使用者可以從其行動電話撥打電話，並將此通話顯示為從公司電話撥出的通話；例如，來電顯示系統會顯示使用者的公司電話號碼，而不是使用者的行動電話號碼。

Mobility Service 本身是透過可套用至全域範圍、網站範圍或服務範圍 (僅限網頁伺服器服務) 的 Mobility Service 組態設定來管理。這些設定控制下列項目：Mobility Service 工作階段的時間長度上限；從組織防火牆外部登入的使用者是否可以使用 Lync Server Autodiscovery Service (引導 Mobility Service 使用者至適當的登錄器集區)；以及推入通知服務提供者的位置。

**Set-CsMcxConfiguration** Cmdlet 可讓系統管理員修改任何現有的 Mobility Service 組態設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsMcxConfiguration** Cmdlet：RTCUniversalServerAdmins。

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>ExposedWebURL</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.McxConfiguration.ExposedWebURL</p></td>
<td><p>表示組織防火牆內部及外部的使用者都可以存取 Autodiscovery Service 所使用的 URL (External)，還是只有防火牆內部的使用者才可以存取 (Internal)。</p>
<p>允許的值為：Internal 或 External。預設值為 External。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>代表要修改之 Mobility Service 組態設定集合的唯一識別碼。若要修改全域設定，請使用下列語法：</p>
<p>-Identity global</p>
<p>若要修改網站範圍上的設定，請使用首碼 &quot;site:&quot; 加上網站名稱。例如：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要修改在服務範圍設定的設定，請使用類似下列的語法：</p>
<p>-Identity service:WebServer:atl-cs-001.litwareinc.com</p>
<p>若未指定此參數，則 <strong>Set-CsMcxConfiguration</strong> Cmdlet 會修改全域設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>MCX 組態物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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

Microsoft.Rtc.Management.WriteableConfig.Settings.McxConfiguration.McxConfiguration 物件。 **Set-CsMcxConfiguration** Cmdlet 接受管線傳送的 McxConfiguration 物件執行個體。

## 傳回類型

無。而是由 **Set-CsMcxConfiguration** Cmdlet 修改現有的 Microsoft.Rtc.Management.WriteableConfig.Settings.McxConfiguration.McxConfiguration 物件執行個體。

