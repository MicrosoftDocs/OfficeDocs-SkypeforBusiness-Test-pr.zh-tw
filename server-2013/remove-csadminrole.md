---
title: Remove-CsAdminRole
TOCTitle: Remove-CsAdminRole
ms:assetid: f676d3d5-2d4c-4095-a174-9278bc0852df
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413036(v=OCS.15)
ms:contentKeyID: 49292829
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAdminRole

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的角色型存取控制 (RBAC) 角色。RBAC 角色可用於定義使用者所能執行的管理工作，以及指定使用者執行這些工作的範圍。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsAdminRole -Identity <String> <COMMON PARAMETERS>

    Remove-CsAdminRole -Sid <String> <COMMON PARAMETERS>

    Remove-CsAdminRole [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除 Identity 為 RedmondHelpDesk 的 RBAC 角色。

    Remove-CsAdminRole -Identity "RedmondHelpDesk"

## 範例 2

範例 2 會刪除 Identity 中的某處包含字串值 "Redmond" 的所有 RBAC 角色。

    Remove-CsAdminRole -Filter "*Redmond*"

## 範例 3

在範例 3 中，命令會刪除已建立來在組織中使用的所有自訂 RBAC 角色。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsAdminRole** Cmdlet，以傳回 RBAC 角色的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 IsStandardRole 屬性等於 False 的角色。根據預設，所有符合該準則的角色都是自訂角色。接著將這些自訂角色管線傳送到 **Remove-CsAdminRole** Cmdlet 加以刪除。

    Get-CsAdminRole | Where-Object {$_.IsStandardRole -eq $False} | Remove-CsAdminRole

## 詳細描述

RBAC 可讓系統管理員委派控制 Lync Server 中的特定管理工作。例如，您可以不授予組織服務台完整的系統管理員權限，而是給予這些員工非常特定的權限：僅限管理使用者帳戶的權限、僅限管理 Enterprise Voice 元件的權限，以及僅限管理封存和封存伺服器的權限。此外，這些權限可限制在以下範圍：可提供某些人管理 Enterprise Voice 的權限，但僅限於 Redmond 網站；也可提供其他人管理使用者的權限，但僅限於那些帳戶屬於 Finance 組織單位 (OU) 的使用者。

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

上述清單中的 Cmdlet，是系統允許被指派某假設 RBAC 角色的使用者在遠端 Windows PowerShell 命令列介面工作階段中執行的唯一 Cmdlet。如果使用者嘗試執行 **Disable-CsUser** Cmdlet，該命令將會失敗，因為指派假設角色的使用者並不具有執行 **Disable-CsUser** Cmdlet 的權限。這也適用於 Lync Server 控制台。例如，封存系統管理員無法使用 Lync Server 控制台來停用使用者，因為 Lync Server 控制台遵守 RBAC 角色 (執行 Lync Server 控制台中的命令時，其實是在呼叫 Windows PowerShell Cmdlet)。如果不允許您執行 **Disable-CsUser** Cmdlet，則無論您是直接從 Windows PowerShell 執行該 Cmdlet，還是在 Lync Server 控制台內間接執行 Cmdlet，該命令都會失敗。

請注意，RBAC 僅套用至遠端管理。如果您登入了執行 Lync Server 的電腦，而且開啟 Lync Server 管理命令介面，則系統不會強制執行 RBAC 角色。而是主要透過安全性群組 RTCUniversalServerAdmins、RTCUniversalUserAdmins 和 RTCUniversalReadOnlyAdmins 來強制執行安全性。

當您安裝 Lync Server 時，安裝程式會建立幾個內建的 RBAC 角色，而這些角色會涵蓋常見的管理範圍，例如語音管理、使用者管理、回應群組管理等。這些內建的角色無法以下列任何方式進行修改：您無法新增或移除角色的 Cmdlet，且您無法刪除角色 (嘗試刪除內建角色將會造成錯誤訊息出現)。但是，您可以使用內建角色，來建立自訂的 RBAC 角色。接著，可藉由變更管理範圍修改這些自訂的角色；例如，您可以使用特定的 Active Directory OU，將角色限制在管理使用者帳戶。

您可以利用 **Remove-CsAdminRole** Cmdlet 刪除任何您建立的自訂角色。請注意，**Remove-CsAdminRole** 將不會刪除對應至自訂角色的 Active Directory 安全性群組，也不會移除已指派給該群組的任何成員。反之，此 Cmdlet 只會確保這個自訂角色無法用來委派 Lync Server 的控制權。

當您刪除 RBAC 角色時，Windows PowerShell 的回應方式是詢問您是否確定要刪除此角色；如果您未回應此提示 (或者未回應「是」)，則將不會刪除此角色。若要避免出現這些確認提示，請使用 Confirm 參數並將參數值設為 $False：

Remove-CsAdminRole RedmondAdministrators –Confirm:$False

誰可以執行這個 Cmdlet：根據預設，下列群組的成員經過授權，可在本機執行 Remove-CsAdminRole Cmdlet：RTCUniversalServerAdmins。執行 Windows PowerShell 提示字元提供的下列命令，即可傳回指派給此 Cmdlet (包括您自行建立的任何自訂 RBAC 角色) 的所有 RBAC 角色清單：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsAdminRole"}

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
<td><p>System.String</p></td>
<td><p>要刪除之 RBAC 角色的唯一識別碼。RBAC 角色的 Identity 必須和與該角色相關聯之 Active Directory 萬用安全性群組的 SamAccountName 相同。例如，Help Desk 角色具有等於 CsHelpDesk 的 Identity；CsHelpDesk 也是與該角色相關聯之 Active Directory 萬用安全性群組的 SamAccountName。</p></td>
</tr>
<tr class="even">
<td><p><em>Sid</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>讓您能夠使用安全性識別碼 (SID) 來指定要刪除的 RBAC 角色。在建立 RBAC 角色時由 Lync Server 指派的 SID 如下所示：S-1-5-21-1573807623-1597889489-1765977225-1145。可以使用 <strong>Get-CsAdminRole</strong> Cmdlet 擷取指定 RBAC 角色的 SID。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>讓您可以略過當您試圖刪除 RBAC 角色時出現的確認提示。若要略過提示，請包含 Confirm 參數並將參數值設為 $False：</p>
<p>Remove-CsAdminRole RedmondAdministrators –Confirm:$False</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>讓您能夠使用萬用字元來指定要移除的自訂 RBAC 角色。例如，若要移除 Identity 中包含字串值 &quot;Redmond&quot; 的所有自訂角色，您可以使用下列語法：-Filter &quot;*Redmond*&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Remove-CsAdminRole** Cmdlet 接受管線傳送的使用者物件輸入。

## 傳回類型

**Remove-CsAdminRole** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.Roles.Role 物件執行個體。

