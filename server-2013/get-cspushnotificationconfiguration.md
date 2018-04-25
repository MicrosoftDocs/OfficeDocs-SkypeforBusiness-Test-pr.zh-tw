---
title: Get-CsPushNotificationConfiguration
TOCTitle: Get-CsPushNotificationConfiguration
ms:assetid: ec2c17e5-ac4d-4d21-995a-642c5cf5c7bc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690049(v=OCS.15)
ms:contentKeyID: 49292710
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPushNotificationConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取組織目前所使用之推播通知組態設定的資訊。推播通知服務 (Apple 推播通知服務及 Microsoft 推播通知服務) 可傳送事件的通知，例如傳送給行動裝置 (如 iPhone 及 Windows Phone) 的新立即訊息或新語音信箱 ，即使這些裝置上的 Lync 應用程式目前為暫止或在背景中執行也不受影響。 Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Get-CsPushNotificationConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPushNotificationConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## 範例

## 範例 1

範例 1 會傳回設定供組織使用之所有推入通知設定的資訊。

    Get-CsPushNotificationConfiguration

## 範例 2

範例 2 所示的命令會傳回單一推入通知設定集合的資訊：為 Redmond 網站設定的設定。

    Get-CsPushNotificationConfiguration -Identity "site:Redmond"

## 範例 3

範例 3 中的命令會傳回所有指派給網站範圍的推入通知設定。為達此目的，命令會使用 Filter 參數搭配篩選值 "site:\*" (此篩選值只會傳回 Identity 開頭為字串值 "site:" 的設定)。

    Get-CsPushNotificationConfiguration -Filter "site:*"

## 範例 4

範例 4 會傳回已停用 iPhones 中之推入通知功能的所有推入通知設定。為達此目的，命令會先使用 **Get-CsPushNotificationConfiguration** Cmdlet 傳回組織目前所使用的所有推入通知設定集合。然後再將該集合管線傳送到 **Where-Object** Cmdlet，以選取 EnableApplePushNotificationService 屬性等於 (-eq) False 的設定。

    Get-CsPushNotificationConfiguration | Where-Object {$_.EnableApplePushNotificationService -eq $False}

## 範例 5

範例 5 會傳回已停用 Apple Push Notification Service 及/或 Microsoft 推播通知服務的所有推播通知設定資訊。為達此目的，命令會先使用 **Get-CsPushNotificationConfiguration** Cmdlet 傳回目前使用之所有推播通知設定的集合。然後再將此集合以管線傳送到 Where-Object Cmdlet，以挑出符合下列其中一個 (或兩個) 準則的設定：1) EnableApplePushNotificationService 屬性等於 (-eq) False；2) EnableMicrosoftPushNotificationService 屬性等於 False。–or 運算子會指示 Where-Object 尋找符合其中一個準則的設定。若要將傳回的資料限制在兩個服務皆已停用的設定，請改用 –and 運算子：

Get-CsPushNotificationConfiguration | Where-Object {$\_.EnableApplePushNotificationService –eq $False –and $\_.EnableMicrosoftPushNotificationService –eq $False}

    Get-CsPushNotificationConfiguration | Where-Object {$_.EnableApplePushNotificationService -eq $False -or $_.EnableMicrosoftPushNotificationService -eq $False}

## 詳細描述

Apple Push Notification Service 和 Microsoft 推播通知服務 可讓在其 Apple iPhone 或 Windows Phone 上執行 Lync 的使用者接收關於 Lync 事件的通知，即使 Lync 已暫停或在背景執行亦然。例如，使用者可以接收類似下列事件的通知：

\- 新立即訊息工作階段或會議的邀請

\- 新立即訊息

\- 新語音信箱

如果沒有推入通知服務，使用者只有當 Lync 在前景執行且做為使用中應用程式時，才會收到這些通知。

系統管理員可以啟用或停用 iPhone 使用者及 (或) Windows Phone 使用者的推入通知功能 (預設會停用 iPhone 使用者和 Windows Phone 使用者的推入通知功能)。系統管理員可以使用 **Set-CsPushNotificationConfiguration** Cmdlet 在全域範圍啟用或停用推入通知功能，也可以使用 **New-CsPushNotificationConfiguration** Cmdlet 在網站範圍建立自訂推入通知設定。

**Get-CsPushNotificationConfiguration** Cmdlet 可讓您傳回組織目前使用的推入通知設定資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsPushNotificationConfiguration** Cmdlet：RTCUniversalServerAdmins。

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
<td><p>可讓您使用萬用字元傳回一或多個推入通知組態設定集合。若要傳回在此網站範圍所設定之所有設定集合，請使用下列語法：</p>
<p>-Filter site:*</p>
<p>若要傳回在其 Identity (您可篩選的唯一屬性) 某處具有字串值 &quot;Canada&quot; 的所有設定集合，請使用下列語法：</p>
<p>-Filter &quot;*Canada*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示您要傳回之推入通知設定集合的唯一識別碼。若要參照全域設定，請使用下列語法：</p>
<p>-Identity global</p>
<p>若要參照在此網站範圍設定的集合，請使用類似下列的語法：</p>
<p>-Identity site:Redmond</p>
<p>請注意，如有指定 Identity，即無法使用萬用字元。如果您必須使用萬用字元，請改為包含 Filter 參數。</p>
<p>若未指定此參數，則 <strong>Get-CsPushNotificationConfiguration</strong> Cmdlet 會傳回組織使用的所有推播通知組態設定集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區本機複本擷取推入通知組態資料，而不從 中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要修改推入通知組態設定之 Office 365 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>如果您正在使用 Windows PowerShell 的遠端工作階段，並且僅連線至 商務用 Skype Online，您不需要包含 Tenant 參數，而是將會根據您的連線資訊自動填入租用戶 ID。Tenant 參數主要用於混合部署。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Get-CsPushNotificationConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPushNotificationConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WriteableConfig.Settings.PushNotificationConfiguration.PushNotificationConfiguration 物件的執行個體。

