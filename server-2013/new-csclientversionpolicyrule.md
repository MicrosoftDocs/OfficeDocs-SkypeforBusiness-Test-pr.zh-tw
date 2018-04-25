---
title: New-CsClientVersionPolicyRule
TOCTitle: New-CsClientVersionPolicyRule
ms:assetid: d28df005-0db0-4b17-9ca0-9dc9ed063d73
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398905(v=OCS.15)
ms:contentKeyID: 49292399
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientVersionPolicyRule

 

_**上次修改主題的時間：** 2015-03-09_

建立新的用戶端版本原則規則。用戶端版本原則規則可用於指定使用者是否能夠使用特定的用戶端應用程式登入 Lync Server。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsClientVersionPolicyRule -Identity <XdsIdentity> <COMMON PARAMETERS>

    New-CsClientVersionPolicyRule -Parent <String> -RuleId <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Action <Allow | AllowAndUpgrade | AllowWithUrl | Block | BlockAndUpgrade | BlockWithUrl>] [-ActionUrl <String>] [-BuildNumber <UInt16>] [-CompareOp <EQL | NEQ | GTR | GEQ | LSS | LEQ>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MajorVersion <UInt16>] [-MinorVersion <UInt16>] [-Priority <Int32>] [-QfeNumber <UInt16>] [-UserAgent <String>] [-UserAgentFullName <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 示範如何建立新用戶端版本原則規則。原則規則具有由以下兩部分組成的 Identity：要指派宣告的範圍和 36 個字元的 GUID。在建立新的用戶端版本原則規則時，首先需要使用 .NET Framework 方法 NewGuid 來建立新的 GUID。範例的第一個命令可實現此步驟，而產生的 GUID 則會儲存在變數 $x 中。

完成 GUID 的建立後，您便可以使用 **New-CsClientVersionPolicyRule** Cmdlet 來建立新規則。此命令使用 4 個參數：Parent：其參數值代表新規則的範圍 (site:Redmond)；RuleId：其參數值 $x 代表新建立的 GUID；MajorVersion (4)；和 UserAgent (InHouse)。在此案例中，UserAgent 參數代表內部用戶端應用程式。

    $x = [guid]::NewGuid()
    
    New-CsClientVersionPolicyRule -Parent "site:Redmond" -RuleId $x -MajorVersion 4 -UserAgent InHouse

## 範例 2

範例 2 所示的命令是範例 1 命令的變化：不過在此案例中，新規則最初只會建立於記憶體中，稍後才會新增至 Lync Server。為達此目的，範例的第一個命令會建立 Identity 的 GUID 部分。第二個命令會建立只存在於記憶體中的新用戶端版本原則規則。InMemory 參數可確保規則只存在於記憶體中，同時不會立即新增至 Lync Server 基礎結構內。如範例 1 所示，Parent 和 RuleId 參數可用來指定新規則的範圍和 GUID，因此這兩個元件可構成規則的 Identity。

在建立虛擬規則後，後續的兩個命令可分別用來指派 MajorVersion 和 UserAgent 屬性的值。在完成上述作業後，範例中的最後一個命令 (連同 **Set-CsClientVersionPolicyRule** Cmdlet) 可用來建立實際的用戶端版本原則規則，並將規則指派給 Redmond 網站。

    $x = [guid]::NewGuid()
    
    $z = New-CsClientVersionPolicyRule -Parent "site:Redmond" -RuleId $x -InMemory
    $z.MajorVersion = 4 
    $z.UserAgent = "Inhouse"
    Set-CsClientVersionPolicyRule -Instance $z

## 詳細描述

用戶端版本原則規則可用來判斷允許登入 Lync Server 的用戶端應用程式。當使用者嘗試登入 Lync Server 時，該使用者的用戶端應用程式會傳送 SIP 標頭給伺服器，這個標頭包含與應用程式本身有關的詳細資訊，包括軟體的主要版本和組建編號。接著，系統會根據用戶端版本規則集合來檢查版本資訊，查看是否有任何規則要套用至該特定應用程式。例如，假設某位使用者嘗試使用 Microsoft Office Communicator 2007 R2 登入。在使用者可以登入 Lync Server 之前，系統會檢查是否有適用於 Office Communicator 2007 R2 的用戶端版本規則。如果有這樣的規則，Lync Server 就會採取此規則指定的動作。該動作必須是下列任一項：

Allow。允許使用者登入。

AllowAndUpgrade。允許使用者登入，並自動將使用者的 Communicator 2007 R2 複本升級為最新版本的 Lync。會視您設定系統的方式而定，使用 Microsoft Update 或 Windows Server Update Services 執行升級。

AllowWithUrl。允許使用者登入，並顯示訊息以指出使用者可以下載及安裝 Lync 最新版本的 URL。該 URL 必須指向您自己建立的網站；而不是指向安裝 Lync Server 時系統為您建立的網站。

Block。不允許使用者登入。

BlockAndUpgrade。不允許使用者登入，但會自動將使用者的 Communicator 2007 R2 複本升級為最新版本的 Lync。接下來，使用者便能嘗試使用新的用戶端應用程式登入。會視您設定系統的方式而定，使用 Microsoft Update 或 Windows Server Update Services 執行升級。

BlockWithUrl。不允許使用者登入，但會顯示訊息以指出使用者可下載及安裝最新版本之 Lync 的 URL。該 URL 必須指向您自己建立的網站；而不是指向安裝 Lync Server 時系統為您建立的網站。

系統會將用戶端版本原則規則收集在用戶端版本原則中。用戶端版本原則是可在全域範圍、網站範圍、服務範圍 (登錄器服務) 或個別使用者範圍內設定的原則。您可以使用 **New-CsClientVersionPolicyRule** Cmdlet 來建立新的用戶端版本規則。在建立新規則時，您還必須指定該規則的 Identity；規則的 Identity 是由範圍 (如 site:Redmond) 和全域唯一識別碼 (GUID) 所組成。您可以自行拼湊 Identity，或提供範圍 (Parent 參數) 和 GUID (RuleId 參數)，再由 **New-CsClientVerisonPolicyRule** Cmdlet 為您建立 Identity。

請注意，用戶端版本原則不適用於同盟使用者；而是同盟使用者受到本身組織中使用的用戶端版本原則所約束。例如，假設某位同盟使用者使用用戶端 A (此為同盟組織所允許的用戶端)。只要同盟組織允許使用用戶端 A，這個使用者就可以使用該用戶端與您的組織通訊。即使您的用戶端版本原則會封鎖使用用戶端 A，此情況也成立。在您組織中強制執行的用戶端版本原則不會覆寫同盟組織中使用者的用戶端版本原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsClientVersionPolicyRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientVersionPolicyRule"}

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
<td><p>要建立之用戶端版本原則規則的唯一識別碼。用戶端版本原則規則的 Identity 是由設定規則的所在範圍和全域唯一識別碼 (GUID) 所組成的。這表示，規則會有類似如下的 Identity：site:Redmond/1987d3c2-4544-489d-bbe3-59f79f530a83.</p>
<p>與其使用 Identity 參數，您可以改用 Parent 和 RuleId 參數，讓 <strong>New-CsClientVerisonPolicyRule</strong> Cmdlet 為您建立 Identity。</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>新規則的範圍資訊。若要使用 Parent 參數來建立全域原則的新規則，請使用下列語法：-Parent global。若要建立網站原則的新規則，請使用下列語法：-Parent &quot;site:Redmond&quot;。若要建立服務原則的新規則，請使用和以下範例相似的語法：-parent &quot;Registrar:atl-cs-001.litwareinc.com&quot;。若要建立個別使用者原則的新規則，請使用下列語法：-Parent &quot;RedmondClientVersionPolicy&quot;。</p>
<p>在建立新規則時，您必須使用 Identity 參數或同時使用 Parent 和 RuleId 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>RuleId</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>規則的全域唯一識別碼 (GUID)。在 Windows PowerShell 中，您可以使用下列命令來建立 GUID：</p>
<p>$x = [guid]::NewGuid()</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Action</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Action</p></td>
<td><p>每當規則觸發時要採取的動作 (即每當有使用者嘗試使用特定軟體登入時)。有效值為：</p>
<p>Allow。允許使用者登入。</p>
<p>AllowWithUrl。允許使用者登入，並顯示訊息以指出使用者可下載及安裝最新版本之 Lync 的 URL。</p>
<p>AllowAndUpgrade。允許使用者登入，並自動將使用者的 Communicator 複本升級為最新版本的 Lync。</p>
<p>Block。不允許使用者登入。</p>
<p>BlockWithUrl。不允許使用者登入，但會顯示訊息以指出使用者可下載及安裝最新版本之 Lync 的 URL。</p>
<p>BlockAndUpgrade。不允許使用者登入，但會自動將使用者的 Communicator 複本升級為最新版本的 Lync。接下來，使用者便能嘗試使用新的用戶端應用程式登入。</p></td>
</tr>
<tr class="odd">
<td><p><em>ActionUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>供使用者下載最新版 Lync 的 URL。如果將 Action 設為 BlockWithUrl 或 AllowWithUrl，此屬性為必要屬性。</p></td>
</tr>
<tr class="even">
<td><p><em>BuildNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>軟體的組建編號。例如，如果您的 Communicator 複本為 2.0.6362.111 版，BuildNumber 即為 6362。組建編號代表軟體開發時的內部軟體版本，它可用來確保您使用的軟體是最終發行版本，而不是預先發行版本。</p></td>
</tr>
<tr class="odd">
<td><p><em>CompareOp</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.CompareOp</p></td>
<td><p>比較運算子，可用來判斷嘗試登入之用戶端軟體的發行時間比規則指定之版本的發行時間早、晚或相同。有效值為：</p>
<p>EQL (等於)</p>
<p>NEQ (不等於)</p>
<p>GTR (大於)</p>
<p>GEQ (大於或等於)</p>
<p>LSS (小於)</p>
<p>LEQ (小於或等於)</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>允許系統管理員提供其他和用戶端版本規則相關的資訊。例如，Description 可包含當您認為該變更規則時，可連絡的連絡人資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否要使用用戶端版本規則。如果將 Enabled 屬性設為 False ($False)，每當使用者嘗試使用指定軟體登入時，系統將忽略規則。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>MajorVersion</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>軟體的主要版本。例如，如果您的 Communicator 複本為 2.0.6362.111 版，MajorVersion 即為 2。主要版本相當於軟體的主要版次。每當您建立新規則時，都必須為 MajorVersion 內容指派值。</p></td>
</tr>
<tr class="even">
<td><p><em>MinorVersion</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>軟體的次要版本。例如，如果您的 Communicator 複本為 2.0.6362.111 版，MinorVersion 即為 0。次要版本相當於軟體的過渡版次。</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>規則的相對優先順序。系統會依照優先順序來處理規則；優先順序為 0 的規則優先處理，優先順序為 1 的規則其次，依此類推。如果您指派的優先順序為使用中的優先順序，新規則會使用該指派的優先順序，而其他規則的優先順序將據此重新排列。</p></td>
</tr>
<tr class="even">
<td><p><em>QfeNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>軟體的快速檢修編號。例如，如果您的 Communicator 複本版本是 2.0.6362.111，則 QfeNumber 為 111。QFE 編號代表規劃在軟體官方版本發行後提供的應用程式更新。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserAgent</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>用來識別軟體用戶端的指示項。例如，OC 是 Communicator 的使用者代理指定。</p></td>
</tr>
<tr class="even">
<td><p><em>UserAgentFullName</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員提供使用者代理的易記名稱。例如，系統管理員可以完整拼出名稱 Microsoft Unified Communications Client，而不是依賴使用者代理 UCCP 來識別代理。</p></td>
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

無。**New-CsClientVersionPolicyRule** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsClientVersionPolicyRule** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Rule 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsClientVersionPolicyRule](get-csclientversionpolicyrule.md)  
[Remove-CsClientVersionPolicyRule](remove-csclientversionpolicyrule.md)  
[Set-CsClientVersionPolicyRule](set-csclientversionpolicyrule.md)

