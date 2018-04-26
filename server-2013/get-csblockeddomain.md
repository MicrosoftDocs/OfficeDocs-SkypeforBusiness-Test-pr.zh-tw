---
title: Get-CsBlockedDomain
TOCTitle: Get-CsBlockedDomain
ms:assetid: 5fa2c2a3-b5e4-430c-970a-0c506a6924b5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398424(v=OCS.15)
ms:contentKeyID: 49291070
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsBlockedDomain

 

_**上次修改主題的時間：** 2015-03-09_

傳回同盟之封鎖網域清單中所含網域的資訊。根據定義，您的使用者無法使用 Lync Server 應用程式與封鎖網域的人員通訊；例如，使用者無法使用 Lync 與在封鎖清單上之網域中使用工作階段初始通訊協定 (SIP) 帳戶的人員交換立即訊息。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsBlockedDomain [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsBlockedDomain [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回包含在封鎖網域清單上所有網域的集合。這可以透過呼叫不含任何額外參數的 **Get-CsBlockedDomain** Cmdlet 來完成。

    Get-CsBlockedDomain

## 範例 2

在範例 2 中，唯一傳回的是 Identity 為 "fabrikam.com" 的封鎖網域。封鎖清單上的網域必須擁有唯一識別碼，因此這個命令最多傳回一個原則。

    Get-CsBlockedDomain -Identity fabrikam.com

## 範例 3

範例 3 會使用 Filter 參數傳回 Identity 結尾為字串值 ".net" 之所有封鎖網域的集合。此範例命令會傳回如 northwindtraders.net、contoso.net 以及 fabrikam.net 之類的網域。

    Get-CsBlockedDomain -Filter *.net

## 範例 4

範例 4 會傳回 Comment 屬性不含值之所有網域的集合。為達成此目的，命令會先使用 **Get-CsBlockedDomain** Cmdlet 傳回封鎖清單上所有網域的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 Comment 屬性等於 Null 值的網域。

    Get-CsBlockedDomain | Where-Object {$_.Comment -eq $Null}

## 範例 5

範例 5 會傳回 Comment 屬性中某處包含字串值 "Ken Myer" 的所有封鎖網域。為了執行此工作，命令會先呼叫 **Get-CsBlockedDomain** Cmdlet，以傳回封鎖網域清單上所有網域的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 Comment 屬性包含字串值 "Ken Myer" 的網域。

    Get-CsBlockedDomain | Where-Object {$_.Comment -match "Ken Myer"}

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與第三方主機供應商之間的同盟。

設定與其他組織間的直接同盟包含幾個工作。若要開始，必須將 Lync Server Access Edge 服務設為允許同盟。此外，另一個組織必須允許與您同盟；除非雙方都同意該關係，否則無法建立同盟。

若要設定同盟關係，您也可能需要管理兩個同盟相關清單：允許清單和封鎖清單。允許清單表示您已選擇與其同盟的組織；如果某個網域顯示在允許清單中，則 (根據您的組態設定而定) 您的使用者就可以與在該同盟網域中具有帳戶的使用者交換立即訊息及目前狀態資訊。相反地，封鎖清單代表明確禁止使用者進行同盟的網域；例如，Lync Server 會自動拒絕從封鎖網域傳送的訊息。

**Get-CsBlockedDomain** Cmdlet 可讓您傳回關於出現在封鎖網域清單上之網域的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsBlockedDomain** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsBlockedDomain"}

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
<td><p>可讓您使用萬用字元傳回封鎖網域清單中的一或多個網域。若要傳回其 Identity 開頭為字母 &quot;r&quot; 的所有網域，請使用下列語法：-Filter r*。若要傳回其 Identity 結尾為 &quot;.net&quot; 的所有網域，請使用下列語法：-Filter &quot;*.net&quot;。若要傳回其 Identity 開頭為字母 &quot;f&quot; 或字母 &quot;g&quot; 的所有網域，請使用下列語法：-Filter [fg]*。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回之網域的名稱。網域會以其完整網域名稱 (FQDN) 列在封鎖清單上；因此，指定網域的 Identity 可能類似於 fabrikam.com 或 contoso.net。請注意，指定網域 Identity 時無法使用萬用字元。若要使用萬用字元傳回指定網域 (或一組網域)，請改用 Filter 參數。</p>
<p>若未指定此參數，則會傳回封鎖網域清單上的所有網域。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取封鎖的網域資料，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsBlockedDomain** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.BlockedDomain 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsBlockedDomain](new-csblockeddomain.md)  
[Remove-CsBlockedDomain](remove-csblockeddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)  
[Set-CsBlockedDomain](set-csblockeddomain.md)

