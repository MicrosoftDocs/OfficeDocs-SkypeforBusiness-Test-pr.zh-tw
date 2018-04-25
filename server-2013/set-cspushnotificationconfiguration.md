---
title: Set-CsPushNotificationConfiguration
TOCTitle: Set-CsPushNotificationConfiguration
ms:assetid: 3aacdb2b-b6dd-4615-a3f9-68360f3ae483
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690013(v=OCS.15)
ms:contentKeyID: 49290641
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPushNotificationConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有之推播通知組態設定的集合。推播通知服務 (Apple 推播通知服務及 Microsoft 推播通知服務) 可傳送事件的通知，例如傳送給行動裝置 (如 iPhone 及 Windows Phone) 的新立即訊息或新語音信箱 ，即使這些裝置上的 Lync 應用程式目前為暫止或在背景中執行也不受影響。 Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Set-CsPushNotificationConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPushNotificationConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableApplePushNotificationService <$true | $false>] [-EnableMicrosoftPushNotificationService <$true | $false>] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會停用 Redmond 網站來自 Apple Push Notification Service 的推播通知。

    Set-CsPushNotificationConfiguration -Identity "site:Redmond" -EnableApplePushNotificationService $False

## 範例 2

範例 2 會為目前主控推播通知設定的所有網站，停用來自 Apple Push Notification Service 的推播通知。為達成此目的，命令會先使用 **Get-CsPushNotificationConfiguration** Cmdlet 和 Filter 參數，傳回在網站範圍設定的所有推播通知設定；篩選值 "site:\*" 可將傳回的設定限制在 Identity 開頭為 "site:" 字串值的設定。然後再將該設定集合管線傳送到 **Set-CsPushNotificationConfiguration** Cmdlet，以取得集合中的每個項目，並將 EnableApplePushNotificationService 屬性設為 False。

    Get-CsPushNotificationConfiguration -Filter "site:*" | Set-CsPushNotificationService -EnableApplePushNotificationService $False

## 範例 3

範例 3 會示範如何找到所有推播通知設定，其中來自 Microsoft 推播通知服務的推播通知都已停用，以及如何停用每個設定的 Apple Push Notification Service 推播通知。為了執行此工作，命令會先使用 **Get-CsPushNotificationConfiguration** Cmdlet 傳回組織目前所使用之所有推播通知設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，此 Cmdlet 只會選取 EnableMicrosoftPushNotificationService 屬性等於 (-eq) False 的設定。接著將篩選後的集合管線傳送到 **Set-CsPushNotificationConfiguration** Cmdlet，以取得篩選後之集合中的每個項目，並將 EnableApplePushNotificationService 屬性設為 False。

    Get-CsPushNotificationConfiguration | Where-Object {$_.EnableMicrosoftPushNotificationService -eq $False} | Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False

## 詳細描述

Apple 推播通知服務 和 Microsoft 推播通知服務可讓在其 Apple iPhone 或 Windows Phone 上執行 Lync 的使用者接收關於 Lync 事件的通知，即使 Lync 已暫停或在背景執行亦然。例如，使用者可以接收類似下列事件的通知：

\- 新立即訊息工作階段或會議的邀請

\- 新立即訊息

\- 新語音信箱

如果沒有推播通知服務，使用者只有當 Lync 在前景執行且做為使用中應用程式時，才會收到這些通知。

系統管理員可以啟用或停用 iPhone 使用者及/或 Windows Phone 使用者的推播通知 (預設會停用 iPhone 使用者和 Windows Phone 使用者的推播通知)。系統管理員可以使用 **Set-CsPushNotificationConfiguration** Cmdlet，在全域範圍啟用或停用推播通知，也可以使用 **New-CsPushNotificationConfiguration** Cmdlet，在網站範圍建立自訂推播通知，並使用 **Set-CsPushNotificationConfiguration** Cmdlet 修改這些自訂設定。

系統管理員只需要管理兩個推播通知組態設定的屬性值：EnableApplePushNotificationService 可決定推播通知是否要傳送給 iPhone 使用者；EnableMicrosoftPushNotificationService 可決定推播通知是否要傳送給 Windows Phone 使用者。請注意，這兩個屬性值不一定要設為相同的值。例如，您可以啟用 Windows Phone 使用者的推播通知 (將 EnableMicrosoftPushNotificationService 設為 True)，同時停用 iPhone 使用者的推播通知 (將 EnableApplePushNotificationService 設為 False)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsPushNotificationConfiguration** Cmdlet：RTCUniversalServerAdmins。

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
<td><p><em>EnableApplePushNotificationService</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，iPhone 使用者會從 Apple Push Notification Service 收到推播通知。設為 False 時，iPhone 使用者不會收到這些通知。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMicrosoftPushNotificationService</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，Windows Phone 使用者就會收到來自 Microsoft 推播通知服務的推播通知。設為 False 時，Windows Phone 使用者就不會收到這些通知。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指出要修改之推播通知組態設定的 Identity。若要參照全域設定，請使用下列語法：</p>
<p>-Identity global</p>
<p>若要參照網站設定，請使用類似如下的語法：</p>
<p>-Identity site:Redmond</p>
<p>請注意，指定 Identity 時，無法使用萬用字元。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>推播設定物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要修改推播通知設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName，TenantID</p>
<p>倘若使用的是 Windows PowerShell 遠端工作階段並僅連線至 商務用 Skype Online，則無需包含 Tenant 參數。相反地，系統將會根據您的連線資訊自動填入租用戶識別碼。Tenant 參數主要用於混合式部署。</p></td>
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

Microsoft.Rtc.Management.WriteableConfig.Settings.PushNotificationConfiguration.PushNotificationConfiguration。 **Set-CsPushNotificationConfiguration** Cmdlet 接受管線傳送的 PushNotificationConfiguration 物件執行個體。

## 傳回類型

無。反之， **Set-CsPushNotificationConfiguration** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WriteableConfig.Settings.PushNotificationConfiguration.PushNotificationConfiguration 物件執行個體。

