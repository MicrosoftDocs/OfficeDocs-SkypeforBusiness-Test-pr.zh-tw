---
title: Get-CsPool
TOCTitle: Get-CsPool
ms:assetid: e0911c68-9a0a-461a-88d6-c610c6cd996c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398992(v=OCS.15)
ms:contentKeyID: 49292580
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPool

 

_**上次修改主題的時間：** 2015-03-09_

傳回 Lync Server 部署所使用之集區的資訊。集區是網站中一群全都是執行 Lync Server 服務的電腦集合。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsPool [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPool [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Site <String>]

## 範例

## 範例 1

範例 1 會傳回在您 Lync Server 部署中找到的所有集區。

    Get-CsPool

## 範例 2

範例 2 會顯示在每個集區中找到之電腦的資訊。作法是呼叫 **Get-CsPool** Cmdlet，然後將傳回的資料管線傳送到 **Select-Object** Cmdlet。接著使用 ExpandProperty 參數「展開」Computers 屬性值。Computers 屬性就是代表集區中每一部電腦的物件陣列。當您展開 Computers 屬性時，可以看到這每一部電腦的詳細資訊。

    Get-CsPool | Select-Object -ExpandProperty Computers

## 範例 3

範例 3 會使用 Identity 參數將傳回的資料限制在 Identity 為 atl-cs-001.litwareinc.com 的集區。

    Get-CsPool -Identity atl-cs-001.litwareinc.com

## 範例 4

範例 4 會傳回於 Redmond 網站中找到的所有集區。為達此目的，命令會使用 Site 參數 (參數值 "Redmond" 可將傳回的資料限制在 Site 屬性等於 Redmond 的集區)。

    Get-CsPool -Site "Redmond"

## 範例 5

範例 5 所示的命令會傳回未安裝任何 Lync Server 服務之所有集區的集合。為執行此工作，命令會先呼叫不含任何參數的 **Get-CsPool** Cmdlet，以傳回組織目前使用之所有集區的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 Services.Count 屬性等於 0 的所有集區。如果 Count 等於 0，則表示該集區未設定任何 Lync Server 服務。

    Get-CsPool | Where-Object {$_.Services.Count -eq 0}

## 詳細描述

在 Lync Server 中，集區代表相同網站 (執行相同服務集) 中的一或多部電腦。例如，若您有一部在 Redmond 網站中執行中繼伺服器服務的伺服器，則中繼伺服器集區會包含該部電腦。若您有兩部在 Redmond 網站中執行中繼伺服器的電腦，則中繼伺服器集區會包含兩部電腦。用於您組織中的集區數量會依您具有的伺服器數量與這些伺服器所執行的不同服務而定。

**Get-CsPool** Cmdlet 可讓您擷取使用於您組織中每個集區的資訊，包含在這些集區上執行之服務的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsPool** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPool"}

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
<td><p>在指定要傳回之集區的 Identity 時，可讓您使用萬用字元。例如，此語法會傳回其 Identity 以字串值 &quot;.fabrikam.com&quot; 結束的所有集區：-Filter &quot;*.fabrikam.com&quot;。</p>
<p>請注意，您不能在同一個命令中同時使用 Filter 和 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回之集區的完整網域名稱 (FQDN)。例如：-Identity atl-cs-001.litwareinc.com。</p>
<p>若未使用此參數，則將會傳回您組織中的所有集區。</p></td>
</tr>
<tr class="odd">
<td><p><em>Site</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>傳回在指定網站上找到的所有集區。問題中的網站應可使用網站的 DisplayName (例如，Redmond) 進行參考，而非使用網站 Identity (例如，site:Redmond)。例如：-Site &quot;Redmond&quot;。您可以執行此命令以擷取網站的顯示名稱：</p>
<p>Get-CsSite | Select-Object Identity, DisplayName</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsPool** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPool** Cmdlet 會傳回 Microsoft.Rtc.Management.Deploy.Internal.Cluster 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsSite](get-cssite.md)  
[Get-CsTopology](get-cstopology.md)

