---
title: Get-CsAllowedDomain
TOCTitle: Get-CsAllowedDomain
ms:assetid: 0b693788-2270-4bf3-b899-f5cf4321351b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398164(v=OCS.15)
ms:contentKeyID: 49290050
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAllowedDomain

 

_**上次修改主題的時間：** 2015-03-09_

傳回同盟之核准網域清單中所含之網域的資訊。當網域通過同盟核准 (藉由加入允許清單中) 後，您的使用者即可與使用該網域帳戶的人員交換立即訊息及目前狀態資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAllowedDomain [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsAllowedDomain [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回已核准同盟之網域清單中包含的所有網域集合。呼叫不含任何參數的 **Get-CsAllowedDomain** Cmdlet 一律會傳回核准網域的完整集合。

    Get-CsAllowedDomain

## 範例 2

範例 2 會傳回關於 Identity 為 "fabrikam.com" 之核准網域的資訊。由於識別身分必須是唯一的，因此這個命令永遠不會傳回一個以上的項目。

    Get-CsAllowedDomain -Identity fabrikam.com

## 範例 3

範例 3 所示的命令會傳回其 Identity 中任何位置有字串值 "fabrikam" 的所有核准網域集合。為達成此目的，命令會使用 Filter 參數與篩選值 "\*fabrikam\*"。此篩選值會指示 **Get-CsAllowedDomain** Cmdlet 只傳回 Identity (您篩選可依據的唯一屬性) 包含字串值 "fabrikam" 的網域。此命令將傳回 fabrikam.com、fabrikam.net 以及 africa.fabrikam.org 之類的網域。

    Get-CsAllowedDomain -Filter *fabrikam*

## 範例 4

在範例 4 中，**Get-CsAllowedDomain** Cmdlet 和 **Where-Object** Cmdlet 用來傳回未針對 ProxyFqdn 屬性輸入任何值之所有網域的集合。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsAllowedDomain** Cmdlet，以傳回所有核准網域的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 ProxyFqdn 屬性等於 Null 值的允許網域；Null 值表示 ProxyFqdn 中未輸入任何值。若要尋找 ProxyFqdn 屬性中已設定某值的所有網域，請改用下列語法：

Where-Object {$\_.ProxyFqdn -ne $Null}

    Get-CsAllowedDomain | Where-Object {$_.ProxyFqdn -eq $Null}

## 範例 5

範例 5 會傳回已由監控伺服器檢查其運作情況狀態的所有允許網域。為達成此目的，命令會先使用 **Get-CsAllowedDomain** Cmdlet 傳回核准網域清單上所有網域的集合。然後，該集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 MarkForMonitoring 屬性等於 True 的網域。

    Get-CsAllowedDomain | Where-Object {$_.MarkForMonitoring -eq $True}

## 詳細描述

「同盟」是兩個組織可建立信任關係的一種方法，此信任關係會簡化兩個團體之間的通訊。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您的組織與其他組織之間的直接同盟；2) 您的組織與公用提供者之間的同盟；以及 3) 您的組織與第三方主機供應商之間的同盟。

設定與其他組織間的直接同盟包含幾個工作。首先，您必須啟用 Access Edge Server 以允許同盟。此外，另一個組織必須允許與您同盟；除非雙方都同意該關係，否則無法建立同盟。

若要設定同盟關係，您也可能需要管理兩個同盟相關清單：允許清單和封鎖清單。允許清單 (如果 EnablePartnerDiscovery 已停用，則為必要) 代表您選擇要結盟的組織。如果網域出現在允許清單上 (視組態設定而定)，則使用者能夠與在該同盟網域中具有帳戶的使用者交換立即訊息和目前狀態資訊。相反地，封鎖清單代表明確禁止使用者進行同盟的網域；例如，Lync Server 會自動拒絕從封鎖網域傳送的訊息。

**Get-CsAllowedDomain** Cmdlet 可讓您傳回有關允許網域清單上所有網域的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsAllowedDomain** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAllowedDomain"}

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
<td><p>System.String</p></td>
<td><p>可讓您使用萬用字元傳回允許網域清單中的一或多個網域。若要傳回其 Identity 開頭為字母 &quot;r' 的所有網域，請使用下列語法：-Filter r*。若要傳回其 Identity 結尾為 &quot;.net&quot; 的所有網域，請使用下列語法：-Filter &quot;*.net&quot;。若要傳回其 Identity 開頭為字母 &quot;r&quot; 或字母 &quot;g&quot; 的所有網域，請使用下列語法：-Filter [rg]*。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回之網域的名稱。允許清單上的網域依完整網域名稱 (FQDN) 列出；這表示指定之網域的 Identity 會類似 fabrikam.com 或 contoso.net。請注意，指定網域 Identity 時，您不能使用萬用字元。若要使用萬用字元傳回指定網域 (或一組網域)，請改用 Filter 參數。</p>
<p>若未指定此參數，則會傳回允許網域清單上的所有網域。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取允許的網域，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsAllowedDomain** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowedDomain 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsAllowedDomain](new-csalloweddomain.md)  
[Remove-CsAllowedDomain](remove-csalloweddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)  
[Set-CsAllowedDomain](set-csalloweddomain.md)

