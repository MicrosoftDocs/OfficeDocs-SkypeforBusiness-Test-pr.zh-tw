---
title: Get-CsNetworkInterface
TOCTitle: Get-CsNetworkInterface
ms:assetid: 06a5fedf-d87e-4469-9bd6-ad16c1f9a801
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398121(v=OCS.15)
ms:contentKeyID: 49289982
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterface

 

_**上次修改主題的時間：** 2015-03-09_

傳回執行 Lync Server 服務或伺服器角色之電腦上所用的網路介面的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsNetworkInterface [-Identity <NetworkInterfaceIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterface [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ComputerFqdn <Fqdn>]

## 範例

## 範例 1

範例 1 會傳回設定為在組織中使用之所有網路介面的資訊。

    Get-CsNetworkInterface

## 範例 2

範例 2 所示的命令會傳回單一網路介面的資訊：Identity 為 atl-cs-001.litwareinc.com.com/Primary/1 的介面。

    Get-CsNetworkInterface -Identity atl-cs-001.litwareinc.com/Primary/1

## 範例 3

範例 3 會傳回網域 litwareinc.com 中所有網路介面的資訊。為達此目的，會加入 -Filter 參數搭配篩選值 "\*.litwareinc.com\*"。此篩選值會將傳回的資料限制為其 Identity 包含字串值 "litwareinc.com" 的介面。

    Get-CsNetworkInterface -Filter "*.litwareinc.com*"

## 範例 4

範例 4 會傳回設定為 IP 位址 192.168.0.240 之所有網路介面的資訊。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsNetworkInterface** Cmdlet，以傳回設定供組織使用之所有網路介面的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 IPAddress 屬性等於 192.168.0.240 的介面。

    Get-CsNetworkInterface | Where-Object {$_.IPAddress -eq "192.168.0.240"}

## 範例 5

範例 5 所示的命令是範例 4 所示命令的變化，但此範例會傳回子網路 "192.168.0.\*" 所設定之所有網路介面的資訊。作法是擷取所有網路介面的集合，再將該集合管線傳送到 **Where-Object** Cmdlet，然後只挑出 IPAddress 開頭字串值是 "192.168.0." 的介面。

    Get-CsNetworkInterface | Where-Object {$_.IPAddress -like "192.168.0.*"}

## 範例 6

範例 6 會傳回設定供外部存取的所有網路介面。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsNetworkInterface** Cmdlet，以傳回目前所使用之所有網路介面的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 Interface 屬性等於 External 的項目。

    Get-CsNetworkInterface | Where-Object {$_.Interface -eq "External"}

## 詳細描述

為了讓資訊從一部電腦傳輸到另一部電腦，電腦都需要網路介面：電腦與網路之間的連線。執行 Lync Server 服務或伺服器角色的電腦至少必須有一個網路介面；否則無法與其他電腦進行通訊。不過，這些電腦也可以擁有多個網路介面；例如 Edge Server 可能擁有一個介面與內部網路連線，另一個介面與網際網路連線。**Get-CsNetworkInterface** Cmdlet 為系統管理員提供一種方法，可以傳回在執行 Lync Server 服務或伺服器角色的電腦上目前所使用之網路介面的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsNetworkInterface** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterface"}

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
<td><p><em>ComputerFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要傳回之網路介面資訊的電腦 FQDN。例如，若要傳回電腦 atl-cs-001.litwareinc.com 的網路介面資訊 (且僅針對該電腦)，請使用下列語法：-ComputerFqdn atl-cs-001.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您在指定要傳回的網路介面 (或多個介面) 時使用萬用字元。例如，此語法會傳回執行 Lync Server 服務或伺服器角色之所有電腦上的主要網路介面相關資訊：-Filter &quot;*/Primary/*&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.NetworkInterfaceIdentity</p></td>
<td><p>要傳回之網路介面的唯一識別碼。網路介面 Identity 包含三個部分：</p>
<p>電腦本身的完整網域名稱 (FQDN) (例如 atl-cs-001.litwareinc.com)。</p>
<p>網路介面「端」(主要、內部、外部、公用交換電話網路)。「端」指的是連接埠用在哪一種流量類型。</p>
<p>該特定端的網路介面號碼。</p>
<p>例如：-Identity &quot;atl-cs-001.litwareinc.com/Primary/1&quot;。</p>
<p>Identity、ComputerFqdn 和 Filter 參數必須分開使用；例如，您無法執行同時使用 ComputerFqdn 與 Identity 的命令。此外，您無法在指定 Identity 時使用萬用字元。若要使用萬用字元，請使用 Filter 參數。</p>
<p>如果 Identity (ComputerFqdn) 與 Filter 參數都未使用，則 <strong>Get-CsNetworkInterface</strong> Cmdlet 會傳回在執行 Lync Server 服務或伺服器角色的電腦上所有目前所使用之網路介面的資訊。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsNetworkInterface** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsNetworkInterface** Cmdlet 會傳回 Microsoft.Rtc.Management.Xds.DisplayNetworkInterface 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsComputer](get-cscomputer.md)

