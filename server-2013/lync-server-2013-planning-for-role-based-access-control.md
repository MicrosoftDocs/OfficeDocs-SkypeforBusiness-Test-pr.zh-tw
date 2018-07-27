---
title: Lync Server 2013：規劃角色型存取控制
TOCTitle: 規劃角色型存取控制 (RBAC)
ms:assetid: 41204ba3-ce5b-41a8-a6c3-b444468fa328
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425917(v=OCS.15)
ms:contentKeyID: 49290715
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中規劃角色型存取控制

 

_**上次修改主題的時間：** 2015-03-09_

為了讓您能委派系統管理工作，同時維護高安全標準， Lync Server 2013 提供了角色型存取控制 (RBAC)。使用 RBAC，指派使用者給系統管理角色，即可授與系統管理權限。 Lync Server 2013 包含了一組豐富的內建系統管理角色，可讓您建立新的角色並針對每一個新角色指定 Cmdlet 的自訂清單。您也可以將 Cmdlet 的指令碼新增至預先定義與自訂 RBAC 角色之允許的工作中。

## 更佳的伺服器安全性與集中性

透過 RBAC，使用者可以依據各自的 Lync Server 角色進行更準確的存取與授權。如此一來便可讓「最低權限」的安全性實務發揮效用，限制系統管理員與使用者擁有執行工作必要的權限。

> [!IMPORTANT]  
> RBAC 限制只對遠端工作的系統管理員有效，並需透過 Lync Server 控制台或 Lync Server 管理命令介面來執行。當使用者直接使用執行 Lync Server 的伺服器時，便不受 RBAC 限制。因此，您的 Lync Server 實體安全攸關 RBAC 限制是否能夠順利實施。



## 角色與範圍

在 RBAC， *「角色」* 已經過啟用可使用 Cmdlet 的清單，主要是提供特定類型的系統管理員或技術人員使用。 *「範圍」* 指的是角色中定義的 Cmdlet 賴以操作的物件集合。範圍影響的物件可能是使用者帳戶 (依組織單位分組) 或伺服器 (依網站分組)。

下表列出 Lync Server 中預先定義的角色清單，並概要說明每一個角色所能從事的工作類型。第四欄說明每一個 Microsoft Exchange Server 角色 (若有的話) 的相近 Lync Server 角色。

