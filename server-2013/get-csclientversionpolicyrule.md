---
title: Get-CsClientVersionPolicyRule
TOCTitle: Get-CsClientVersionPolicyRule
ms:assetid: f81f4f6c-5201-46c5-89f6-da859ce99b2e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413048(v=OCS.15)
ms:contentKeyID: 49292863
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientVersionPolicyRule

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用的用戶端版本原則規則。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsClientVersionPolicyRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClientVersionPolicyRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回組織目前所使用的所有用戶端版本原則規則相關資訊。

    Get-CsClientVersionPolicyRule

## 範例 2

範例 2 會傳回單一用戶端版本原則規則的資訊：Identity 為 Global/2336c611-a243-4c5d-994b-eea8a524d0e4 的規則。

    Get-CsClientVersionPolicyRule -Identity "Global/2336c611-a243-4c5d-994b-eea8a524d0e4"

## 範例 3

範例 3 會傳回在全域範圍設定的所有用戶端版本原則規則。為達此目的，命令會使用 Filter 參數和篩選值 "Global/\*"。此篩選值只會傳回 Identity 開頭為字串值 "Global/" 的規則。

    Get-CsClientVersionPolicyRule -Filter "Global/*"

## 範例 4

範例 4 所示的命令會傳回目前已停用的所有用戶端版本原則規則。為達成此目的，命令會先呼叫 **Get-CsClientVersionPolicy** Cmdlet 傳回所有可用用戶端原則規則的集合。然後，此集合會以管線傳送到 **Where-Object** Cmdlet，這會只挑出 Enabled 屬性等於 False 的規則。

    Get-CsClientVersionPolicyRule | Where-Object {$_.Enabled -eq $False}

## 範例 5

範例 5 會傳回所有封鎖用戶端應用程式登入的用戶端版本原則規則。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsClientVersionPolicy** Cmdlet，以傳回目前所使用之所有規則的集合。然後，此集合會以管線傳送到 **Where-Object** Cmdlet，這會只選取 Action 屬性等於 Block 的規則。

    Get-CsClientVersionPolicyRule | Where-Object {$_.Action -eq "Block"}

## 詳細描述

用戶端版本原則規則可用來判斷允許登入 Lync Server 的用戶端應用程式。當使用者嘗試登入 Lync Server 時，該使用者的用戶端應用程式會傳送 SIP 標頭給伺服器，這個標頭包含與應用程式本身有關的詳細資訊，包括軟體的主要版本、次要版本和組建編號。接著，系統會根據用戶端版本規則集合來檢查版本資訊，查看是否有任何規則要套用至該特定應用程式。例如，假設某位使用者嘗試使用 Microsoft Office Communicator 2007 R2 登入。在使用者可以登入 Lync Server 之前，系統會檢查是否有適用於 Office Communicator 2007 R2 的用戶端版本規則。如果有這樣的規則，Lync Server 就會採取此規則指定的動作。該動作必須是下列任一項：

Allow。允許使用者登入。

AllowAndUpgrade。允許使用者登入，並自動將使用者的 Communicator 2007 R2 複本升級為最新版本的 Lync。會視您設定系統的方式而定，使用 Microsoft Update 或 Windows Server Update Services 執行升級。

AllowWithUrl。允許使用者登入，並顯示訊息以指出使用者可以下載及安裝 Lync 最新版本的 URL。該 URL 必須指向您自己建立的網站；而不是指向安裝 Lync Server 時系統為您建立的網站。

Block。不允許使用者登入。

BlockAndUpgrade。不允許使用者登入，但會自動將使用者的 Communicator 2007 R2 複本升級為最新版本的 Lync。接下來，使用者便能嘗試使用新的用戶端應用程式登入。會視您設定系統的方式而定，使用 Microsoft Update 或 Windows Server Update Services 執行升級。

BlockWithUrl。不允許使用者登入，但會顯示訊息以指出使用者可下載及安裝最新版本之 Lync 的 URL。該 URL 必須指向您自己建立的網站；而不是指向安裝 Lync Server 時系統為您建立的網站。

系統會將用戶端版本規則收集在用戶端版本原則中。這些原則可在全域範圍、網站範圍、服務範圍 (登錄器服務) 或個別使用者範圍內設定。 **Get-CsClientVersionPolicyRule** Cmdlet 會為系統管理員提供一種方法，來檢視有關已設定為供組織使用之每個原則規則的詳細資訊。

請注意，用戶端版本原則不會套用到同盟使用者；而是同盟使用者受到本身組織中使用的用戶端版本原則所約束。例如，假設某位同盟使用者使用用戶端 A (此為同盟組織所允許的用戶端)。只要同盟組織允許使用用戶端 A，這個使用者就可以使用該用戶端與您的組織通訊。即使您的用戶端版本原則會封鎖使用用戶端 A，此情況也成立。在您組織中強制執行的用戶端版本原則不會覆寫同盟組織中使用者的用戶端版本原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsClientVersionPolicyRule** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientVersionPolicyRule"}

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
<td><p>讓您能夠在指定要傳回的用戶端版本原則規則時使用萬用字元。例如，若要傳回已在 Redmond 網站內設定的所有規則，請使用下列語法：-Filter &quot;site:Redmond/*&quot;。</p>
<p>您無法在同一個命令中同時使用 Filter 與 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之用戶端版本原則規則的唯一識別碼。用戶端版本規則的 Identity 是由設定規則的所在範圍和全域唯一識別碼 (GUID) 所組成的。這表示，規則會有類似如下的 Identity：site:Redmond/1987d3c2-4544-489d-bbe3-59f79f530a83。由於 GUID 很難記住和使用，所以本說明主題中的＜範例＞區段列出了讓您可以識別要傳回規則的替代方法。</p>
<p>若未指定此參數，則將傳回已設定為要使用的所有用戶端版本原則規則。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取用戶端版本原則規則資料，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsClientVersionPolicyRule** Cmdlet 不接受以管線傳送的輸入。

## 傳回類型

**Get-CsClientVersionPolicyRule** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Rule 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsClientVersionPolicyRule](new-csclientversionpolicyrule.md)  
[Remove-CsClientVersionPolicyRule](remove-csclientversionpolicyrule.md)  
[Set-CsClientVersionPolicyRule](set-csclientversionpolicyrule.md)

