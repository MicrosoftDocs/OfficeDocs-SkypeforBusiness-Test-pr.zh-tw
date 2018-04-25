---
title: New-CsAdminRole
TOCTitle: New-CsAdminRole
ms:assetid: 1e46c02e-0937-4e3b-b02e-e7507189f6aa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398271(v=OCS.15)
ms:contentKeyID: 49290287
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAdminRole

 

_**上次修改主題的時間：** 2015-03-09_

建立新的角色型存取控制 (RBAC) 角色。RBAC 角色可用於定義使用者所能執行的管理工作，以及指定使用者執行這些工作的範圍。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsAdminRole -Identity <String> -Template <String> [-Cmdlets <PSListModifier>] [-ConfigScopes <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-ScriptModules <PSListModifier>] [-UserScopes <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 中的命令會複製 RBAC 角色 CsVoiceAdministrator。因為沒有使用其他參數，所以新角色 RedmondVoiceAdministrators 會是與 CsVoiceAdministrator 完全相同的複製項目，其中包含設為 "global" 的 UserScopes 和 ConfigScopes 內容。

    New-CsAdminRole -Identity "RedmondVoiceAdministrator" -Template "CsVoiceAdministrator"

## 範例 2

範例 2 會建立一個新的 RBAC 角色 (RedmondVoiceAdministrator)，然後將該角色設定為允許單一使用者範圍：Redmond OU。為達此目的，UserScopes 參數會與下列參數值一起加入："OU:ou=Redmond,dc=litwareinc,dc=com"。此參數值會將 UserScopes 屬性的目前值取代成一個項目：將 OU 取代成辨別名稱 (DN) "ou=Redmond,dc=litwareinc,dc=com"。

    New-CsAdminRole -Identity "RedmondVoiceAdministrator" -Template "CsVoiceAdministrator" -UserScopes "OU:ou=Redmond,dc=litwareinc,dc=com"

## 範例 3

範例 3 所示的命令是範例 2 所示命令的變化；唯一的差異在於此範例會將兩個 OU 加入 UserScopes 屬性。作法是指派逗號分隔清單給 Replace 方法：清單中的兩個項目分別代表要指派給新 RBAC 角色之兩個 OU (Redmond 和 Portland) 的識別碼。

    New-CsAdminRole -Identity "RedmondVoiceAdministrator" -Template "CsVoiceAdministrator" -UserScopes "OU:ou=Redmond,dc=litwareinc,dc=com","OU:ou=Portland,dc=litwareinc,dc=com"

## 範例 4

範例 4 會將 SiteId 為 Redmond 的網站指派給新 RBAC 角色的 ConfigScopes 屬性。請注意，ConfigScopes 內容的語法需要使用 "site:" 前置碼加上新增之網站的 SiteId 內容值。

    New-CsAdminRole -Identity "RedmondVoiceAdministrator" -Template "CsVoiceAdministrator" -ConfigScopes "site:Redmond"

## 詳細描述

角色型存取控制 (RBAC) 可讓系統管理員委派控制 Lync Server 中的特定管理工作。例如，您可以不授予組織服務台完整的系統管理員權限，而是給予這些員工非常特定的權限：只管理使用者帳戶的權限；只管理 Enterprise Voice 元件的權限；只管理封存和封存伺服器的權限。此外，這些權限可以依範圍限制：可提供某些人管理 Enterprise Voice 的權限，但僅限於 Redmond 網站；也可提供其他人管理使用者的權限，但僅限於那些帳戶屬於 Finance 組織單位 (OU) 的使用者。

RBAC 的 Lync Server 實作根據以下兩個重要元素：Active Directory 安全性群組與 Windows PowerShell Cmdlet。當您安裝 Lync Server 時，會為您建立許多萬用安全性群組，例如 CsAdministrator、CsArchivingAdministrator 和 CsHelpDesk。這些萬用安全性群組具有一個含 RBAC 角色的一對一對應；這表示任何位於 CsArchivingAdministrator 安全性群組中的使用者具有所有授與 CsArchivingAdministrator RBAC 角色的權限。授與 RBAC 角色的這些權限會依序地以指派給該角色的 Cmdlet 為基礎 (Cmdlet 可以被指派給多個 RBAC 角色)。例如，假設已對某個角色指派下列 Cmdlet：

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

上述清單代表允許指派某假設 RBAC 角色的使用者，在遠端 Windows PowerShell 命令列介面工作階段期間僅能執行的 Cmdlet。如果使用者嘗試執行 **Disable-CsUser** Cmdlet，該命令將會失敗，因為指派假設角色的使用者並不具有執行 **Disable-CsUser** Cmdlet 的權限。這也適用於 Lync Server 控制台。例如，封存系統管理員無法使用 Lync Server 控制台來停用使用者，因為 Lync Server 控制台遵守 RBAC 角色。當您執行 Lync Server 控制台的命令時，實際上是在呼叫 Windows PowerShell Cmdlet。如果不允許您執行 **Disable-CsUser** Cmdlet，則無論您是直接從 Windows PowerShell 執行該 Cmdlet，還是在 Lync Server 控制台內間接執行 Cmdlet，該命令都會失敗。

請注意，RBAC 僅適用於遠端管理。如果您登入執行 Lync Server 的電腦，並開啟 Lync Server 管理命令介面，將不會強制執行 RBAC 角色。而是主要透過安全性群組 RTCUniversalServerAdmins、RTCUniversalUserAdmins 和 RTCUniversalReadOnlyAdmins 來強制執行安全性。

當您安裝 Lync Server 時，安裝程式會建立數個內建的 RBAC 角色。這些角色涵蓋常見的管理範圍，例如語音管理、使用者管理和回應群組管理。這些內建的角色無法以下列任何方式進行修改：您無法將 Cmdlet 新增到角色或從中移除，也無法刪除這些角色 (嘗試刪除內建角色將會造成錯誤出現)。不過，您可以使用內建角色建立自訂 RBAC 角色。接著，可藉由變更管理範圍修改這些自訂的角色；例如，您可以使用特定的 Active Directory OU，將角色限制在管理使用者帳戶。

若要建立新角色，您必須先在 Active Directory 網域服務中建立一個與該角色共用名稱的萬用安全性群組；例如，若要建立一個名稱為 DialInConferencingAdministrator 的新角色，您必須先建立一個具有 SamAccountName DialInConferencingAdministrator 的安全性群組。請注意，**New-CsAdminRole** Cmdlet 不會為您建立此群組。當您呼叫 **New-CsAdminRole** Cmdlet 時，如果 DialInConferencingAdministrator 群組不存在，則命令會失敗。您指派給新角色的 Identity 必須是對應 Active Directory 群組的 SamAccountName。

建立 Active Directory 安全性群組之後，您必須選取一個內建的 RBAC 角色，當做新自訂角色的範本使用。您無法使用 **New-CsAdminRole** Cmdlet 建立空白的 RBAC 角色。所有的自訂角色都必須以其中一個內建 RBAC 角色為基礎。也就是說，自訂角色必須擁有與其中一個內建角色相同的已指派 Cmdlet。但是，您可以使用 **Set-CsAdminRole** Cmdlet 來變更此自訂角色的管理範圍。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsAdminRole** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsAdminRole"}

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
<td><p>要建立之 RBAC 角色的唯一識別碼。RBAC 角色的 Identity 必須與該角色相關聯之 Active Directory 萬用安全性群組的 SamAccountName 相同。例如，Help Desk 角色具有等於 CsHelpDesk 的 Identity；CsHelpDesk 也是與該角色相關聯之 Active Directory 萬用安全性群組的 SamAccountName。</p></td>
</tr>
<tr class="even">
<td><p><em>Template</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>內建 RBAC 角色的名稱，該角色將會當作要建立之自訂 RBAC 角色的範本使用。所有新的 RBAC 角色都必須以現有角色為基礎；您無法建立空白的 RBAC 角色 (亦即，未指派 Cmdlet 的角色，或未指派值給 ConfigScopes 或 UserScopes 內容的角色)。不過，在自訂角色建立完成之後，您可以使用 <strong>Set-CsAdminRole</strong> Cmdlet 修改新角色的屬性。</p></td>
</tr>
<tr class="odd">
<td><p><em>Cmdlets</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>可讓您指定可供擁有新 RBAC 角色之使用者使用的 Cmdlet。例如，若要建立只提供一個 Cmdlet (<strong>Export-CsArchivingData</strong> Cmdlet) 存取權的新角色，請使用如下語法：</p>
<p>-Cmdlets &quot;Export-CsArchivingData&quot;</p>
<p>若要允許存取多個 Cmdlet，請使用逗號將 Cmdlet 名稱隔開：</p>
<p>-Cmdlets &quot;Export-CsArchivingData&quot;,&quot;Invoke-CsArchivingDatabasePurge&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ConfigScopes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>用來將 Cmdlet 的範圍限制為指定之網站中的組態設定。若要將 Cmdlet 範圍限制在單一網站，請使用類似下列的語法：-ConfigScopes site:Redmond。使用逗號分隔清單可以指定多個網站：-ConfigScopes &quot;site:Redmond, &quot;site:Dublin&quot;。您也可以將 ConfigScopes 屬性設定為 &quot;global&quot;。</p>
<p>指派值給 ConfigScopes 參數時，您必須使用首碼 &quot;site:&quot; 加上網站 SiteId 內容的值；請注意，SiteID 的值與網站的 Identity 或網站的 DisplayName 不一定相同。若要決定指定網站的 SiteId，您可以使用類似下列的命令：</p>
<p>Get-CsSite &quot;Redmond&quot; | Select-Object SiteId</p>
<p>您必須為 ConfigScopes 或 UserScopes 屬性 (或兩者) 指定值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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
<td><p><em>ScriptModules</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>可讓您指定 Windows PowerShell 指令碼中的功能，以供擁有新 RBAC 角色的使用者使用。例如，下列語法提供 UpdateDatabase.ps1 指令碼中 Reset 函式的存取權：</p>
<p>-ScriptModules &quot;UpdateDatabase.ps1:Reset&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>UserScopes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>用來將 Cmdlet 的範圍限制為指定之組織單位中的使用者管理活動。若要將 Cmdlet 範圍限制為單一組織單位，請使用類似下列的語法：-UserScopes &quot;OU:ou=Redmond,dc=litwareinc,dc=com&quot;。使用逗號分隔清單可以指定多個組織單位：-UserScopes &quot;OU:ou=Redmond,dc=litwareinc,dc=com&quot;, &quot;OU:ou=Dublin,dc=litwareinc,dc=com&quot;。若要從角色新增範圍 (或移除現有範圍)，請使用 Windows PowerShell 清單修飾詞語法。如需詳細資訊，請參閱本主題的＜範例＞一節。</p>
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

**New-CsAdminRole** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.Roles.Role 物件的新執行個體。

