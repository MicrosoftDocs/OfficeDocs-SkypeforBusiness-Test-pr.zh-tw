---
title: New-CsUserServicesConfiguration
TOCTitle: New-CsUserServicesConfiguration
ms:assetid: bdcb11b5-b8bf-4d63-a8a5-11f2b43686dd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412926(v=OCS.15)
ms:contentKeyID: 49292156
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsUserServicesConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的 使用者服務組態設定集合。User Services 服務可維護目前狀態資訊及管理會議。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsUserServicesConfiguration -Identity <XdsIdentity> [-AnonymousUserGracePeriod <TimeSpan>] [-Confirm [<SwitchParameter>]] [-DeactivationGracePeriod <TimeSpan>] [-DefaultSubscriptionExpiration <Int64>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaintenanceTimeOfDay <DateTime>] [-MaxContacts <UInt16>] [-MaxPersonalNotes <UInt32>] [-MaxScheduledMeetingsPerOrganizer <UInt32>] [-MaxSubscriptionExpiration <Int64>] [-MaxSubscriptions <UInt16>] [-MinSubscriptionExpiration <Int64>] [-PresenceProviders <PSListModifier>] [-SubscribeToCollapsedDG <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會為 Redmond 網站 (-Identity site:Redmond) 建立新的 User Services 組態設定集合。除了指定 Identity 外，這個命令也會設定連絡人數目上限 (-MaxContacts 500) 以及維護發生於一天中的什麼時間 (-MaintenanceTimeOfDay "11:00 PM")。請注意，如果 Redmond 網站的 User Services 設定已經完成，這個命令就會失敗。這是因為您有每個網站一個設定集合的限制。

    New-CsUserServicesConfiguration -Identity site:Redmond -MaxContacts 500 -MaintenanceTimeOfDay "11:00 PM"

## 範例 2

範例 2 也會為 Redmond 網站建立新的 User Services 組態設定集合。但在此範例中，集合一開始只會建立於記憶體中，且之後只會套用到 Redmond 網站。為達成此目的，範例中的第一個命令會使用 **New-CsUserServicesConfiguration** Cmdlet 搭配 InMemory 參數，以建立只存在記憶體中的新集合 (Identity 為 site:Redmond)。因為此集合只存在記憶體中，所以 User Services 物件必須儲存於變數中。在此範例中，這是名為 $x 的變數。

建立虛擬集合後，會使用命令 2 和 3 來修改 MaxContacts 和 MaintenanceTimeOfDay 屬性的值。然後，範例中的最後一個命令會使用 **Set-CsUserServicesConfiguration** Cmdlet，將這些虛擬設定轉換為實際的 使用者服務組態設定集合，並套用到 Redmond 網站。最後這一個步驟很重要：如果沒有呼叫 **Set-CsUserServicesConfiguration** Cmdlet，就不會將任何設定套用到 Redmond 網站，那麼只要您終止 Windows PowerShell 工作階段或刪除變數 $x，您的虛擬設定便會立即消失。

    $x = New-CsUserServicesConfiguration -Identity site:Redmond -InMemory
    $x.MaxContacts = 500 
    $x.MaintenanceTimeOfDay = "11:00 PM"
    Set-CsUserServicesConfiguration -Instance $x

## 詳細描述

Lync Server 依賴 User Services 協助維護使用者的目前狀態資訊，以及管理會議。 **CsUserServicesConfiguration** Cmdlet 依序用於管理全域、網站和服務範圍的 User Services 設定 (請注意，可主控 User Services 組態設定的唯一服務為 User Services 服務本身)。這些設定有助於決定使用者可擁有的連絡人數目、使用者可在任何一個時間中排程的會議數，以及所指定的會議可保持為作用中的時間長度等作業。

**New-CsUserServicesConfiguration** Cmdlet 可讓系統管理員在網站或服務範圍建立新的 User Services 組態設定集合。(不可在全域範圍建立新集合)。請注意，任何特定網站或服務最多只能有一個 User Services 組態設定集合。舉例來說，如果您嘗試為 Redmond 網站建立設定，而這個網站已經裝載 User Services 組態設定集合，您的命令就會失敗。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsUserServicesConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsUserServicesConfiguration"}

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
<td><p>要建立的 User Services 組態設定的唯一識別碼。若要在網站範圍建立設定，請使用類似下列的語法：-Identity site:Redmond。若要在服務層級建立設定，請使用下列語法：-Identity service:UserServer:atl-cs-001.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>AnonymousUserGracePeriod</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>表示在會議中尚未加入已驗證使用者的情況下，匿名 (未驗證的) 使用者可以待在同一會議中的時間長度。例如，如果將這個值設為 15 分鐘，在已驗證的使用者必須加入前，匿名使用者最多可留在會議中 15 分鐘。如果在這段寬限期結束前沒有已驗證的使用者加入，則必須將匿名使用者從會議中移除。此設定同時適用於排程會議及在 Microsoft Lync 中按一下 [立即開會] 所建立的臨時會議。</p>
<p>您必須以下列格式指定 AnonymousUserGracePeriod：天數.小時數:分鐘數:秒數 (例如 0.00:30:00 表示 30 分鐘)。寬限期必須設為介於 0 秒和 1 天之間的任何值，預設值是 90 分鐘 (01:30:00)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DeactivationGracePeriod</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>會議可持續使用的時間長度上限。此值必須使用下列格式：天數.小時數:分鐘數:秒數。例如，若要使會議持續 60 小時，要使用此格式：2.12:00:00 (2 天. 12 小時: 00 分鐘: 00 秒。)</p>
<p>DeactivationGracePeriod 必須介於 8 小時 (含) 和 365 天 (含) 之間。預設值為 1 天 (1.00:00:00)。</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultSubscriptionExpiration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int64</p></td>
<td><p>任何時候，只要使用者要求資料，如目前狀態資訊，就會建立訂閱。在建立要求時，使用者 (或者更正確的說，是使用者的用戶端應用程式) 可以要求此訂閱在必須續訂之前，保持有效的時間長度。如果沒有發出這類要求，則會將訂閱設為 DefaultSubscriptionExpiration 屬性所指定的值。</p>
<p>預設訂閱時間必須以介於 300 秒 (5 分鐘) 與 86400 秒 (24 小時) (含) 之間的整數值來表示。預設值是 28800 秒 (8 小時)。</p></td>
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
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>MaintenanceTimeOfDay</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>指定定期資料庫維護 (如清除過時的記錄) 該發生在一天當中的什麼時候。這個值必須指定為日期時間值。您可以使用 24 小時制 (如 &quot;14:00&quot;) 或 12 小時制 (如 &quot;2:00 PM&quot;)。</p>
<p>MaintenanceTimeOfDay 的預設值是 1:00 AM (01:00:00)。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxContacts</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>使用者可擁有的連絡人數目上限；預設值為 250。MaxContacts 屬性代表使用者可擁有之連絡人的絕對數目上限。不過，您可使用 CsClientPolicy Cmdlet 限制特定使用者的連絡人數目上限，使其低於 MaxContacts 的值。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxPersonalNotes</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指出儲存在使用者的記事歷程記錄中的個人記事數目上限。根據預設，在記事歷程記錄中會保留最新的 3 個個人記事。在歷程記錄中可保留的記事數目上限為 10 個。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxScheduledMeetingsPerOrganizer</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>在特定時間單一使用者可做為會議召集人的會議數目上限。預設值為 1000。也就是說，如果使用者已是 1000 場會議的召集人，其嘗試排程新會議 (會議編號 1001) 時將會失敗。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxSubscriptionExpiration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int64</p></td>
<td><p>任何時候，只要使用者要求資料，如目前狀態資訊，就會建立訂閱。在建立要求時，使用者 (或者更正確的說，是使用者的用戶端應用程式) 可以要求此訂閱在必須續訂之前，保持有效的時間長度。MaxSubscriptionExpiration 屬性表示可授與用戶端的時間長度上限。例如，如果時間上限設為 28800 秒，而用戶端要求 86400 秒的逾時間隔，則用戶端將獲得最高允許的到期時間：28800 秒。</p>
<p>訂閱時間上限必須以介於 300 秒 (5 分鐘) 與 86400 秒 (24 小時) (含) 之間的整數值來表示。預設值是 43200 秒 (12 小時)。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxSubscriptions</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>使用者隨時可開啟的 SIP 訂閱對話方塊數目上限。一個訂閱對話方塊代表一個對 SIP 資源的要求。預設值為 200。</p></td>
</tr>
<tr class="even">
<td><p><em>MinSubscriptionExpiration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int64</p></td>
<td><p>任何時候，只要使用者要求資料，如目前狀態資訊，就會建立訂閱。在建立要求時，使用者 (或者更正確的說，是使用者的用戶端應用程式) 可以要求此訂閱在必須續訂之前，保持有效的時間長度。MinSubscriptionExpiration 屬性表示可授與用戶端的時間長度下限。例如，如果時間下限設為 1200 秒，而用戶端要求 200 秒的逾時間隔，則用戶端將獲得最低允許的到期時間：1200 秒。</p>
<p>訂閱時間下限必須以介於 300 秒 (5 分鐘) 與 86400 秒 (24 小時) (含) 之間的整數值來表示。預設值是 1200 秒 (20 分鐘)。</p></td>
</tr>
<tr class="odd">
<td><p><em>PresenceProviders</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>新的 User Services 組態設定之目前狀態提供者集合。最好是使用 <strong>New-CsPresenceProvider</strong> Cmdlet，將目前狀態提供者新增到 User Services 組態設定集合。</p></td>
</tr>
<tr class="even">
<td><p><em>SubscribeToCollapsedDG</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True (預設值)，即允許用戶端應用程式訂閱目前在連絡人清單中未展開的通訊群組。如此一來用戶端能夠保有群組中每一個成員最即時的目前狀態資訊。如果設為 False，用戶端應用程式將不能夠訂閱「摺疊」的群組。</p></td>
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

無。 **New-CsUserServicesConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsUserServicesConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.UserServicesSettings 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[Remove-CsUserServicesConfiguration](remove-csuserservicesconfiguration.md)  
[Set-CsUserServicesConfiguration](set-csuserservicesconfiguration.md)

