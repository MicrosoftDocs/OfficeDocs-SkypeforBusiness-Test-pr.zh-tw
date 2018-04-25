---
title: New-CsPushNotificationConfiguration
TOCTitle: New-CsPushNotificationConfiguration
ms:assetid: 8bf61c72-7902-4075-9388-47a7dd4e649c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690027(v=OCS.15)
ms:contentKeyID: 49291598
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPushNotificationConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

在網站範圍建立新的推播通知組態設定集合。推播通知服務 (Apple 推播通知服務及 Microsoft 推播通知服務) 可傳送事件的通知，例如傳送給行動裝置 (如 iPhone 及 Windows Phone) 的新立即訊息或新語音信箱 ，即使這些裝置上的 Lync 應用程式目前為暫止或在背景中執行也不受影響。 Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    New-CsPushNotificationConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableApplePushNotificationService <$true | $false>] [-EnableMicrosoftPushNotificationService <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會為 Redmond 網站建立新的推播通知設定集合，並啟用 Apple Push Notification Service 和 Microsoft 推播通知服務的推播通知功能。後者的作法是將 EnableApplePushNotificationService 和 EnableMicrosoftPushNotificationService 屬性設為 True。

    New-CsPushNotificationConfiguration -Identity "site:Redmond" -EnableApplePushNotificationService $True -EnableMicrosoftPushNotificationService -$True

## 範例 2

範例 2 顯示如何建立每個 Lync Server 網站的一組推播組態設定。為達成此目的，命令會先使用 **Get-CsSite** Cmdlet 傳回所有 Lync Server 網站的集合。然後將此集合管線傳送給 **ForEach-Object** Cmdlet，以針對集合中的每個網站呼叫 **New-CsPushNotificationConfiguration** Cmdlet，這會針對各網站建立一組新的推播通知組態設定。請注意，如果任何網站已代管推播通知組態設定的集合，則此命令會失敗。

    Get-CsSite | ForEach-Object {New-CsPushConfigurationNotification -Identity $_.Identity}

## 範例 3

範例 3 會示範如何使用 InMemory 參數建立一開始僅存在於記憶體中的推播通知組態設定的集合。為達成此目的，此範例會建立新的設定集合 (Identity 為 site:Redmond)，並將此集合儲存在名為 $x 的變數中。請注意，當第一個命令執行之後，集合只會存在於記憶體中；如果您執行 **Get-CsPushNotificationConfiguration** Cmdlet，將看不到 site:Redmond 的項目。

在接下來的兩個命令中，會將此虛擬設定集合的 EnableApplePushNotificationService 和 EnableMicrosoftPushNotificationService 屬性設為 True，以啟用 Apple Push Notification Service 和 Microsoft 推播通知服務的推播通知功能。最後，最後一個命令會使用 **Set-CsPushNotificationConfiguration** Cmdlet，以將虛擬推播通知設定轉換為套用到 Redmond 網站的實際設定集合。若您沒有呼叫 **Set-CsPushNotificationConfiguration** Cmdlet，這些設定將只會保留在記憶體中，而且一旦終止 Windows PowerShell 工作階段或刪除 $x 變數，這些設定就會消失。

    $x = New-CsPushNotificationConfiguration -Identity "site:Redmond" -InMemory
    $x.EnableApplePushNotificationService = $True 
    $x.EnableMicrosoftPushNotificationService = $True
    Set-CsPushNotificationConfiguration -Instance $x

## 詳細描述

Apple Push Notification Service 和 Microsoft 推播通知服務 可讓在其 Apple iPhone 或 Windows Phone 上執行 Lync 的使用者接收關於 Lync 事件的通知，即使 Lync 已暫停或在背景執行亦然。例如，使用者可以接收類似下列事件的通知：

\- 新立即訊息工作階段或會議的邀請

\- 新立即訊息

\- 新語音信箱

如果沒有推入通知服務，使用者只有當 Lync 在前景執行且做為使用中應用程式時，才會收到這些通知。

系統管理員可以啟用或停用 iPhone 使用者及 (或) Windows Phone 使用者的推入通知功能 (預設會停用 iPhone 使用者和 Windows Phone 使用者的推入通知功能)。系統管理員可以使用 **Set-CsPushNotificationConfiguration** Cmdlet 在全域範圍啟用或停用推入通知功能，也可以使用 **New-CsPushNotificationConfiguration** Cmdlet 在網站範圍建立自訂推入通知設定。這讓系統管理員可以提供推入通知功能給某些網站 (例如 Redmond) 的使用者，同時限制在其他網站使用這些通知。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsPushNotificationConfiguration** Cmdlet：RTCUniversalServerAdmins。

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
<td><p>您只能在網站範圍建立推入通知設定。若要指定新的網站設定集合，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>請注意，如果 Redmond 網站已託管推入通知設定集合，則此命令會失敗。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableApplePushNotificationService</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，iPhone 使用者會從 Apple Push Notification Service 收到推入通知。設為 False 時，iPhone 使用者不會收到這些通知。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMicrosoftPushNotificationService</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，Windows Phone 使用者就會收到來自 Microsoft 推播通知服務的推播通知。設為 False 時，Windows Phone 使用者就不會收到這些通知。</p>
<p>預設值為 False。</p></td>
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
<td><p>建立物件參照，但而不實際將物件認可為永久變更。若將此參數所呼叫的 Cmdlet 輸出指派給變數，將可變更物件參照的屬性，然後呼叫此 Cmdlet 的對應 Set- Cmdlet 認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要建立新推播通知組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName，TenantID</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **New-CsPushNotificationConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsPushNotificationConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WriteableConfig.Settings.PushNotificationConfiguration.PushNotificationConfiguration 物件的新執行個體。

