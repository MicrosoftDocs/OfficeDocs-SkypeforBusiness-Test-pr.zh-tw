---
title: Get-CsClientVersionPolicy
TOCTitle: Get-CsClientVersionPolicy
ms:assetid: d99bfa89-01a7-4dd4-8f6e-96e0a84ab1ce
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398957(v=OCS.15)
ms:contentKeyID: 49292483
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientVersionPolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回 Lync Server 環境所支援之用戶端 (例如 Microsoft Office Communicator 2007 R2) 的資訊。用戶端版本原則可讓您指定可以登入您 Lync Server 系統的用戶端 (例如 Office Communicator 2007 R2)。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsClientVersionPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClientVersionPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

第一個範例會呼叫不含任何其他參數的 **Get-CsClientVersionPolicy** Cmdlet，讓 **Get-CsClientVersionPolicy** Cmdlet 傳回設定供組織使用之所有用戶端版本原則的集合。

    Get-CsClientVersionPolicy

## 範例 2

在範例 2 中， **Get-CsClientVersionPolicy** Cmdlet 會傳回所有 Identity 為 site:Redmond 的用戶端版本原則。由於 Identity 必須是唯一的，因此這個命令絕對不會傳回一個以上的項目。

    Get-CsClientVersionPolicy -Identity site:Redmond

## 範例 3

範例 3 會傳回在網站範圍設定的所有用戶端版本原則。作法是加入 Filter 參數搭配篩選值 "site:\*"。此值會指示 **Get-CsClientVersionPolicy** Cmdlet 只傳回 Identity 開頭為 "site:" 字串值的原則。

    Get-CsClientVersionPolicy -Filter site:*

## 範例 4

範例 4 使用的命令會顯示個別規則的詳細資訊，這些規則是針對每一個用戶端版本原則而設定。為達成此目的，會先使用 **Get-CsClientVersionPolicy** Cmdlet，以擷取設定供組織使用之所有用戶端版本原則的集合。然後，此集合會管線傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 篩選來展開 Rules 屬性的屬性值。展開此屬性時，每一個規則的詳細資訊 (包括組建編號、主要版本及次要版本等內容值) 都會顯示在螢幕上。

    Get-CsClientVersionPolicy | Select-Object -ExpandProperty Rules

## 詳細描述

用戶端版本原則代表用戶端版本規則的集合；而用戶端版本規則用於決定允許登入 Lync Server 的用戶端應用程式。當使用者嘗試登入 Lync Server 時，該使用者的用戶端應用程式會傳送 SIP 標頭給伺服器，這個標頭包含與應用程式本身有關的詳細資訊，包括軟體的主要版本和組建編號。然後系統會根據用戶端版本規則的集合，檢查 SIP 標頭所含的版本資訊，查看是否有任何規則要套用至該特定應用程式。如果有這樣的規則，Lync Server 就會採取此規則指定的行動。例如，規則可能會告知 Lync Server 允許登入、封鎖登入，或允許登入，但是會以無訊息方式將用戶端應用程式升級為最新版本 (例如，將 Communicator 2007 R2 升級到 Lync)。

用戶端版本原則 (可套用至全域範圍、網站範圍、服務範圍 (僅登錄器服務)，或個別使用者範圍)，可讓您在決定哪些用戶端應用程式可用來存取系統時，擁有彈性。例如，您可能想防止使用者使用 Communicator 2007 R2 登入 Lync Server，畢竟它與 Lync 2013 所支援的功能和特性並不同。但是，由於硬體或軟體衝突，您可能也想選取一組無法升級為 Lync 的使用者。在該情況下，您可以建立個別的規則 (以及個別的用戶端版本原則)，允許那些使用者從 Communicator 2007 R2 登入。

**Get-CsClientVersionPolicy** Cmdlet 可讓您擷取所有正在組織中使用的用戶端版本原則，也能讓您檢視組成各個原則的個別規則。

請注意，用戶端版本原則不適用於同盟使用者；而是同盟使用者受到本身組織中使用的用戶端版本原則所約束。例如，假設某位同盟使用者使用用戶端 A (此為同盟組織所允許的用戶端)。只要同盟組織允許使用用戶端 A，這個使用者就可以使用該用戶端與您的組織通訊。即使您的用戶端版本原則會封鎖使用用戶端 A，此情況也成立。在您組織中強制執行的用戶端版本原則不會覆寫同盟組織中使用者的用戶端版本原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsClientVersionPolicy** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientVersionPolicy\\b"}

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
<td><p>System.Strkng</p></td>
<td><p>可讓您在指定要擷取的原則時使用萬用字元。例如，下列語法會傳回所有在網站範圍內設定的原則：-Filter &quot;site:*&quot;。下列語法會傳回所有在個別使用者範圍內設定的原則：-Filter &quot;tag:*&quot;。</p>
<p>您無法在同一個命令中同時使用 Filter 與 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之原則的唯一識別碼。若要傳回全域原則，請使用下列語法：-Identity global。若要傳回在網站範圍設定的原則，請使用下列語法：-Identity &quot;site:Redmond&quot;。若要傳回在服務範圍設定的原則，請使用下列語法：-Identity &quot;Registrar:atl-cs-001.litwareinc.com&quot;。登錄器服務是唯一能主控用戶端版本原則的服務。</p>
<p>原則也能在個別使用者範圍內加以設定。若要傳回其中一個原則，請使用類似下列的語法：-Identity &quot;SalesDepartmentPolicy&quot;。</p>
<p>若未加入此參數，將會傳回所有設定供組織使用的用戶端版本原則。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區本機複本擷取用戶端版本原則資料，而不從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsClientVersionPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsClientVersionPolicy** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersion 原則物件的執行個體。

## 請參閱

#### 其他資源

[Grant-CsClientVersionPolicy](grant-csclientversionpolicy.md)  
[New-CsClientVersionPolicy](new-csclientversionpolicy.md)  
[Remove-CsClientVersionPolicy](remove-csclientversionpolicy.md)  
[Set-CsClientVersionPolicy](set-csclientversionpolicy.md)

