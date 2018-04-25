---
title: Get-CsAdminRole
TOCTitle: Get-CsAdminRole
ms:assetid: ea15ee37-f7a1-4e67-afe8-08e63e8ca765
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399050(v=OCS.15)
ms:contentKeyID: 49292693
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdminRole

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之角色型存取控制 (RBAC) 角色的資訊。RBAC 角色可用於定義使用者所能執行的管理工作，以及指定使用者執行這些工作的範圍。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAdminRole [-Identity <String>] <COMMON PARAMETERS>

    Get-CsAdminRole [-Sid <String>] <COMMON PARAMETERS>

    Get-CsAdminRole [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織用之所有 RBAC 角色的資訊。作法是呼叫不含任何參數的 **Get-CsAdminRole** Cmdlet。

    Get-CsAdminRole

## 範例 2

於範例 2 中，會傳回單一 RBAC 角色：Identity 為 CsHelpDesk 的角色。

    Get-CsAdminRole -Identity "CsHelpDesk"

## 範例 3

範例 3 會傳回 Identity (例如，CsVoiceAdministrator、RedmondVoiceAdministrators) 包含字串值 "Voice" 的所有 RBAC 角色。為達此目的，會呼叫 **Get-CsAdminRole** 搭配 Filter 參數 (篩選值 "\*Voice\*" 可將傳回的資料限制為在 Identity 包含字串值 "Voice" 的 RBAC 角色)。

    Get-CsAdminRole -Filter "*Voice*"

## 範例 4

範例 4 會傳回建立供組織使用的所有自訂 RBAC 角色。為了執行此工作，命令會先使用 **Get-CsAdminRole** Cmdlet，以傳回目前使用之所有 RBAC 角色的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 IsStandardRole 屬性等於 False 的角色。根據定義，所有符合該準則的角色都是自訂的 RBAC 角色。

    Get-CsAdminRole | Where-Object {$_.IsStandardRole -eq $False}

## 範例 5

範例 5 所示的命令會傳回所有包含 **Set-CsUser** Cmdlet 的 RBAC 角色。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsAdminRole** Cmdlet，以傳回組織中所有 RBAC 角色的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 Cmdlets 屬性包含字串值 "Set-CsUser\\b" 的角色 (\\b 為字元界線標記，表示 "Set-CsUser" 代表整個字串值)。

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsUser\b"}

## 範例 6

範例 6 會傳回 UserScopes 屬性中包含指定 OU (ou=Redmond, dc=litwareinc, dc=com) 之所有 RBAC 角色的資訊。為了執行此工作，命令會先呼叫 **Get-CsAdminRole** Cmdlet，以傳回目前設定使用之所有 RBAC 角色的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以選取 UserScopes 屬性中包含 "OU:ou=Redmond,dc=litwareinc,dc=com" 字串值的所有角色。

    Get-CsAdminRole | Where-Object {$_.UserScopes -match "OU: ou=Redmond,dc=litwareinc,dc=com"}

## 範例 7

範例 7 所示的命令會傳回 CsVoiceAdministrator 角色所含之所有 Cmdlet 的清單。為達成此目的，命令會先使用 **Get-CsAdminRole** Cmdlet，以傳回所有屬性與 CsVoiceAdministrator 的屬性值。然後將此資訊管線傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 參數來顯示 Cmdlets 屬性所含的所有項目。

    Get-CsAdminRole -Identity "CsVoiceAdministrator" | Select-Object -ExpandProperty Cmdlets

## 詳細描述

角色型存取控制 (RBAC) 可讓系統管理員委派控制 Lync Server 中的特定管理工作。例如，您可以不要授與組織中的服務台完整的系統管理員權限，而是給予這些員工非常特定的權限，例如僅能管理使用者帳戶的權限；僅能管理 Enterprise Voice 元件的權限；以及僅能管理封存及 封存伺服器 的權限。此外，這些權利可限制在以下範圍：可提供某些人管理 Enterprise Voice 的權限，但僅限於 Redmond 網站；也可提供其他人管理使用者的權限，但僅限於那些帳戶屬於 Finance 組織單位 (OU) 的使用者。

RBAC 的 Lync Server 實作根據以下兩個重要元素：Active Directory 安全性群組與 Windows PowerShell Cmdlet。當您安裝 Lync Server 時，系統會為您建立一些萬用安全性群組，例如 CsAdministrator、CsArchivingAdministrator 及 CsViewOnlyAdministrator。這些萬用安全性群組具有一個含 RBAC 角色的一對一對應；這表示任何位於 CsArchivingAdministrator 安全性群組中的使用者具有所有授與 CsArchivingAdministrator RBAC 角色的權限。授與 RBAC 角色的權限也是根據指派給該角色的 Cmdlet 而定 (可將 Cmdlet 指派給多個 RBAC 角色)。例如，假設已對某個角色指派下列 Cmdlet：

Get-ArchivingPolicy

Grant-ArchivingPolicy

New-ArchivingPolicy

Remove-ArchivingPolicy

Set-ArchivingPolicy

Get-ArchivingConfiguration

New-ArchivingConfiguration

Remove-ArchivingConfiguration

Set-ArchivingConfiguration

Get-CsUser

Export-CsArchivingData

Get-CsComputer

Get-CsPool

Get-CsService

Get-CsSite

上述清單代表唯一的 Cmdlet，此 Cmdlet 允許在遠端 Windows PowerShell 命令列介面工作階段中執行指派假設 RBAC 角色的使用者。如果使用者嘗試執行 **Disable-CsUser** Cmdlet，該命令將會失敗；這是因為指派假設角色的使用者不具有執行 **Disable-CsUser** Cmdlet 的權限。這也適用於 Lync Server 控制台。例如，封存系統管理員無法使用 Lync Server 控制台來停用使用者，因為 Lync Server 控制台遵守 RBAC 角色 (任何時候當您在 Lync Server 控制台中執行命令時，其實是在呼叫 Windows PowerShell Cmdlet)。如果無法執行 **Disable-CsUser** Cmdlet，則無論是從 Windows PowerShell 的遠端工作階段直接執行此 Cmdlet，或是從 Lync Server 控制台間接執行此 Cmdlet，命令都會失敗。

請注意，RBAC 僅套用至遠端管理。如果您登入執行 Lync Server 的電腦，並開啟 Lync Server 管理命令介面，將不會強制執行 RBAC 角色。而是主要透過安全性群組 RTCUniversalServerAdmins、RTCUniversalUserAdmins 和 RTCUniversalReadOnlyAdmins 來強制執行安全性。

當您安裝 Lync Server 時，安裝程式會建立數個內建的 RBAC 角色。這些角色涵蓋常見的管理範圍，例如語音管理、使用者管理和回應群組管理。這些內建的角色無法以下列任何方式進行修改：您無法在角色中新增或移除 Cmdlet，且您無法刪除這些角色。(嘗試刪除內建角色將會造成錯誤訊息出現)。但是，您可以使用內建角色，來建立自訂的 RBAC 角色。接著，您可藉由變更管理範圍來修改這些自訂的角色。例如，您可以使用特定的 Active Directory OU，將角色限制在管理使用者帳戶。

**Get-CsAdminRole** Cmdlet 會傳回在組織中可以使用的所有 RBAC 相關資訊。

誰可以執行這個 Cmdlet：根據預設，下列群組的成員經過授權，可在本機執行 **Get-CsAdminRole** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。執行 Windows PowerShell 提示字元提供的下列命令，即可傳回指派給此 Cmdlet (包括您自行建立的任何自訂 RBAC 角色) 的所有 RBAC 角色清單：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdminRole\\b"}

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
<td><p>可讓您使用萬用字元來指定要傳回的 RBAC 角色。例如，若要傳回 Identity 中包含字串值 &quot;Redmond&quot; 的所有角色，請使用下列語法：-Filter &quot;*Redmond*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要傳回之 RBAC 角色的唯一識別碼。RBAC 角色的 Identity 必須和與該角色相關聯之 Active Directory 萬用安全性群組的 SamAccountName 相同。例如，Help Desk 角色具有等於 CsHelpDesk 的 Identity；CsHelpDesk 也是與該角色相關聯之 Active Directory 萬用安全性群組的 SamAccountName。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取 RBAC 資料，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Sid</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您使用安全性識別碼 (SID) 來指定要擷取的 RBAC 角色。在建立 RBAC 角色時由 Lync Server 指派的 SID 如下所示：S-1-5-21-1573807623-1597889489-1765977225-1145。</p>
<p>這個相同的 SID 也可在對應的 Active Directory 安全性群組上找到。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsAdminRole** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Roles.Role 物件的執行個體。

