---
title: New-CsClientVersionPolicy
TOCTitle: New-CsClientVersionPolicy
ms:assetid: 8c95493a-ce18-49eb-937f-7348743fcbb4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398709(v=OCS.15)
ms:contentKeyID: 49291612
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientVersionPolicy

 

_**上次修改主題的時間：** 2015-03-09_

建立新的用戶端版本原則。用戶端版本原則可讓您指定可以登入您 Lync Server 的系統哪些用戶端版本 (例如 Microsoft Office Communicator 2007 R2)。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsClientVersionPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Rules <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立 Redmond 網站的新用戶端版本原則。由於未指定任何參數 (強制的 Identity 參數除外)，因此新原則將會包含用戶端版本原則的所有預設值。

    New-CsClientVersionPolicy -Identity site:Redmond

## 範例 2

範例 2 所示的命令會針對組織中的每個網站建立新的用戶端版本原則。為了執行此工作，此命令會先呼叫不含任何額外參數的 **Get-CsSite** Cmdlet；這會傳回拓撲中所有網站的集合。接著會將此網站集合管線傳送到 **Select-Object** Cmdlet，以擷取每個網站的 Identity 屬性。然後將這些 Identity 管線傳送到 **ForEach-Object** Cmdlet，以針對集合中的每個網站建立新的用戶端版本原則。

    Get-CsSite | Select-Object Identity | ForEach-Object {New-CsClientVersionPolicy -Identity ("site:" + $_.Identity)}

## 詳細描述

用戶端版本原則代表用戶端版本規則的集合；而用戶端版本規則用於決定允許登入 Lync Server 的用戶端應用程式。當使用者嘗試登入 Lync Server 時，該使用者的用戶端應用程式會傳送 SIP 標頭給伺服器，這個標頭包含與應用程式本身有關的詳細資訊，包括軟體的主要版本和組建編號。然後系統會根據用戶端版本規則的集合，檢查 SIP 標頭所含的版本資訊，查看是否有任何規則要套用至該特定應用程式。如果有這樣的規則，Lync Server 就會採取此規則指定的行動。例如，規則可能會告知 Lync Server 允許登入、封鎖登入，或允許登入，但是會以無訊息方式將用戶端應用程式升級為最新版本 (例如，將 Communicator 2007 R2 升級到 Lync 2013)。

用戶端版本原則 (可套用至全域範圍、網站範圍、服務範圍 (僅登錄器服務)，或個別使用者範圍)，可讓您在決定哪些用戶端應用程式可用來存取系統時，擁有彈性。例如，一般而言，您可能想防止使用者使用 Communicator 2007 R2 登入 Lync Server，因為舊版的用戶端應用程式與 Lync 所支援的功能和特性並不同。但是，由於硬體或軟體衝突，您可能也想選取一組無法升級為 Lync Server 的使用者。在該情況下，您可以建立個別的規則 (以及個別的用戶端版本原則)，允許那些使用者從 Communicator 2007 R2 登入。

但是請注意，匿名使用者僅會受到全域原則的影響。這是因為匿名使用者不會與網站或服務產生關聯，且無法指派個別使用者原則。

您可以使用 **New-CsClientVersionPolicy** Cmdlet 來建立新的用戶端版本規則。這些新原則可以在網站範圍、服務範圍 (僅登錄程式服務) 或個別使用者範圍建立。

請注意，用戶端版本原則不適用於同盟使用者；而是同盟使用者受到本身組織中使用的用戶端版本原則所約束。例如，假設某位同盟使用者使用用戶端 A (此為同盟組織所允許的用戶端)。只要同盟組織允許使用用戶端 A，這個使用者就可以使用該用戶端與您的組織通訊。即使您的用戶端版本原則會封鎖使用用戶端 A，此情況也成立。在您組織中強制執行的用戶端版本原則不會覆寫同盟組織中使用者的用戶端版本原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsClientVersionPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientVersionPolicy\\b"}

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
<td><p>要建立之原則的唯一識別碼。若要建立網站範圍的原則，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要建立服務範圍的原則，請使用類似以下的語法：-Identity &quot;Registrar:atl-cs-001.litwareinc.com&quot;。登錄程式服務是唯一可以主控用戶端版本原則的服務。</p>
<p>在個別使用者範圍也可以建立原則。若要建立個別使用者原則，請使用類似下列的語法：-Identity &quot;SalesDepartmentPolicy&quot;。</p>
<p></p></td>
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
<td><p>可讓您提供有關原則的說明文字。例如，您可以加入應該被指派原則之使用者的資訊。</p></td>
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
<td><p><em>Rules</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>用戶端版本原則規則的集合。您可以使用 <strong>New-CsClientVersionPolicyRule</strong> Cmdlet 和 <strong>Remove-CsClientVersionPolicyRule</strong> Cmdlet，在原則中新增或移除規則。若要在建立新原則時新增規則，請先建立規則並將值儲存在變數中 (例如 $x)。然後，在建立新原則時，就可以使用類似下列的語法：</p>
<p>New-CsClientVersionPolicy –Identity &quot;RedmondClientVersionPolicy&quot; –Rules @{Add=$x}</p></td>
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

無。**Get-CsClientVersionPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsClientVersionPolicy** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionPolicy 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsClientVersionPolicy](get-csclientversionpolicy.md)  
[Grant-CsClientVersionPolicy](grant-csclientversionpolicy.md)  
[Remove-CsClientVersionPolicy](remove-csclientversionpolicy.md)  
[Set-CsClientVersionPolicy](set-csclientversionpolicy.md)

