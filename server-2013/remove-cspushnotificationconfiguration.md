---
title: Remove-CsPushNotificationConfiguration
TOCTitle: Remove-CsPushNotificationConfiguration
ms:assetid: 77574e30-a75f-4aaa-b2d8-ccbabda31797
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690028(v=OCS.15)
ms:contentKeyID: 49291369
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPushNotificationConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

刪除現有之推播通知設定的集合。推播通知服務 (Apple 推播通知服務及 Microsoft 推播通知服務) 可傳送事件的通知，例如傳送給行動裝置 (如 iPhone 及 Windows Phone) 的新立即訊息或新語音信箱 ，即使這些裝置上的 Lync 應用程式目前為暫止或在背景中執行也不受影響。 Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Remove-CsPushNotificationConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除指派給 Redmond 網站的推入通知設定集合。

    Remove-CsPushNotificationConfiguration -Identity "site:Redmond"

## 範例 2

範例 2 會刪除在網站範圍設定的所有推播通知設定。為達此目的，Cmdlet 會先使用 **Get-CsPushNotificationConfiguration** Cmdlet 搭配 Filter 參數，以傳回在網站範圍設定的所有設定集合 (篩選值 "site:\*" 可將傳回的項目限制在 Identity 開頭為 "site:" 字串值的設定)。然後將網站範圍設定管線傳送到 **Remove-CsPushNotificationConfiguration** Cmdlet，以刪除。

    Get-CsPushNotificationConfiguration -Filter "site:*" | Remove-CsPushNotificationConfiguration

## 範例 3

範例 3 顯示如何移除已停用 Microsoft 推播通知服務之推播通知功能的所有推播通知組態設定。為達成此目的，命令會先使用 **Get-CsPushNotificationConfiguration** Cmdlet，以傳回目前所使用之所有推播通知設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 EnableMicrosoftPushNotificationService 屬性等於 (-eq) False 的設定。接著將篩選後的集合管線傳送到 **Remove-CsPushNotificationConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsPushNotificationConfiguration | Where-Object {$_.EnableMicrosoftPushNotificationService -eq $False} | Remove-CsPushNotificationConfiguration

## 詳細描述

Apple Push Notification Service 和 Microsoft 推播通知服務 可讓在其 Apple iPhone 或 Windows Phone 上執行 Lync 的使用者接收關於 Lync 事件的通知，即使 Lync 已暫停或在背景執行亦然。例如，使用者可以接收類似下列事件的通知：

\- 新立即訊息工作階段或會議的邀請

\- 新立即訊息

\- 新語音信箱

如果沒有推入通知服務，使用者只有當 Lync 在前景執行且做為使用中應用程式時，才會收到這些通知。

系統管理員可以啟用或停用 iPhone 使用者及 (或) Windows Phone 使用者的推入通知功能 (預設會停用 iPhone 使用者和 Windows Phone 使用者的推入通知功能)。系統管理員可以使用 **Set-CsPushNotificationConfiguration** Cmdlet 在全域範圍啟用或停用推入通知功能，也可以使用 **New-CsPushNotificationConfiguration** Cmdlet 在網站範圍建立自訂推入通知設定。

稍後，您可以使用 **Remove-CsPushNotificationConfiguration** Cmdlet 刪除這些自訂設定。如果您刪除在網站範圍設定的設定，則該網站的使用者將自動變成由全域推入通知設定管理。

請注意，您也可以對全域設定執行 **Remove-CsPushNotificationConfiguration** Cmdlet。不過，如此並不會移除全域設定，而是將全域設定中的屬性全部重設為預設值。在此情況下，表示會停用 Apple 推播通知服務和 Microsoft 推播通知服務兩者的推播通知功能。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsPushNotificationConfiguration** Cmdlet：RTCUniversalServerAdmins。

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
<td><p>要移除之推入通知組態設定集合的唯一識別碼。若要移除全域集合，請使用下列語法：</p>
<p>-Identity global</p>
<p>請注意，您無法真正移除全域設定，您只能將屬性重設回預設值。</p>
<p>若要移除網站集合，請使用類似下列的語法：</p>
<p>-Identity site:Redmond</p>
<p>在指定原則 Identity 時不能使用萬用字元。</p></td>
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
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要刪除推播通知組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName，TenantID</p></td>
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

Microsoft.Rtc.Management.WriteableConfig.Settings.PushNotificationConfiguration.PushNotificationConfiguration。 **Remove-CsPushNotificationConfiguration** Cmdlet 接受管線傳送的 PushNotificationConfiguration 物件執行個體。

## 傳回類型

無。反之， **Remove-CsPushNotificationConfiguration** Cmdlet 會刪除 Microsoft.Rtc.Management.WriteableConfig.Settings.PushNotificationConfiguration.PushNotificationConfiguration 物件的執行個體。

