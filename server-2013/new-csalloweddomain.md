---
title: New-CsAllowedDomain
TOCTitle: New-CsAllowedDomain
ms:assetid: 7e040cf8-8e6f-4293-b7c4-1be76053d43d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398628(v=OCS.15)
ms:contentKeyID: 49291445
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAllowedDomain

 

_**上次修改主題的時間：** 2015-03-09_

將網域新增至已核准進行同盟的網域清單。當網域通過同盟核准 (藉由將網域加入允許清單中) 後，您的使用者就可以和具有同盟網域帳戶的人員交換立即訊息及目前狀態資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsAllowedDomain -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    New-CsAllowedDomain -Domain <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Comment <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MarkForMonitoring <$true | $false>] [-ProxyFqdn <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，可將 fabrikam.com 網域新增至允許網域的清單中。為達此目的，會呼叫 **New-CsAllowedDomain** Cmdlet 搭配 Identity 參數 (此參數可指派要新增至允許清單的網域名稱)。請注意，若 fabrikam.com 已在允許或封鎖的清單中，此命令會失敗。

    New-CsAllowedDomain -Identity "fabrikam.com"

## 範例 2

範例 2 是範例 1 所示命令的變化。但此範例會加入兩個額外的參數及 Identity，其中 ProxyFqdn 可用來指定 fabrikam.com 之 Proxy 伺服器的 FQDN，而 MarkForMonitoring 則可用來將此同盟連線新增至 監控伺服器 所監控的項目清單。

    New-CsAllowedDomain -Identity "fabrikam.com" -ProxyFqdn "proxyserver.fabrikam.com" -MarkForMonitoring $True -Comment "Contact: Ken Myer (kenmyer@fabrikam.com)"

## 範例 3

範例 3 示範如何使用 InMemory 參數建立一開始僅存在於記憶體中的新允許網域。當您修改這個僅在記憶體中之網域的屬性值之後，接著可以呼叫 **Set-CsAllowedDomain** Cmdlet 以將網域新增至允許清單。

為達此目的，範例中的第一個命令會使用 **New-CsAllowedDomain** Cmdlet 和 InMemory 參數建立 Identity 為 fabrikam.com 的允許網域。建立之後，會將此虛擬網域儲存在變數 $x 中。

第 2、3 及 4 行分別用來修改 ProxyFqdn、MarkForMonitoring 及 Comment 屬性的值。修改完所有屬性值之後，最後一個命令會使用 **Set-CsAllowedDomain** Cmdlet 將虛擬網域新增至允許網域清單。請記住，在呼叫 **Set-CsAllowedDomain** Cmdlet 之前，fabrikam.com 只存在於記憶體中：如果您在範例的最後一行之前就執行 **Get-CsAllowedDomain** Cmdlet，fabrikam.com 將不會出現在允許網域清單中。只有在呼叫 **Set-CsAllowedDomain** Cmdlet 之後，Fabrikam.com 才會出現在允許清單中。

    $x = New-CsAllowedDomain -Identity "fabrikam.com" -InMemory
    $x.ProxyFqdn = "proxyserver.fabrikam.com" 
    $x.MarkForMonitoring = $True 
    $x.Comment = "Contact: Ken Myer (kenmyer@fabrikam.com)"
    Set-CsAllowedDomain -Instance $x

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與第三方主機供應商之間的同盟。

設定與其他組織的直接同盟需要幾項工作。若要開始，必須啟用執行 Lync Server Access Edge 服務的伺服器以允許同盟。此外，另一個組織必須允許與您同盟；雙方必須皆同意同盟關係，才能建立同盟。

若要建立同盟關係，可能也需要管理兩個與同盟相關的清單：允許清單與封鎖清單。允許清單代表您選擇要建立同盟的組織；如果網域出現在允許清單上 (取決於您的組態設定)，您的使用者便能與在該同盟網域中有帳戶的使用者交換立即訊息與目前狀態資訊。相反地，封鎖清單代表明確禁止使用者進行同盟的網域；例如， Lync Server 會自動拒絕從封鎖網域傳送的訊息。

如果您要建立新的同盟關係，可以使用 **New-CsAllowedDomain** Cmdlet 將網域新增至允許網域清單。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsAllowedDomain** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsAllowedDomain"}

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
<td><p>System.Strkng</p></td>
<td><p>要新增至允許清單之網域的 FQDN (例如 fabrikam.com)。您可以使用 Identity 或 Domain 參數 (但不得同時使用) 來指定網域名稱。如果使用 Identity，系統會將 Domain 屬性的值設為指派給 Identity 的值。如果使用 Domain，系統會將 Identity 屬性的值設為指派給 Domain 的值。</p>
<p>請注意，Domain 必須是唯一的：如果指定的網域已存在封鎖或允許的清單中，命令將會失敗。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要新增至允許清單之網域的完整網域名稱 (FQDN)；例如 fabrikam.com。您可以使用 Identity 或 Domain 參數 (但不得同時使用) 來指定網域名稱。如果使用 Identity，系統會將 Domain 屬性的值設為指派給 Identity 的值。如果使用 Domain，系統會將 Identity 屬性的值設為指派給 Domain 的值。</p>
<p>請注意，Identity 必須是唯一的：如果指定的網域已存在封鎖或允許的清單中，命令將會失敗。</p></td>
</tr>
<tr class="odd">
<td><p><em>Comment</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>提供有關要新增至允許清單之網域的其他相關資訊的選用字串值。例如，您可以新增一個 Comment，提供同盟網域的連絡資訊。</p></td>
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
<td><p><em>MarkForMonitoring</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否讓監控伺服器監控網域和遠端網域間的同盟連線。根據預設，MarkForMonitoring 設為 False，表示不監控連線。</p>
<p>如果您尚未部署監控伺服器，則會忽略這個屬性。</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要新增至允許清單之網域中部署的 SIP Proxy 伺服器的 FQDN (例如 proxy-server.fabrikam.com)。此為選用屬性：若未指定，則會使用 DNS SRV 探索程序來判斷 SIP Proxy 伺服器的位置。</p></td>
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

無。**New-CsAllowedDomain** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowedDomain 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAllowedDomain](get-csalloweddomain.md)  
[Remove-CsAllowedDomain](remove-csalloweddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)  
[Set-CsAllowedDomain](set-csalloweddomain.md)

