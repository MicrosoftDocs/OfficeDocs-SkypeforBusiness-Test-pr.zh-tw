---
title: Remove-CsMcxConfiguration
TOCTitle: Remove-CsMcxConfiguration
ms:assetid: 71904a62-a1f1-4466-9921-0a175909e117
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690026(v=OCS.15)
ms:contentKeyID: 49291284
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsMcxConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的 Lync Server 2013 Mobility Service 組態設定集合。Mobility Service 可讓行動電話使用者 (例如 iPhone 和 Windows Phone) 交換立即訊息與目前狀態資訊；從內部儲存及擷取語音信箱，而不使用無線提供者；以及利用 \[從公司撥號\] 和 \[電話撥出式會議\] 等 Lync Server 功能。Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Remove-CsMcxConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除指派給 Redmond 網站的 Mobility Service 組態設定集合。

    Remove-CsMcxConfiguration -Identity "site:Redmond"

## 範例 2

在範例 2 中，所有指派給服務範圍的 Mobility Service 組態設定都會遭到移除。為達此目的，會使用 **Get-CsMcxConfiguration** Cmdlet 搭配 Filter 參數 (篩選值 "service:\*" 可確保系統只會傳回 Identity 開頭為 "service:" 字串值的設定)。然後再將篩選後的集合管線傳送給 **Remove-CsMcxConfiguration** Cmdlet 加以刪除。

    Get-CsMcxConfiguration -Filter "service:*" | Remove-CsMcxConfiguration

## 範例 3

範例 3 會刪除 ExposedWebURL 屬性已設為 Internal 的所有 Mobility Service 組態設定。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsMcxConfiguration** Cmdlet，以傳回組織目前所使用之所有 Mobility Service 組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 ExposedWebURL 等於 (-eq) Internal 的設定。接著將篩選後的集合管線傳送到 **Remove-CsMcxConfiguration** Cmdlet，以刪除篩選後集合中的每個項目。

    Get-CsMcxConfiguration | Where-Object {$_.ExposedWebURL -eq "Internal"} | Remove-CsMcxConfiguration

## 範例 4

範例 4 會從 Lync Server 中移除所有未指派推播通知 Proxy URI 的 Mobility Service 組態設定。為達成此目的，命令會先使用 **Get-CsMcxConfiguration** Cmdlet (不含任何參數)，以傳回目前所使用之所有 Mobility Service 組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 PushNotificationProxyUri 屬性等於 (-eq) Null 值的設定。接著將所有符合該準則的設定管線傳送到 **Remove-CsMcxConfiguration** Cmdlet 加以刪除。

    Get-CsMcxConfiguration | Where-Object {$_.PushNotificationProxyUri -eq $Null} | Remove-CsMcxConfiguration

## 詳細描述

Mobility Service 將 Lync Server 的許多功能擴充至 Apple iPhone、Windows Phone、Android 手機及 Nokia 電話等行動裝置。使用者可以使用這些電話交換立即訊息和目前狀態資訊、接收新語音信箱的通知，以及執行其他功能。多虧有推播通知服務 (Apple Push Notification Service 和 Microsoft 推播通知服務)，iPhone 或 Windows Phone 使用者可以接收這些通知，即使 Lync 在背景執行。Mobility Service 也讓組織有機會啟用 \[從公司撥號\]。利用 \[從公司撥號\]，使用者可以從其行動電話撥打電話，並將此通話顯示為從公司電話撥出的通話；例如，來電顯示系統會顯示使用者的公司電話號碼，而不是使用者的行動電話號碼。

Mobility Service 本身是透過可套用至全域範圍、網站範圍或服務範圍 (僅限網頁伺服器服務) 的 Mobility Service 組態設定來管理。這些設定控制下列項目：Mobility Service 工作階段的時間長度上限；從組織防火牆外部登入的使用者是否可以使用自動探索服務 (將 Mobility Service 使用者導向適當的登錄器集區)；以及推播通知服務提供者的位置。

當您安裝 Lync Server 時，系統會在全域範圍建立一個 Mobility Service 組態設定集合；但是，系統管理員可以在網站範圍或服務範圍建立自訂組態設定。稍後，您可以使用 **Remove-CsMcxConfiguration** Cmdlet 移除這些自訂設定。若您移除服務設定，先前受到這些設定管理的 Mobility Service 伺服器，將變成由網站設定 (如果存在) 或全域設定管理。若果您移除網站設定，則伺服器將變成由全域設定管理。

請注意，您也可以對全域設定執行 **Remove-CsMcxConfiguration** Cmdlet。不過，這樣做並不會移除全域設定，而只是將全域集合中的屬性重設為其預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsMcxConfiguration** Cmdlet：RTCUniversalServerAdmins。

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
<td><p>要移除之 Mobility Service 組態設定的唯一識別碼。若要「移除」全域設定，請使用下列語法：</p>
<p>-Identity global</p>
<p>請注意，您無法真正移除全域設定，您所能做的只有將屬性重設回預設值。</p>
<p>若要將設定從網站範圍移除，請使用類似下列的語法：</p>
<p>-Identity site:Redmond</p>
<p>若要移除在服務範圍設定的設定，請使用類似下列的語法：</p>
<p>-Identity service:WebServer:atl-cs-001.litwareinc.com</p>
<p>您無法在指定 Identity 時使用萬用字元。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WriteableConfig.Settings.McxConfiguration.McxConfiguration。**Remove-CsMcxConfiguration** Cmdlet 接受管線傳送的 McxConfiguration 物件輸入。

## 傳回類型

無。而是由 Cmdlet 刪除 Microsoft.Rtc.Management.WriteableConfig.Settings.McxConfiguration.McxConfiguration 物件的執行個體。

