---
title: Remove-CsClientVersionPolicyRule
TOCTitle: Remove-CsClientVersionPolicyRule
ms:assetid: 71a107c9-5499-460f-b4b8-08b368be9321
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398541(v=OCS.15)
ms:contentKeyID: 49291286
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClientVersionPolicyRule

 

_**上次修改主題的時間：** 2015-03-09_

移除一或多個設定供組織使用的用戶端版本原則規則。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsClientVersionPolicyRule -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除 Identity 為 site:Redmond/74ba9211-8610-42f9-91ba-846cdee98820 的用戶端版本原則規則。由於 Identity 必須是唯一的，因此這個命令最多只會刪除單一規則。

    Remove-CsClientVersionPolicyRule -Identity site:Redmond/74ba9211-8610-42f9-91ba-846cdee98820

## 範例 2

範例 2 會刪除已針對 Redmond 網站設定的所有用戶端版本原則規則。為達成此目的，命令會先呼叫 **Get-CsClientVersionPolicyRule** Cmdlet 並搭配 Filter 參數；"site:Redmond/\*" 篩選值會將傳回的資料限制在 Identity 開頭為 "site:Redmond/" 字串值的原則規則。接著將篩選後的集合管線傳送到 **Remove-CsClientVersionPolicyRule** Cmdlet，以刪除該集合中的每個項目。

    Get-CsClientVersionPolicyRule -Filter "site:Redmond/*" | Remove-CsClientVersionPolicyRule

## 範例 3

範例 3 會刪除目前已停用的所有用戶端版本原則規則。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsClientVersionPolicyRule** Cmdlet，以傳回組織目前所使用之所有原則規則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 Enabled 屬性等於 False 的所有規則。接著將篩選後的集合管線傳送到 **Remove-CsClientVersionPolicyRule** Cmdlet，以刪除該集合中的每個項目。

    Get-CsClientVersionPolicyRule | Where-Object {$_.Enabled -eq $False} | Remove-CsClientVersionPolicyRule

## 詳細描述

用戶端版本規則可用來判斷允許登入 Lync Server 的用戶端應用程式。當使用者嘗試登入 Lync Server 時，該使用者的用戶端應用程式會傳送 SIP 標頭給伺服器，此標頭包含與應用程式本身有關的詳細資訊，包括軟體的主要版本和組建編號。接著，系統會根據用戶端版本規則的集合檢查版本資訊，以查看是否有任何規則適用於該特定應用程式。例如，假設某位使用者嘗試使用 Microsoft Office Communicator 2007 R2 登入。在使用者開始登入之前，系統會檢查是否有適用於 Office Communicator 2007 R2 的用戶端版本規則。若有這樣的規則， Lync Server 就會採取此規則指定的行動。該動作必須是下列其中一項：

Allow。允許使用者登入。

AllowAndUpgrade。允許使用者登入，並自動將使用者的 Communicator 2007 R2 複本升級為最新版本的 Lync。會視您設定系統的方式而定，使用 Microsoft Update 或 Windows Server Update Services 執行升級。

AllowWithUrl。允許使用者登入，並顯示訊息以指出使用者可以下載及安裝 Lync 最新版本的 URL。該 URL 必須指向您自己建立的網站；而不是指向安裝 Lync Server 時系統為您建立的網站。

Block。不允許使用者登入。

BlockAndUpgrade。不允許使用者登入，但會自動將使用者的 Communicator 2007 R2 複本升級為最新版本的 Lync。接下來，使用者便能嘗試使用新的用戶端應用程式登入。會視您設定系統的方式而定，使用 Microsoft Update 或 Windows Server Update Services 執行升級。

BlockWithUrl。不允許使用者登入，但會顯示訊息以指出使用者可下載及安裝最新版本之 Lync 的 URL。該 URL 必須指向您自己建立的網站；而不是指向安裝 Lync Server 時系統為您建立的網站。

系統會將用戶端版本規則收集在用戶端版本原則中；用戶端版本原則是一種可在全域範圍、網站範圍、服務範圍 (登錄器服務) 或個別使用者範圍內設定的原則。 **Remove-CsClientVersionPolicyRule** Cmdlet 可讓您刪除一或多個設定為在組織中使用的用戶端原則規則。這些規則可以從您的任何用戶端版本原則中刪除，包括全域原則。

請注意，用戶端版本原則不適用於同盟使用者；而是同盟使用者受到本身組織中使用的用戶端版本原則所約束。例如，假設某位同盟使用者使用用戶端 A (此為同盟組織所允許的用戶端)。只要同盟組織允許使用用戶端 A，這個使用者就可以使用該用戶端與您的組織通訊。即使您的用戶端版本原則會封鎖使用用戶端 A，此情況也成立。在您組織中強制執行的用戶端版本原則不會覆寫同盟組織中使用者的用戶端版本原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsClientVersionPolicyRule** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientVersionPolicyRule"}

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
<td><p>要移除之用戶端版本原則規則的唯一識別碼。用戶端版本規則的 Identity 是由設定此規則的範圍加上全域唯一識別碼 (GUID) 組成。也就是說，規則所擁有的 Identity 類似如下：site:Redmond/1987d3c2-4544-489d-bbe3-59f79f530a83。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Rule 物件。**Remove-CsClientVersionPolicyRule** Cmdlet 接受管線傳送的用戶端版本規則物件執行個體。

## 傳回類型

無。反之， **Remove-CsClientVersionPolicyRule** Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Rule 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsClientVersionPolicyRule](get-csclientversionpolicyrule.md)  
[New-CsClientVersionPolicyRule](new-csclientversionpolicyrule.md)  
[Set-CsClientVersionPolicyRule](set-csclientversionpolicyrule.md)

