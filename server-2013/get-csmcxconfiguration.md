---
title: Get-CsMcxConfiguration
TOCTitle: Get-CsMcxConfiguration
ms:assetid: a09c0d49-5377-4a22-89e6-2751030ccf20
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690031(v=OCS.15)
ms:contentKeyID: 49291836
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsMcxConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取組織目前所使用之 Lync Server Mobility Service 組態設定的資訊。Mobility Service 可讓行動電話使用者 (例如 iPhone 和 Windows Phone) 交換立即訊息與目前狀態資訊；從內部儲存及擷取語音信箱，而不使用無線提供者；以及利用 \[從公司撥號\] 和 \[電話撥出式會議\] 等 Lync Server 功能。Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Get-CsMcxConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsMcxConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織目前使用的所有 Mobility Service 組態設定資訊。

    Get-CsMcxConfiguration

## 範例 2

在範例 2 中，僅會傳回全域的 Mobility Service 組態設定集合資訊。

    Get-CsMcxConfiguration -Identity "global"

## 範例 3

範例 3 傳回所有指派給服務範圍的 Mobility Service 組態設定資訊。為達此目的，會加上 Filter 參數並搭配字串值 "service:\*"。該篩選值會傳回 Identity 開頭為字串值 "service:" 的所有 Mobility Service 組態設定。

    Get-CsMcxConfiguration -Filter "service:*"

## 範例 4

在範例 4 中，僅會傳回 ExposedWebURL 屬性等於 External 的 Mobility Service 組態設定。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsMcxConfiguration** Cmdlet，以傳回組織目前使用之所有 Mobility Service 組態設定的集合。然後再將該集合管線傳送給 **Where-Object** Cmdlet，這會只挑出 ExposedWebURL 屬性等於 (-eq) External 的設定。

    Get-CsMcxConfiguration | Where-Object {$_.ExposedWebURL -eq "External"}

## 範例 5

範例 5 會傳回 SessionExpirationInterval 屬性值設為小於預設值 259200 秒 (72 小時) 的所有 Mobility Service 組態設定。做法是先使用 **Get-CsMcxConfiguration** Cmdlet，以傳回所有現有的 Mobility Service 組態設定。然後將該集合管線傳送給 **Where-Object** Cmdlet，這會只選取 SessionExpirationInterval 屬性小於 259200 的設定。

    Get-CsMcxConfiguration | Where-Object {$_.SessionExpirationInterval -lt 259200}

## 詳細描述

Lync Server Mobility Service 將 Lync Server 的許多功能擴充至 Apple iPhone、Windows Phone、Android 電話及 Nokia 電話等行動裝置。使用者可以使用這些電話交換立即訊息和目前狀態資訊、接收新語音信箱的通知，以及執行其他功能。多虧有推入通知服務 (Apple Push Notification Service 和 Microsoft Push Notification Service)，iPhone 或 Windows Phone 使用者可以接收這些通知，即使 Lync 在背景執行亦然。Mobility Service 也讓組織有機會啟用 \[從公司撥號\]。利用 \[從公司撥號\]，使用者可以從其行動電話撥打電話，並將此通話顯示為從公司電話撥出的通話；例如，來電顯示系統會看見使用者的公司電話號碼，而不是使用者的行動電話號碼。

Mobility Service 本身是透過可套用至全域範圍、網站範圍或服務範圍 (僅限網頁伺服器服務) 的 Mobility Service 組態設定來管理。這些設定控制下列項目：Mobility Service 工作階段的時間長度上限；從組織防火牆外部登入的使用者是否可以使用 Lync Server Autodiscovery Service (引導 Mobility Service 使用者至適當的登錄器集區)；以及推入通知服務提供者的位置。**Get-CsMcxConfiguration** Cmdlet 提供方法，讓系統管理員可以擷取組織目前使用的所有 Mobility Service 組態設定資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsMcxConfiguration** Cmdlet：RTCUniversalServerAdmins。

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您使用萬用字元傳回 Mobility Service 組態設定集合。例如，若要傳回在此網站範圍所設定之所有設定集合，請使用下列語法：</p>
<p>-Filter site:*</p>
<p>若要傳回在服務範圍設定的所有設定集合，請使用下列語法：</p>
<p>-Filter service:*</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示您要傳回之 Mobility Service 組態設定集合的唯一識別碼。若要參照全域設定，請使用下列語法：</p>
<p>-Identity global</p>
<p>若要參照在此網站範圍設定的集合，請使用類似下列的語法：</p>
<p>-Identity site:Redmond</p>
<p>若要參照在服務範圍設定的集合，請使用類似下列的語法：</p>
<p>-Identity service:WebServer:atl-cs-001.litwareinc.com</p>
<p>請注意，如有指定 Identity，即無法使用萬用字元。如果您必須使用萬用字元，請改用 Filter 參數。</p>
<p>若未指定此參數，則 <strong>Get-CsMcxConfiguration</strong> 會傳回組織使用之所有 Mobility Service 組態設定的集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 本機複本擷取 Mobility Service 組態資料，而不從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Get-CsMcxConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsMcxConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WriteableConfig.Settings.McxConfiguration.McxConfiguration 物件的執行個體。

