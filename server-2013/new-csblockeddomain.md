---
title: New-CsBlockedDomain
TOCTitle: New-CsBlockedDomain
ms:assetid: c7b49baf-759b-485f-9391-58584b227fd5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398822(v=OCS.15)
ms:contentKeyID: 49292273
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsBlockedDomain

 

_**上次修改主題的時間：** 2015-03-09_

新增網域到同盟的封鎖網域清單。根據定義，您的使用者無法使用 Lync Server 應用程式與封鎖網域的人員通訊；例如，使用者無法使用 Lync 與封鎖清單上之網域中使用 SIP 帳戶的人員交換立即訊息。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsBlockedDomain -Domain <String> <COMMON PARAMETERS>

    New-CsBlockedDomain -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Comment <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會將 fabrikam.com 網域新增至封鎖網域的清單中。為達成此目的，會先呼叫 **New-CsBlockedDomain** Cmdlet 搭配 Identity 參數，以指派要封鎖之網域的名稱。此外，命令還會加入 Comment 參數，以新增封鎖之網域的相關註解。請注意，如果 fabrikam.com 已存在封鎖或允許的清單中，此命令將會失敗。

    New-CsBlockedDomain -Identity "fabrikam.com" -Comment "Blocked per Ken Myer."

## 範例 2

範例 2 示範如何使用 InMemory 參數，針對原本只存在記憶體中的網域建立新的封鎖網域。在修改這個只存在記憶體中之網域的屬性值之後，接著可呼叫 **Set-CsBlockedDomain** Cmdlet，以將網域新增至封鎖的清單中。

為了執行此工作，命令的第一行會使用 **New-CsBlockedDomain** Cmdlet 搭配 InMemory 參數，以建立 Identity 為 fabrikam.com 的封鎖網域。完成建立後，這個虛擬網域即會儲存於變數 $x 中。

命令的第二行會修改虛擬網域的 Comment 屬性。完成上述作業後，第 3 行會使用 **Set-CsBlockedDomain** Cmdlet 將虛擬網域新增至封鎖的清單中。若未使用第三行的 Cmdlet，虛擬網域便只會存在於記憶體中，且永遠無法新增至封鎖的清單中。反之，當您結束 Windows PowerShell 工作階段或刪除變數 $x 之後，虛擬網域便會立即消失。

    $x = New-CsBlockedDomain -Identity "fabrikam.com" -InMemory
    $x.Comment = "Blocked per Ken Myer."
    Set-CsBlockedDomain -Instance $x

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與第三方主機供應商之間的同盟。

設定與其他組織的直接同盟需要幾項工作。若要開始，必須啟用執行 Lync Server Access Edge 服務的伺服器以允許同盟。此外，另一個組織必須允許與您同盟；雙方必須皆同意同盟關係，才能建立同盟。

若要建立同盟關係，可能也需要管理兩個與同盟相關的清單：允許清單與封鎖清單。允許清單代表您選擇要建立同盟的組織；如果網域出現在允許清單上 (取決於您的組態設定)，您的使用者便能與在該同盟網域中有帳戶的使用者交換立即訊息與目前狀態資訊。相反地，封鎖清單代表明確禁止使用者進行同盟的網域；例如，Lync Server 會自動拒絕從封鎖網域傳送的訊息。

**New-CsBlockedDomain** Cmdlet 可讓您將網域新增至受封鎖的網域清單中。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsBlockedDomain** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsBlockedDomain"}

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
<td><p><em>Domain</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要新增至封鎖清單之網域的 FQDN (例如 fabrikam.com)。您可以使用 Identity 或 Domain 參數 (但不得同時使用) 來指定網域名稱。如果使用 Identity，系統會將 Domain 屬性的值設為指派給 Identity 的值。如果使用 Domain，系統會將 Identity 屬性的值設為指派給 Domain 的值。</p>
<p>請注意，Domain 必須是唯一的：如果指定的網域已存在封鎖或允許的清單中，命令將會失敗。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要新增至封鎖清單之網域的完整網域名稱 (FQDN)，例如 &quot;fabrikam.com&quot;。您可以使用 Identity 或 Domain 參數 (但不得同時使用) 來指定網域名稱。如果使用 Identity，系統會將 Domain 屬性的值設為指派給 Identity 的值。如果使用 Domain，系統會將 Identity 屬性的值設為指派給 Domain 的值。</p>
<p>請注意，Identity 必須是唯一的。如果指定的網域已存在封鎖或允許的清單中，命令將會失敗。</p></td>
</tr>
<tr class="odd">
<td><p><em>Comment</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>選用的字串值，可提供和封鎖之網域相關的額外資訊。例如，您可以加入 Comment 以說明網域遭到封鎖的原因。</p></td>
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
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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

無。**New-CsBlockedDomain** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.BlockedDomain 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsBlockedDomain](get-csblockeddomain.md)  
[Remove-CsBlockedDomain](remove-csblockeddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)  
[Set-CsBlockedDomain](set-csblockeddomain.md)