### 預先定義的系統管理角色

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>角色</th>
<th>允許的工作</th>
<th>Active Directory 基礎群組</th>
<th>Exchange 相等項目</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CsAdministrator</p></td>
<td><p>可執行所有系統管理工作並修改所有設定，包括建立角色及指派使用者給角色。可新增新的網站、集區與服務，藉以擴充部署項目。</p></td>
<td><p>CSAdministrator</p></td>
<td><p>組織管理</p></td>
</tr>
<tr class="even">
<td><p>CsUserAdministrator</p></td>
<td><p>可為 Lync Server 啟用及停用使用者、移動使用者並將現有原則指派給使用者。無法修改原則。</p></td>
<td><p>CSUserAdministrator</p></td>
<td><p>郵件收件者</p></td>
</tr>
<tr class="odd">
<td><p>CsVoiceAdministrator</p></td>
<td><p>可建立、設定及管理語音相關的設定及原則。</p></td>
<td><p>CSVoiceAdministrator</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>CsServerAdministrator</p></td>
<td><p>可對伺服器與相關服務進行管理、監控及疑難排解。可防止對伺服器進行全新的連線作業、停止與啟動服務，以及套用軟體更新。無法進行具有全域組態影響的變更。</p></td>
<td><p>CSServerAdministrator</p></td>
<td><p>伺服器管理</p></td>
</tr>
<tr class="odd">
<td><p>CsViewOnlyAdministrator</p></td>
<td><p>可檢視部署情況 (包括使用者與伺服器資訊) 以監控部署運作情況。</p></td>
<td><p>CSViewOnlyAdministrator</p></td>
<td><p>僅供檢視的組織管理</p></td>
</tr>
<tr class="even">
<td><p>CsHelpDesk</p></td>
<td><p>可檢視部署內容，包括使用者內容與原則。可執行特定疑難排解工作。無法變更使用者內容或原則、伺服器組態或相關服務。</p></td>
<td><p>CSHelpDesk</p></td>
<td><p>技術服務</p></td>
</tr>
<tr class="odd">
<td><p>CsArchivingAdministrator</p></td>
<td><p>可修改封存組態與原則。</p></td>
<td><p>CSArchivingAdministrator</p></td>
<td><p>保留管理、法務保存措施</p></td>
</tr>
<tr class="even">
<td><p>CsResponseGroupAdministrator</p></td>
<td><p>可管理網站內的回應群組應用程式組態。</p></td>
<td><p>CSResponseGroupAdministrator</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>CsLocationAdministrator</p></td>
<td><p>最低層級的增強型 9-1-1 (E9-1-1) 管理權限，包括建立 E9-1-1 位置與網路識別碼，並將這些識別碼彼此關聯。此角色一律指派全域範圍。</p></td>
<td><p>CSLocationAdministrator</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>CsResponseGroupManager</p></td>
<td><p>可管理特定回應群組。</p></td>
<td><p>CSResponseGroupManager</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>CsPersistentChatAdministrator</p></td>
<td><p>可管理常設聊天功能和特定的常設聊天室。</p></td>
<td><p>CSPersistentChatAdministrator</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>CsAdministrator</p></td>
<td><p>可執行所有系統管理工作並修改所有設定，包括建立角色及指派使用者給角色。可新增新的網站、集區與服務，藉以擴充部署項目。</p></td>
<td><p>CSAdministrator</p></td>
<td><p>組織管理</p></td>
</tr>
<tr class="odd">
<td><p>CsUserAdministrator</p></td>
<td><p>可為 Lync Server 啟用及停用使用者、移動使用者並將現有原則指派給使用者。無法修改原則。</p></td>
<td><p>CSUserAdministrator</p></td>
<td><p>郵件收件者</p></td>
</tr>
<tr class="even">
<td><p>CsVoiceAdministrator</p></td>
<td><p>可建立、設定及管理語音相關的設定及原則。</p></td>
<td><p>CSVoiceAdministrator</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>CsServerAdministrator</p></td>
<td><p>可對伺服器與相關服務進行管理、監控及疑難排解。可防止對伺服器進行全新的連線作業、停止與啟動服務，以及套用軟體更新。無法進行具有全域組態影響的變更。</p></td>
<td><p>CSServerAdministrator</p></td>
<td><p>伺服器管理</p></td>
</tr>
<tr class="even">
<td><p>CsViewOnlyAdministrator</p></td>
<td><p>可檢視部署情況 (包括使用者與伺服器資訊) 以監控部署運作情況。</p></td>
<td><p>CSViewOnlyAdministrator</p></td>
<td><p>僅供檢視的組織管理</p></td>
</tr>
<tr class="odd">
<td><p>CsHelpDesk</p></td>
<td><p>可檢視部署內容，包括使用者內容與原則。可執行特定疑難排解工作。無法變更使用者內容或原則、伺服器組態或相關服務。</p></td>
<td><p>CSHelpDesk</p></td>
<td><p>技術服務</p></td>
</tr>
<tr class="even">
<td><p>CsArchivingAdministrator</p></td>
<td><p>可修改封存組態與原則。</p></td>
<td><p>CSArchivingAdministrator</p></td>
<td><p>保留管理、法務保存措施</p></td>
</tr>
<tr class="odd">
<td><p>CsResponseGroupAdministrator</p></td>
<td><p>可管理網站內的回應群組應用程式組態。</p></td>
<td><p>CSResponseGroupAdministrator</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>CsLocationAdministrator</p></td>
<td><p>最低層級的增強型 9-1-1 (E9-1-1) 管理權限，包括建立 E9-1-1 位置與網路識別碼，並將這些識別碼彼此關聯。此角色一律指派全域範圍。</p></td>
<td><p>CSLocationAdministrator</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>CsResponseGroupManager</p></td>
<td><p>可管理特定回應群組。</p></td>
<td><p>CSResponseGroupManager</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>CsPersistentChatAdministrator</p></td>
<td><p>可管理常設聊天功能和特定的常設聊天室。</p></td>
<td><p>CSPersistentChatAdministrator</p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


Lync Server 中隨附的所有預先定義的角色都具有全域範圍。為了遵循最低權限實務，當使用者只需要管理有限的伺服器或使用者時，請勿將全域範圍的角色指派給他們。要達到這個目的，請依據現有的角色建立相關角色，但在範圍上稍做限制即可。

## 建立有範圍的角色

建立範圍有限的角色 (有範圍的角色) 時，您必須指定範圍及其依據的現有角色，以及要指派給該角色的 Active Directory 群組。您指定的 Active Directory 群組必須事先建立好。以下 Cmdlet 將示範如何建立範圍有限且擁有其中一個預先定義管理權限的角色)。該 Cmdlet 會建立名為 `Site01 Server Administrators` 的全新角色。此角色具有預先定義之 CsServerAdministrator 角色的能力，但僅適用位於 Site01 網站的伺服器。為了讓此 Cmdlet 順利運作，Site01 網站必須預先定義好，且名為 `Site01 Server Administrators` 的萬用安全性群組必須已存在。

    New-CsAdminRole -Identity "Site01 Server Administrators" -Template CsServerAdministrator -ConfigScopes "site:Site01"

