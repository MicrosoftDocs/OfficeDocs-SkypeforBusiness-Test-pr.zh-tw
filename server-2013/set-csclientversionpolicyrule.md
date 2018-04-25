---
title: Set-CsClientVersionPolicyRule
TOCTitle: Set-CsClientVersionPolicyRule
ms:assetid: 2e061fa8-bb1a-4382-bb0d-298f81aefb3d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425790(v=OCS.15)
ms:contentKeyID: 49290455
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientVersionPolicyRule

 

_**上次修改主題的時間：** 2015-03-09_

修改一或多個目前設定供組織使用的用戶端版本原則規則。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsClientVersionPolicyRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClientVersionPolicyRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Action <Allow | AllowAndUpgrade | AllowWithUrl | Block | BlockAndUpgrade | BlockWithUrl>] [-ActionUrl <String>] [-BuildNumber <UInt16>] [-CompareOp <EQL | NEQ | GTR | GEQ | LSS | LEQ>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-MajorVersion <UInt16>] [-MinorVersion <UInt16>] [-Priority <Int32>] [-QfeNumber <UInt16>] [-UserAgent <String>] [-UserAgentFullName <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會停用 Identity 為 site:Redmond/74ba9211-8610-42f9-91ba-846cdee98820 的用戶端版本原則規則。若要停用規則，則在命令中加入 Enabled 參數和參數值 $False。

    Set-CsClientVersionPolicyRule -Identity site:Redmond/74ba9211-8610-42f9-91ba-846cdee98820 -Enabled $False

## 範例 2

範例 2 會為指派給 Redmond 網站的所有用戶端版本原則規則新增一般描述。為達成此目的，命令會先呼叫 **Get-CsClientVersionPolicyRule** Cmdlet 搭配 Filter 參數；篩選值 "site:Redmond\*" 可將傳回的資料限制在指派給 Redmond 網站的原則規則)。然後，此集合會管線傳送到 **Set-CsClientVersionPolicyRule** Cmdlet，以將描述「Redmond 的用戶端原則規則」指派給該集合中的每個項目。

    Get-CsClientVersionPolicyRule -Filter "site:Redmond*" | Set-CsClientVersionPolicyRule -Description "Client policy rules for Redmond"

## 範例 3

範例 3 會針對參考 UCCP 做為使用者代理的任何用戶端版本原則規則，封鎖整合通訊用戶端平台 (UCCP) 用戶端的使用。為了執行此工作，命令會先呼叫 **Get-CsClientVersionPolicyRule** Cmdlet 擷取目前所使用之所有用戶端原則規則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 UserAgent 屬性等於 (-eq) UCCP 的規則。接著將篩選後的集合管線傳送到 **Set-CsClientVersionPolicyRule** Cmdlet，以取得集合中的每個項目，並將 Action 屬性設為 Block。

    Get-CsClientVersionPolicyRule | Where-Object {$_.UserAgent -eq "UCCP"} | Set-CsClientVersionPolicyRule -Action "Block"

## 詳細描述

用戶端版本規則可用來判斷允許登入 Lync Server 的用戶端應用程式。當使用者嘗試登入 Lync Server 時，該使用者的用戶端應用程式會傳送 SIP 標頭給伺服器，這個標頭包含與應用程式本身有關的詳細資訊，包括軟體的主要版本和組建編號。接著，系統會根據用戶端版本規則的集合檢查版本資訊，以查看是否有任何規則適用於該特定應用程式。例如，假設某位使用者嘗試使用 Microsoft Office Communicator 2007 R2 登入。在使用者可以登入 Lync Server 之前，系統會檢查是否有適用於 Office Communicator 2007 R2 的用戶端版本規則。如果有這樣的規則， Lync Server 就會採取此規則指定的行動。該動作必須是下列其中一項：

Allow。允許使用者登入。

AllowAndUpgrade。允許使用者登入，並自動將使用者的 Communicator 2007 R2 複本升級為最新版本的 Lync。會視您設定系統的方式而定，使用 Microsoft Update 或 Windows Server Update Services 執行升級。

