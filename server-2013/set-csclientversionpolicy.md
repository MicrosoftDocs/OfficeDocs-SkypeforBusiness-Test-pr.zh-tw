---
title: Set-CsClientVersionPolicy
TOCTitle: Set-CsClientVersionPolicy
ms:assetid: cf7c1a6c-b8a9-4609-97f4-6c8ef9e45be7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398876(v=OCS.15)
ms:contentKeyID: 49292365
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientVersionPolicy

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的用戶端版本原則。用戶端版本原則可讓您指定可以登入您 Lync Server 系統的用戶端 (如 Microsoft Office Communicator 2007 R2)。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsClientVersionPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClientVersionPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-Rules <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將某個用戶端版本原則中的所有用戶端版本規則複製到另一個用戶端版本原則中。為達成此目的，範例中的第一個命令會使用 **Set-CsClientVersionPolicy** Cmdlet，以移除原則 site:Redmond 中的所有規則；作法是將 Rules 屬性的值設為 Null。刪除規則之後，範例中的第二個命令會使用 **Get-CsClientVersionPolicy** Cmdlet，以擷取所有針對 site:Dublin 原則設定的用戶端版本原則規則。這些規則會儲存於名為 $x 的變數中。

最後一個命令會再次叫用 **Set-CsClientVersionPolicy** Cmdlet，這次會將 Redmond 原則的 Rules 屬性設為 $x。如此便能有效率地複製 site:Dublin 原則中的所有規則，然後將這些規則新增至 site:Redmond 原則中。

    Set-CsClientVersionPolicy -Identity site:Redmond -Rules $Null
    
    $x = Get-CsClientVersionPolicy -Identity site:Dublin | Select-Object -ExpandProperty Rules
    
    Set-CsClientVersionPolicy -Identity site:Redmond -Rules $x

## 詳細描述

用戶端版本原則代表用戶端版本規則的集合；而用戶端版本規則用於決定允許登入 Lync Server 的用戶端應用程式。當使用者嘗試登入 Lync Server 時，該使用者的用戶端應用程式會傳送 SIP 標頭給伺服器，這個標頭包含與應用程式本身有關的詳細資訊，包括軟體的主要版本和組建編號。然後系統會根據用戶端版本規則的集合，檢查 SIP 標頭所含的版本資訊，查看是否有任何規則要套用至該特定應用程式。如果有這樣的規則，Lync Server 就會採取此規則指定的行動。例如，規則可能會告知 Lync Server 允許登入、封鎖登入，或允許登入，但是會以無訊息方式將用戶端應用程式升級為最新版本 (例如，將 Communicator 2007 R2 升級到 Lync 2013)。

用戶端版本原則 (可套用至全域範圍、網站範圍、服務範圍 (僅登錄器服務)，或個別使用者範圍)，可讓您在決定哪些用戶端應用程式可用來存取系統時，擁有彈性。例如，您可能想防止使用者使用 Communicator 2007 R2 登入 Lync Server，畢竟它與 Lync 所支援的功能和特性並不同。但是，由於硬體或軟體衝突，您可能有一群不能升級為 Lync 的使用者。在該情況下，您可以建立個別的規則 (以及個別的用戶端版本原則)，允許那些使用者從 Communicator 2007 R2 登入。

您可以隨時修改用戶端版本原則。修改用戶端版本原則通常是指新增規則、刪除現有的規則，或修改現有規則的屬性 (例如，將規則動作從「允許」變更為「封鎖」)。這些變更都能藉由使用 **Set-CsClientVersionPolicy** Cmdlet 完成。但是，您可能會發現使用 **CsClientVersionPolicyRule** Cmdlet 可以更輕鬆地進行這些修改。

另一方面， **Set-CsClientVersionPolicy** Cmdlet 可以讓您輕易地將某個用戶端版本原則的一整組規則複製到另一個用戶端版本原則。如需詳細資訊，請參閱本說明主題中的＜範例＞一節。

請注意，用戶端版本原則不適用於同盟使用者；而是同盟使用者受到本身組織中使用的用戶端版本原則所約束。例如，假設某位同盟使用者使用用戶端 A (此為同盟組織所允許的用戶端)。只要同盟組織允許使用用戶端 A，這個使用者就可以使用該用戶端與您的組織通訊。即使您的用戶端版本原則會封鎖使用用戶端 A，此情況也成立。在您組織中強制執行的用戶端版本原則不會覆寫同盟組織中使用者的用戶端版本原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsClientVersionPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientVersionPolicy\\b"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您提供原則的相關說明資訊。例如，您可以藉由提供資訊來描述應接受原則指派的使用者。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之原則的唯一識別碼。若要修改全域原則，請使用下列語法：-Identity global。若要修改在網站範圍設定的原則，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要修改在服務範圍設定的原則，請使用類似下列的語法：-Identity &quot;Registrar:atl-cs-001.litwareinc.com&quot;。登錄器服務是唯一能主控用戶端版本原則的服務。</p>
<p>您也可以使用這個 Cmdlet 修改個別使用者原則。若要修改個別使用者原則，請使用類似下列的語法：-Identity &quot;SalesDepartmentPolicy&quot;。</p>
<p>如果未加入此參數，則 <strong>Set-CsClientVersionPolicy</strong> Cmdlet 將會修改全域原則。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>ClientVersionPolicy 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>Rules</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>個別用戶端原則規則的集合，這些用戶端原則規則皆已指派給原則。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionPolicy 物件。 **Remove-CsClientVersionPolicy** Cmdlet 接受管線傳送的用戶端版本原則物件執行個體。

## 傳回類型

**Set-CsClientVersionPolicy** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsClientVersionPolicy](get-csclientversionpolicy.md)  
[New-CsClientVersionPolicy](new-csclientversionpolicy.md)  
[Remove-CsClientVersionPolicy](remove-csclientversionpolicy.md)  
[Set-CsClientVersionPolicy](set-csclientversionpolicy.md)

