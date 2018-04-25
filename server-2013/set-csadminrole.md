---
title: Set-CsAdminRole
TOCTitle: Set-CsAdminRole
ms:assetid: ec927ce6-a37b-4876-a6df-a347404f4e84
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399066(v=OCS.15)
ms:contentKeyID: 49292724
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAdminRole

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的角色型存取控制 (RBAC) 角色。RBAC 角色可用於定義使用者所能執行的管理工作，以及指定使用者執行這些工作的範圍。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsAdminRole -Identity <String> [-Cmdlets <PSListModifier>] [-ConfigScopes <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-ScriptModules <PSListModifier>] [-UserScopes <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會新增 OU (Portland) 到 RBAC 角色 RedmondVoiceAdministrators 的 UserScopes 屬性中。為達此目的，命令會加入 UserScopes 屬性和下列參數值：@{Add="OU:ou=Portland,dc=litwareinc,dc=com"}。此語法會將辨別名稱為 "ou=Portland,dc=litwareinc,dc=com" 的 OU 加入 UserScopes 屬性中既有的 OU。

    Set-CsAdminRole -Identity "RedmondVoiceAdministrators" -UserScopes @{Add="OU:ou=Portland,dc=litwareinc,dc=com"}

## 範例 2

範例 2 所示的命令會從 RBAC 角色 RedmondVoiceAdministrators 中移除 Portland OU。為達此目的，命令會加入 UserScopes 屬性和下列參數值：@{Remove="OU:ou=Portland,dc=litwareinc,dc=com"}。此語法會從 UserScopes 屬性中既有的 OU 集合刪除辨別名稱為 "ou=Portland,dc=litwareinc,dc=com" 的 OU。

    Set-CsAdminRole -Identity "RedmondVoiceAdministrators" -UserScopes @{Remove="OU:ou=Portland,dc=litwareinc,dc=com"}

## 範例 3

範例 3 會將新網站 (即 SiteId Redmond 網站) 加入 RBAC 角色 RedmondVoiceAdministrators 的 ConfigScopes 屬性。為達此目的，命令會加入 ConfigScopes 屬性和下列參數值：@{Add="OU:ou=Portland,dc=litwareinc,dc=com"}。此語法會將 Redmond 網站加入 ConfigScopes 屬性中的既有項目。

    Set-CsAdminRole -Identity "RedmondVoiceAdministrators" -ConfigScopes @{Add="site:Redmond"}

## 範例 4

範例 4 所示的命令會從 RBAC 角色 RedmondVoiceAdministrators 中移除 Redmond 網站。為達此目的，命令會加入 ConfigScopes 屬性和下列參數值：@{Remove="site:Redmond"}。此參數會從 ConfigScopes 屬性中的現有項目集合刪除 Redmond 網站。請注意，如果 Redmond 網站是 ConfigScopes 屬性中的唯一網站，命令會失敗。如果您只要移除 ConfigScopes 屬性中的網站，應使用與此類似的命令，此類命令會以 Global 屬性取代 ConfigScopes 中的所有項目：

Set-CsAdminRole -Identity "RedmondVoiceAdministrators" -ConfigScopes @{Replace="Global"}

    Set-CsAdminRole -Identity "RedmondVoiceAdministrators" -ConfigScopes @{Remove="siteRedmond"}

## 詳細描述

RBAC 可讓系統管理員委派控制 Lync Server 中的特定管理工作。例如，您可以不授予組織服務台完整的系統管理員權限，而是給予這些員工非常特定的權限：只管理使用者帳戶的權限；只管理 Enterprise Voice 元件的權限；只管理封存和 封存伺服器的權限。此外，這些權利可限制在以下範圍：可提供某些人管理 Enterprise Voice 的權限，但僅限於 Redmond 網站；也可提供其他人管理使用者的權限，但僅限於那些帳戶屬於 Finance 組織單位 (OU) 的使用者。

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

上述清單僅代表 Cmdlet，該 Cmdlet 允許在遠端 Windows PowerShell 命令列介面工作階段中執行指派某假設 RBAC 角色的使用者。如果使用者嘗試執行 **Disable-CsUser** Cmdlet，該命令將會失敗；這是因為指派假設角色的使用者並不具有執行 **Disable-CsUser** Cmdlet 的權限。這也適用於 Lync Server 控制台。例如，封存系統管理員無法使用 Lync Server 控制台來停用使用者，因為 Lync Server 控制台遵守 RBAC 角色 (執行 Lync Server 控制台中的命令時，其實是在呼叫 Windows PowerShell Cmdlet)。若您並未獲准執行 **Disable-CsUser** Cmdlet，則無論您是從 Windows PowerShell 直接執行該 Cmdlet，或是從 Lync Server 控制台內間接執行 Cmdlet，該命令都會失敗。

請注意，RBAC 僅套用至遠端管理。如果您登入執行 Lync Server 的電腦，並開啟 Lync Server 管理命令介面，將不會強制執行 RBAC 角色。而是主要透過安全性群組 RTCUniversalServerAdmins、RTCUniversalUserAdmins 和 RTCUniversalReadOnlyAdmins 來強制執行安全性。

當您安裝 Lync Server 時，安裝程式會建立幾個內建的 RBAC 角色，而這些角色會涵蓋常見的管理範圍，例如語音管理、使用者管理、回應群組管理等。這些內建的角色無法以下列任何方式進行修改：您無法新增或移除角色的 Cmdlet，且您無法刪除角色 (嘗試刪除內建角色將會造成錯誤訊息出現)。但是，您可以使用內建角色，來建立自訂的 RBAC 角色。接著，可藉由變更管理範圍修改這些自訂的角色；例如，您可以在特定 Active Directory OU 中，將角色限制在管理使用者帳戶。

任何您所建立的自訂角色都必須以現有的 RBAC 角色為範本依據。 例如，若要建立電話撥入式會議管理員角色，您必須有效地複製現有的 RBAC 角色 (例如，可能會以現有的語音管理員角色來做為電話撥入式會議管理員角色角色的依據)。在建立自訂角色之後，即可使用 **Set-CsAdminRole** Cmdlet 修改新角的屬性。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsAdminRole cmdlet**：RTCUniversalServerAdmins。若要傳回已指派此 Cmdlet 的所有 RBAC 角色的清單 (包括您自行建立的任何自訂 RBAC 角色)，請從 Windows PowerShell 命令提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAdminRole"}

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
<td><p>要修改之 RBAC 角色的唯一識別碼。RBAC 角色的 Identity 必須和與該角色相關聯之 Active Directory 萬用安全性群組的 SamAccountName 相同。例如，Help Desk 角色具有等於 CsHelpDesk 的 Identity；CsHelpDesk 也是與該角色相關聯之 Active Directory 萬用安全性群組的 SamAccountName。</p></td>
</tr>
<tr class="even">
<td><p><em>Cmdlets</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>可讓您指定擁有 RBAC 角色之使用者可用的 Cmdlet。例如，若只要提供一個 Cmdlet ( <strong>Export-CsArchivingData</strong> Cmdlet) 的存取權，請使用類似下列的語法：</p>
<p>-Cmdlets &quot;Export-CsArchivingData&quot;</p>
<p>上述語法以單一項目 Export-CsArchivingData 取代目前儲存在 Cmdlets 屬性中的所有項目。如果您想將 <strong>Export-CsArchivingData</strong> Cmdlet 新增至該屬性中已儲存的 Cmdlet，請改用下列語法：</p>
<p>-Cmdlets @{Add=&quot;Export-CsArchivingData&quot;}</p>
<p>您可以透過以逗號分隔的 Cmdlet 名稱來新增多個 Cmdlet：</p>
<p>-Cmdlets @{Add=&quot;Export-CsArchivingData&quot;,&quot;Invoke-CsArchivingDatabasePurge&quot;}</p>
<p>若要從角色移除 Cmdlet，請使用下列語法：</p>
<p>-Cmdlets @{Remove=&quot;Export-CsArchivingData&quot;}</p></td>
</tr>
<tr class="odd">
<td><p><em>ConfigScopes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>限制 Cmdlet 在指定網站內對於組態設定的範圍。若要將 Cmdlet 範圍限制在單一網站，請使用類似下列的語法：-ConfigScopes site:Redmond。您可以使用以逗號分隔的清單來指定多個網站：-ConfigScopes &quot;site:Redmond，&quot;site:Dublin&quot;。您也可以將 ConfigScopes 屬性設定為 &quot;global&quot;。</p>
<p>指派值給 ConfigScopes 參數時，您必須使用 &quot;site:&quot;首碼後面要加上網站之 SiteId 屬性的值；SiteId 不一定與網站的 Identity 或網站的 DisplayName 有相同的值。若要決定指定網站的 SiteId，您可以使用類似下列的命令：</p>
<p>Get-CsSite &quot;Redmond&quot; | Select-Object SiteId</p>
<p>您必須為 ConfigScopes 或 UserScopes 屬性 (或兩者) 指定值。</p></td>
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
<td><p><em>ScriptModules</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>可讓您指定 Windows PowerShell 指令碼中的功能，以供擁有新 RBAC 角色的使用者使用。例如，下列語法提供 UpdateDatabase.ps1 指令碼中 Reset 函式的存取權：</p>
<p>-ScriptCmdlets &quot;UpdateDatabase.ps1:Reset&quot;</p>
<p>上述命令以 Reset 函式和 UpdateDatabase.ps1 指令碼取代目前儲存在 ScriptCmdlets 屬性的任何指令碼。若要將此指令碼/函式新增至目前儲存在 ScriptCmdlets 屬性的項目，請使用下列語法：</p>
<p>-ScriptCmdlets @{Add=&quot;UpdateDatabase.ps1:Reset&quot;}</p>
<p>若要移除指令碼/函式，請使用下列語法：</p>
<p>-ScriptCmdlets @{Add=&quot;UpdateDatabase.ps1:Reset&quot;}</p>
<p>您可以使用下列語法，刪除指派給角色的所有 ScriptCmdlets：</p>
<p>-ScriptCmdlets $Null</p></td>
</tr>
<tr class="odd">
<td><p><em>UserScopes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>限制 Cmdlet 在指定 OU 內對於使用者管理活動的範圍。若要將 Cmdlet 範圍限制在單一 OU，請使用類似下列的語法：-UserScopes &quot;OU:ou=Redmond,dc=litwareinc,dc=com&quot;。您可以使用以逗號分隔的清單來指定多個 OU：-UserScopes &quot;OU:ou=Redmond,dc=litwareinc,dc=com&quot;，&quot;OU:ou=Dublin,dc=litwareinc,dc=com&quot;。若要從角色新增範圍 (或移除現有範圍)，請使用 Windows PowerShell 清單修飾詞語法。如需詳細資訊，請參閱本說明主題中的＜範例＞一節。</p>
<p>您必須為 ConfigScopes 或 UserScopes 屬性 (或兩者) 指定值。</p></td>
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

無。

## 傳回類型

**Set-CsAdminRole** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Roles.Role 物件的執行個體。

