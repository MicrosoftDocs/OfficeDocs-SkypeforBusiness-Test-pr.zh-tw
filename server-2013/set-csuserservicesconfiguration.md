---
title: Set-CsUserServicesConfiguration
TOCTitle: Set-CsUserServicesConfiguration
ms:assetid: 51d76f29-4b2b-4208-962c-c5420414ad1b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398340(v=OCS.15)
ms:contentKeyID: 49290915
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUserServicesConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改 User Services 組態設定的現有集合。User Services 可協助維護目前狀態資訊及管理會議。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsUserServicesConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsUserServicesConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AnonymousUserGracePeriod <TimeSpan>] [-Confirm [<SwitchParameter>]] [-DeactivationGracePeriod <TimeSpan>] [-DefaultSubscriptionExpiration <Int64>] [-Force <SwitchParameter>] [-MaintenanceTimeOfDay <DateTime>] [-MaxContacts <UInt16>] [-MaxPersonalNotes <UInt32>] [-MaxScheduledMeetingsPerOrganizer <UInt32>] [-MaxSubscriptionExpiration <Int64>] [-MaxSubscriptions <UInt16>] [-MinSubscriptionExpiration <Int64>] [-PresenceProviders <PSListModifier>] [-SubscribeToCollapsedDG <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改 Redmond 網站的 User Services 組態設定 (-identity site:Redmond)。在此範例中，AnonymousUserGracePeriod 設為 30 分鐘 (00 小時：30 分鐘：00 秒) 的 A/V Edge 組態設定。

    Set-CsUserServicesConfiguration -Identity site:Redmond -AnonymousUserGracePeriod "00:30:00"

## 範例 2

在範例 2 中會修改套用至 Redmond 網站之 User Services 組態設定的 MaintenanceTimeOfDay 屬性。使用 MaintenanceTimeOfDay 參數與參數值 13:30 可完成這個工作。這樣會將一天的維護時間設為 1:30 PM (24 小時制的 13 時 30 分)。

    Set-CsUserServicesConfiguration -Identity site:Redmond -MaintenanceTimeOfDay "13:30"

## 範例 3

範例 3 會擷取在服務範圍套用的所有 User Services 組態設定，然後針對每一個項目修改允許的連絡人數目。為了執行此工作，命令會先使用 **Get-CsUserServicesConfiguration** Cmdlet 搭配 Filter 參數，以擷取在服務範圍設定的所有設定；篩選值 "service:\*" 會將傳回的資料限制在 Identity 開頭字元為 "service:" 的設定。然後再將篩選後的集合傳送到 **Set-CsUserServicesConfiguration** Cmdlet，以取得集合中的每一個項目，並將 MaxContacts 屬性設為 300。

    Get-CsUserServicesConfiguration -Filter "service:*" | Set-CsUserServicesConfiguration -MaxContacts 300

## 範例 4

範例 4 會修改允許使用者擁有的連絡人數目超過 300 個的所有 User Services 組態設定；修改完成後，就不允許設定超過 300 個連絡人。為達成此目的，命令會先呼叫不含任何其他參數的 **Get-CsUserServicesConfiguration** Cmdlet，以傳回組織目前所使用之所有 User Services 組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 MaxContacts 屬性大於 300 的設定。接著將篩選後的集合管線傳送到 **Set-CsUserServicesConfiguration** Cmdlet，以取得已篩選之集合中的每個項目，並將允許之連絡人的數目上限變更為 300。

    Get-CsUserServicesConfiguration | Where-Object {$_.MaxContacts -gt 300} | Set-CsUserServicesConfiguration -MaxContacts 300

## 詳細描述

Lync Server 依賴 User Services 協助維護使用者的目前狀態資訊，以及管理會議。然後，**CsUserServicesConfiguration** Cmdlet 用於管理全域範圍、網站範圍和服務範圍的 User Services 組態設定 (請注意，可主控 User Services 組態設定的唯一服務為 User Services 本身)。這些設定有助於決定使用者可擁有的連絡人數目、使用者可在任何一個時間中排程的會議數，以及所指定的會議可保持為作用中的時間長度等作業。

The **Set-CsUserServicesConfiguration** Cmdlet 可讓系統管理員修改目前所使用之任何 (或所有) User Services 組態設定的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsUserServicesConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUserServicesConfiguration"}

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
<td><p><em>AnonymousUserGracePeriod</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>表示在會議中尚未加入已驗證使用者的情況下，匿名 (未驗證的) 使用者可以待在同一會議中的時間長度。例如，如果將這個值設為 15 分鐘，在已驗證的使用者必須加入前，匿名使用者最多可留在會議中 15 分鐘。如果在這段寬限期結束前沒有已驗證的使用者加入，則必須將匿名使用者從會議中移除。此設定同時適用於排程會議及在 Lync 中按一下 [立即開會] 所建立的臨時會議。</p>
<p>您必須以下列格式指定 AnonymousUserGracePeriod：天數.小時數:分鐘數:秒數 (例如 0.00:30:00 表示 30 分鐘)。寬限期可設為介於 0 秒與 1 天之間的任何值，預設值為 90 分鐘 (01:30:00)。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DeactivationGracePeriod</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>會議維持作用中的時間長度上限。您必須以下列格式指定此值：天數.小時數:分鐘數:秒數。例如，若要讓會議持續 60 小時，您可以使用此格式：2.12:00:00 (2 天：12 小時：00 分鐘：00 秒。)</p>
<p>DeactivationGracePeriod 必須介於 8 小時和 365 天 (含) 之間。預設值是 1 天。</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultSubscriptionExpiration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int64</p></td>
<td><p>每次使用者要求目前狀態資訊之類的資料時，就會建立訂閱。要求提出時，使用者 (或更正確地說，使用者的用戶端應用程式) 可以要求訂閱在必須更新前可維持有效的時間長度。如果未發出此類要求，則訂閱會設為由 DefaultSubscriptionExpiration 屬性指定的值。</p>
<p>預設訂閱時間必須以介於 300 秒 (5 分鐘) 與 86400 秒 (24 小時) (含) 之間的整數值來表示。預設值為 28800 秒 (8 小時)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>抑制顯示執行命令時可能引起的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之 User Services 組態設定的唯一識別碼。若要修改全域設定，請使用下列語法：-Identity global。若要修改在網站範圍設定的設定，請使用類似下列的語法：-Identity site:Redmond。若要修改服務層級的設定，請使用類似下列的語法：-Identity service:UserServer:atl-cs-001.litwareinc.com。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>UserServicesSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>MaintenanceTimeOfDay</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>表示一天內定期排程之資料庫維護 (例如清除過時記錄) 進行的時間。這個值必須指定為日期時間值；可以使用 24 小時制 (例如 &quot;14:00&quot;) 或 12 小時制 (例如 &quot;2:00 PM&quot;)。</p>
<p>MaintenanceTimeOfDay 的預設值為 1:00 AM (01:00:00)。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxContacts</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>使用者可擁有的連絡人數目上限；預設值為 250。MaxContacts 屬性代表使用者可擁有之連絡人的絕對數目上限。不過，您可使用 <strong>CsClientPolicy</strong> Cmdlet 限制特定使用者的連絡人數目上限，使其低於 MaxContacts 的值。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxPersonalNotes</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示儲存在使用者之記事歷程記錄中的個人記事數目上限。根據預設，最後 3 筆個人記事會保留在記事歷程記錄中。可保留在歷程記錄中之記事數目上限為 10。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxScheduledMeetingsPerOrganizer</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指定時間內單一使用者可做為召集人之會議的數目上限。預設值為 1000；也就是說，如果使用者已是 1000 場會議的召集人，其排程新會議 (會議編號 1001) 的要求將會失敗。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxSubscriptionExpiration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int64</p></td>
<td><p>每次使用者要求目前狀態資訊之類的資料時，就會建立訂閱。要求提出時，使用者 (或更正確地說，使用者的用戶端應用程式) 可以要求訂閱在必須更新前可維持有效的時間長度。MaxSubscriptionExpiration 屬性代表可授與用戶端的時間長度上限。例如，如果時間上限設為 28800 秒，而用戶端要求的逾時間隔為 86400 秒，則用戶端會獲得下列允許的到期時間上限：28800 秒。</p>
<p>訂閱時間上限必須以介於 300 秒 (5 分鐘) 與 86400 秒 (24 小時) (含) 之間的整數值來表示。預設值為 43200 秒 (12 小時)。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxSubscriptions</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>任一時間內使用者可開啟之 SIP 訂閱對話方塊的數目上限。訂閱對話方塊代表 SIP 資源的要求。</p></td>
</tr>
<tr class="even">
<td><p><em>MinSubscriptionExpiration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int64</p></td>
<td><p>每次使用者要求目前狀態資訊之類的資料時，就會建立訂閱。要求提出時，使用者 (或更正確地說，使用者的用戶端應用程式) 可以要求訂閱在必須更新前可維持有效的時間長度。MinSubscriptionExpiration 屬性代表可授與用戶端的時間長度下限。例如，如果時間下限設為 1200 秒，而用戶端要求的逾時間隔為 200 秒，則用戶端將獲得下列允許的到期時間下限：1200 秒。</p>
<p>訂閱時間下限必須以介於 300 秒 (5 分鐘) 與 86400 秒 (24 小時) (含) 之間的整數值來表示。預設值為 1200 秒 (20 分鐘)。</p></td>
</tr>
<tr class="odd">
<td><p><em>PresenceProviders</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>User Services 組態設定之目前狀態提供者的集合。最好是使用 <strong>New-CsPresenceProvider</strong> Cmdlet 以將目前狀態提供者新增至 User Services 組態設定的集合。</p></td>
</tr>
<tr class="even">
<td><p><em>SubscribeToCollapsedDG</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True (預設值)，即允許用戶端應用程式訂閱目前在連絡人清單中未展開的通訊群組。如此一來用戶端能夠保有群組中每一個成員最即時的目前狀態資訊。如果設為 False，用戶端應用程式將無法訂閱「摺疊的」群組。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.UserServicesSettings 物件。**Set-CsUserServicesConfiguration** Cmdlet 會接受 User Services 設定物件的管線執行個體。

## 傳回類型

**Set-CsUserServicesConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.UserServicesSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[New-CsUserServicesConfiguration](new-csuserservicesconfiguration.md)  
[Remove-CsUserServicesConfiguration](remove-csuserservicesconfiguration.md)

