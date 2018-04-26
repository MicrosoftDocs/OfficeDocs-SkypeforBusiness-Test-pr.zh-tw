---
title: Set-CsAllowedDomain
TOCTitle: Set-CsAllowedDomain
ms:assetid: d5b25b66-2b11-40ef-9ea4-efcae0b610e6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398931(v=OCS.15)
ms:contentKeyID: 49292463
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAllowedDomain

 

_**上次修改主題的時間：** 2015-03-09_

修改同盟核准網域清單中之一或多個網域的屬性值。當網域通過同盟核准 (藉由將網域加入允許清單中) 後，您的使用者就可以和具有同盟網域帳戶的人員交換立即訊息及目前狀態資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsAllowedDomain [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsAllowedDomain [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Comment <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MarkForMonitoring <$true | $false>] [-ProxyFqdn <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改 Identity 為 "fabrikam.com" 之允許網域的 Comment 屬性。作法是加入 Comment 參數搭配適當的屬性值："Contact:Ken Myer (kenmyer@fabrikam.com)"。

    Set-CsAllowedDomain -Identity fabrikam.com -Comment "Contact: Ken Myer (kenmyer@fabrikam.com)"

## 範例 2

範例 2 會針對其 Identity 的任何部分含有 "fabrikam" 字串值的所有允許網域，修改 Comment 和 MarkForMonitoring 屬性。為了執行此工作，命令會先呼叫 **Get-CsAllowedDomain** Cmdlet 搭配 Filter 參數。篩選值 "\*fabrikam\*" 會指示 **Get-CsAllowedDomain** Cmdlet，以傳回 Identity 包含 "fabrikam" 字串值的所有網域 (例如，此命令會傳回如 fabrikam.com、us.fabrikam.net 及 fabrikam-users.org 等網域)。然後將篩選後的集合管線傳送到 **Set-CsAllowedDomain** Cmdlet，以修改集合中每一個項目的 Comment 屬性，並將 MarkForMonitoring 屬性設為 True ($True)。

    Get-CsAllowedDomain -Filter *fabrikam* | Set-CsAllowedDomain -Comment "Contact: Ken Myer (kenmyer@fabrikam.com)" -MarkForMonitoring $True

## 範例 3

範例 3 所示的命令會修改允許清單中目前不受監控伺服器監控的所有網域 (即所有 MarkForMonitoring 屬性設為 False 的網域)。為達成此目的，會呼叫不含任何其他參數的 **Get-CsAllowedDomain** Cmdlet，以擷取允許清單中所有網域的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 MarkForMonitoring 屬性等於 False 的網域。接著將篩選後的集合管線傳送到 **Set-CsAllowedDomain** Cmdlet，以將集合中每一個網域的 MarkForMonitoring 屬性設為 True。

    Get-CsAllowedDomain | Where-Object {$_.MarkForMonitoring -eq $False} | Set-CsAllowedDomain -MarkForMonitoring $True

## 範例 4

範例 4 會將一般註解 ("Need contact information.") 新增至允許清單中 Comment 屬性目前沒有值的網域。為了執行此工作，命令會先呼叫 **Get-CsAllowedDomain** Cmdlet，以擷取允許清單中所有網域的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 Comment 屬性等於 Null 值的網域。接著將該篩選後的集合管線傳送到 **Set-CsAllowedDomain** Cmdlet，以修改集合中每一個項目的 Comment 屬性。

    Get-CsAllowedDomain | Where-Object {$_.Comment -eq $Null} | Set-CsAllowedDomain -Comment "Need contact information."

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與第三方主機供應商之間的同盟。

設定與其他組織的直接同盟需要幾項工作。若要開始，必須啟用執行 Lync Server Access Edge 服務的伺服器以允許同盟。此外，另一個組織必須允許與您同盟；雙方必須皆同意同盟關係，才能建立同盟。

若要設定同盟關係，您也可能需要管理兩個同盟相關清單：允許清單與封鎖清單。允許清單代表您選擇要建立同盟的組織。如果網域出現在允許清單上 (視組態設定而定)，則使用者能夠與在該同盟網域中具有帳戶的使用者交換立即訊息和目前狀態資訊。相反地，封鎖清單代表明確禁止使用者進行同盟的網域；例如，Lync Server 會自動拒絕從封鎖網域傳送的訊息。

**Set-CsAllowedDomain** Cmdlet 可讓您為允許網域清單中的任何網域修改屬性值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsAllowedDomain** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAllowedDomain"}

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
<td><p><em>Comment</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>選用的字串值，可提供和待修改之網域相關的額外資訊。例如，您可以加入 Comment 以提供同盟網域的連絡人資訊。</p></td>
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
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改內容值之允許網域的完整網域名稱 (FQDN)。例如：</p>
<p>-Identity fabrikam.com</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>封鎖的網域物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>MarkForMonitoring</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否讓 監控伺服器 監控網域和遠端網域間的同盟連線。根據預設，MarkForMonitoring 設為 False，這表示連線不受到監控。</p>
<p>如果您尚未部署 監控伺服器，此屬性將會被略過。</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要新增至允許清單之網域中部署的 SIP Proxy 伺服器完整網域名稱 (例如 proxy-server.fabrikam.com)。此屬性為選用屬性：若未指定，則會使用 DNS SRV 探索程序來判斷 SIP Proxy 伺服器的位置。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowedDomain 物件。**Set-CsAllowedDomain** Cmdlet 接受允許之網域物件管線傳送的執行個體。

## 傳回類型

**Set-CsAllowedDomain** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowedDomain 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAllowedDomain](get-csalloweddomain.md)  
[New-CsAllowedDomain](new-csalloweddomain.md)  
[Remove-CsAllowedDomain](remove-csalloweddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