AllowWithUrl。允許使用者登入，並顯示訊息以指出使用者可以下載及安裝 Lync 最新版本的 URL。該 URL 必須指向您自己建立的網站；而不是指向安裝 Lync Server 時系統為您建立的網站。

Block。不允許使用者登入。

BlockAndUpgrade。不允許使用者登入，但會自動將使用者的 Communicator 2007 R2 複本升級為最新版本的 Lync。接下來，使用者便能嘗試使用新的用戶端應用程式登入。會視您設定系統的方式而定，使用 Microsoft Update 或 Windows Server Update Services 執行升級。

BlockWithUrl。不允許使用者登入，但會顯示訊息以指出使用者可下載及安裝最新版本之 Lync 的 URL。該 URL 必須指向您自己建立的網站；而不是指向安裝 Lync Server 時系統為您建立的網站。

系統會將用戶端版本規則收集在用戶端版本原則中。用戶端版本原則是一種可在全域範圍、網站範圍、服務範圍 (登錄器服務) 或個別使用者範圍內設定的原則。 **Set-CsClientVersionPolicyRule** Cmdlet 提供了一種方式，讓您修改現有用戶端版本規則的屬性。

請注意，用戶端版本原則不適用於同盟使用者；而是同盟使用者受到本身組織中使用的用戶端版本原則所約束。例如，假設某位同盟使用者使用用戶端 A (此為同盟組織所允許的用戶端)。只要同盟組織允許使用用戶端 A，這個使用者就可以使用該用戶端與您的組織通訊。即使您的用戶端版本原則會封鎖使用用戶端 A，此情況也成立。在您組織中強制執行的用戶端版本原則不會覆寫同盟組織中使用者的用戶端版本原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsClientVersionPolicyRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientVersionPolicyRule"}

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
<tr class="even">
<td><p><em>ActionUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>供使用者下載最新版 Lync 的 URL。如果將 Action 設為 BlockWithUrl 或 AllowWithUrl，此屬性為必要屬性。</p></td>
</tr>
<tr class="odd">
<td><p><em>BuildNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>軟體的組建編號。例如，如果您的 Communicator 複本為 2.0.6362.111 版，BuildNumber 即為 6362。組建編號代表軟體開發時的內部軟體版本，它可用來確保您使用的軟體是最終發行版本，而不是預先發行版本。</p></td>
</tr>
<tr class="even">
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
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>允許系統管理員提供其他和用戶端版本規則相關的資訊。例如，Description 可包含當您認為該變更規則時，可連絡的連絡人資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否要使用用戶端版本規則。如果將 Enabled 屬性設為 False，每當使用者嘗試使用指定軟體登入時，系統將忽略規則。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之用戶端版本原則規則的唯一識別碼。用戶端版本規則的 Identity 是由設定此規則的範圍加上全域唯一識別碼 (GUID) 組成。也就是說，規則所擁有的 Identity 類似如下：site:Redmond/1987d3c2-4544-489d-bbe3-59f79f530a83。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>規則物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>MajorVersion</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>軟體的主要版本。例如，如果您的 Communicator 複本為 2.0.6362.111 版，MajorVersion 即為 2。主要版本相當於軟體的主要版次。</p></td>
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
<td><p>規則的相對優先順序。規則是依照優先順序進行處理，先處理優先順序為 0 的規則，接下來處理優先順序為 1 的規則，依此類推。如果您指派的優先順序已在使用中，新的規則將會使用該優先順序，而其他規則會依此重新編號。</p></td>
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
<td><p>用於識別軟體用戶端的指示項。例如，OC 是 Communicator 的使用者代理指定。 <strong>Get-CsClientVersionConfiguration</strong> Cmdlet 可為每個使用者代理指定提供對應的易記名稱。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Rule 物件。**Set-CsClientVersionPolicyRule** Cmdlet 接受管線傳送的用戶端版本規則物件執行個體。

## 傳回類型

無。反之， **Set-CsClientVersionPolicyRule** Cmdlet 會修改 Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Rule 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsClientVersionPolicyRule](get-csclientversionpolicyrule.md)  
[New-CsClientVersionPolicyRule](new-csclientversionpolicyrule.md)  
[Set-CsClientVersionPolicyRule](set-csclientversionpolicyrule.md)