此 Cmdlet 一經執行，所有屬於 `Site01 Server Administrators` 群組成員的使用者，都會擁有 Site01 中伺服器的伺服器管理員權限。此外，後續新增至此萬用安全性群組的任何使用者，也會取得該角色的所有權限。請注意，角色本身與指派的萬用安全性群組都稱為 `Site01 Server Administrators`。

以下範例將限制使用者範圍，而非伺服器範圍。該範例將建立 `Sales Users Administrator` 角色，以管理 Sales 組織單位裡的使用者帳戶。必須事先建立 SalesUsersAdministrator 萬用安全性群組，此 Cmdlet 才能運作。

    New-CsAdminRole -Identity "Sales Users Administrator " -Template CsUserAdministrator -UserScopes "OU:OU=Sales, OU=Lync Tenants, DC=Domain, DC=com"

## 建立新角色

若要建立一個新角色能夠存取非預先定義角色中的一組 Cmdlet、指令碼或模組，您可再次從使用其中一個預先定義角色為範本開始。請注意，角色可執行的指令碼和模組必須儲存於下列位置：

  - Lync 模組的預設路徑為 C:\\Program Files\\Common Files\\Microsoft Lync Server 2013\\Modules\\Lync

  - 使用者指令碼的預設路徑為 C:\\Program Files\\Common Files\\Microsoft Lync Server 2013\\AdminScripts

若要建立新角色，需使用 **New-CsAdminRole** Cmdlet。執行 **New-CsAdminRole** 之前，必須先建立與此角色相關聯的基礎萬用安全性群組。

下列 Cmdlet 可作為建立新角色的範例。這些 Cmdlet 建立的新角色類型稱為 `MyHelpDeskScriptRole`。新角色具有預先定義 CsHelpDesk 角色的功能，可在名為「testscript」的指令碼中額外執行各項功能。

    New-CsAdminRole -Identity "MyHelpDeskScriptRole" -Template CsHelpDesk -ScriptModules @{Add="testScript.ps1"}

若要讓此 Cmdlet 能夠運作，必須先建立萬用安全性群組 MyHelpDeskScriptRole。

此 Cmdlet 執行後，就能將使用者直接指派給此角色 (此時使用者擁有全域範圍)，或是依據此角色建立有範圍的角色，如本文件先前在〈建立有範圍的角色〉中所述。

## 指派角色給使用者

每個 Lync Server 角色都會有相關聯的 Active Directory 萬用安全性群組。您新增至基礎群組的任何使用者都會獲得該角色的能力。

上述各節的範例會建立新的角色，並為其指派現有的萬用安全性群組。若要將現有角色指派給一或多位使用者，請將那些使用者新增至與該角色關聯的群組。您可以新增個別使用者與萬用安全性群組至這些群組。

例如，Active Directory 中的「CS 系統管理員」 萬用安全性群組會自動獲授予 **CsAdministrator** 角色。這個萬用安全性群組是您在部署 Lync Server 時於 Active Directory 中建立的。若要授予這個權限給使用者或群組，只需將使用者或群組新增至「CS 系統管理員」 群組即可。

您可以將使用者新增至對應每個群組的 Active Directory 基礎群組，藉此賦予其多重 RBAC 角色。

請注意，當您建立角色時，後續新增至該 Active Directory 基礎群組的使用者將會繼承該角色的權限。

## 修改角色功能

您可以修改角色可執行的 Cmdlet 和指令碼清單；也可同時修改自訂角色可執行的 Cmdlet 和指令碼，但僅能修改預先定義角色的指令碼。每個鍵入的 Cmdlet 均可新增、移除或更換 Cmdlet 或指令碼。

若要修改角色，請使用 **Set-CsAdminRole** Cmdlet。下列 Cmdlet 可移除角色中的一個指令碼。

    Set-CsAdminRole -Identity "MyHelpDeskScriptRole" -ScriptModules @{Remove="testScript.ps1"}

## 規劃 RBAC

至於被授予 Lync Server 部署各種管理權限的人員，可確實考量其所需執行的任務，再指派擁有最低權限以及該工作所需範圍的角色給他們。必要時可以使用 **Set-CsAdminRole** Cmdlet 建立只擁有其任務所需 Cmdlet 的新角色。

具有 CsAdministrator 角色的使用者可以建立所有種類的角色，包括依據 CsAdministrator 建立的角色，並將其指派給使用者。最佳做法是將 CsAdministrator 角色指派給非常少數的受信任使用者。

