---
title: Get-CsConferencingConfiguration
TOCTitle: Get-CsConferencingConfiguration
ms:assetid: db4ab3bc-071c-4f73-a3a0-62dc8aed48a1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398965(v=OCS.15)
ms:contentKeyID: 49292513
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferencingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織的會議組態設定集合。會議設定可指定會議內容與講義的大小上限、內容寬限期 (即內容刪除前所能儲存的時間)，以及支援之用戶端內部與外部下載的 URL 等事項。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsConferencingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsConferencingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回組織目前使用之所有會議組態設定的資訊。作法是呼叫不含任何參數的 **Get-CsConferencingConfiguration** Cmdlet。

    Get-CsConferencingConfiguration

## 範例 2

範例 2 會傳回 Redmond 網站 (-Identity site:Redmond) 的會議組態資訊。由於 Identity 必須是唯一的，因此這個命令一律只會傳回一個會議組態設定集合。

    Get-CsConferencingConfiguration -Identity site:Redmond

## 範例 3

範例 3 所示的命令會傳回已在網站範圍套用之所有會議組態設定的資訊。為達成此目的，會呼叫 **Get-CsConferencingConfiguration** Cmdlet 搭配 Filter 參數。篩選值 "site:\*" 會確保只傳回 Identity 開頭為 "site:" 字串值的設定。

    Get-CsConferencingConfiguration -Filter "site:*"

## 範例 4

範例 4 會傳回組織未設為 Litwareinc 之所有會議組態設定的資訊。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsConferencingConfiguration** Cmdlet，以傳回組織使用之所有會議組態設定的集合。然後將產生的集合管線傳送到 **Where-Object** Cmdlet，這會只選取 Organization 屬性不等於 Litwareinc 的設定。

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Litwareinc"}

## 範例 5

範例 5 只會傳回內容儲存空間上限大於 100 MB 之會議組態設定的資訊。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsConferencingConfiguration** Cmdlet，以傳回所有會議組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出內容儲存空間大於 100 MB 的設定。

    Get-CsConferencingConfiguration | Where-Object {$_.MaxContentStorageMB -gt 100}

## 詳細描述

對於會議而言，管理與系統管理會分別以兩組 Cmdlet 進行。如果您想要管理使用者能做與不能做的事情 (例如，使用者是否可以邀請匿名參與者加入會議、使用者是否可以在會議內進行應用程式共用，或使用者是否可以在會議內傳輸檔案)，則需使用 **CsConferencingPolicy** Cmdlet。

除了使用者活動之外，系統管理員還需要管理 Lync Server Web 會議服務。例如，系統管理員需要能夠執行一些動作，例如指定配置給單一會議的內容儲存量上限，以及指定自動刪除該會議內容之前的寬限期。他們也需要能夠指定諸如應用程式共用及檔案傳輸這類活動使用的連接埠。

後面的活動是使用 **CsConferencingConfiguration** Cmdlet 來管理的。這些 Cmdlet 可讓您管理實際伺服器本身。**CsConferencingConfiguration** Cmdlet (可以套用至全域、網站及服務範圍) 雖然不能用來指定使用者是否可在會議期間共用應用程式，但是可以在允許應用程式共用時，用來指出該活動應該使用哪些連接埠。同樣地，Cmdlet 也可讓您指定一些事項，例如儲存限制和期限，以及可供使用者用來取得會議說明及資源的內部與外部 URL 指標。

**Get-CsConferencingConfiguration** Cmdlet 可讓系統管理員傳回目前用於組織之所有會議組態設定的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsConferencingConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferencingConfiguration"}

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
<td><p>可讓您在指定要傳回之會議組態設定的 Identity 時使用萬用字元。例如，此語法會傳回網站範圍設定的所有設定：-Filter &quot;site:*&quot;。此語法會傳回所有在服務範圍內所做的設定：-Filter &quot;service:*&quot;。</p>
<p>請注意，您不能在同一個命令中同時使用 Identity 和 Filter 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之會議組態設定集合的唯一識別碼。若要擷取全域設定，請使用下列語法：-Identity global。若要擷取在網站範圍內所做的設定，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要擷取在服務範圍內所做的設定，請使用類似下列的語法：-Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>如果沒有加入此參數，<strong>Get-CsConferencingConfiguration</strong> Cmdlet 會傳回組織目前使用的所有會議組態設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取會議組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsConferencingConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsConferencingConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Remove-CsConferencingConfiguration](remove-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

