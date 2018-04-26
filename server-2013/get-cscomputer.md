---
title: Get-CsComputer
TOCTitle: Get-CsComputer
ms:assetid: 493931a9-1670-4a76-abba-7d3c7723d2e1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425959(v=OCS.15)
ms:contentKeyID: 49290815
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsComputer

 

_**上次修改主題的時間：** 2015-03-09_

傳回在 Lync Server 基礎結構內擔任服務角色之電腦的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsComputer [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsComputer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Local <SwitchParameter>] [-Pool <String>]

## 範例

## 範例 1

在範例 1 中，**Get-CsComputer** Cmdlet 會用來傳回 Lync Server 基礎結構內執行服務角色之所有電腦的資訊。

    Get-CsComputer

## 範例 2

範例 2 所示的命令會使用 Filter 參數，只傳回為 litwareinc.com 網域之一部份的服務角色電腦。萬用字元字串 \*.litwareinc.com 會將傳回的資訊限制為 FQDN 結尾為 .litwareinc.com 的電腦。

    Get-CsComputer -Filter "*.litwareinc.com"

## 範例 3

在範例 3 中，Identity 參數用來限制傳回資料具 FQDN 為 atl-cs-001.litwareinc.com 的一部電腦。

    Get-CsComputer -Identity "atl-cs-001.litwareinc.com"

## 範例 4

範例 4 使用 Pool 參數來傳回集區 atl-cs-001.litwareinc.com 中所有電腦的資訊。

    Get-CsComputer -Pool "atl-cs-001.litwareinc.com"

## 詳細描述

**Get-CsComputer** Cmdlet 可快速識別執行 Lync Server 服務或伺服器角色的電腦。呼叫時若未使用任何參數，**Get-CsComputer** Cmdlet 將會傳回所有執行 Lync Server 服務或擔任伺服器角色之電腦的集合。此集合包括每部電腦的 Identity、集區名稱及完整網域名稱 (FQDN)。或者，您可以使用選用參數，例如 Identity、Filter 或 Pool，以限制傳回單一電腦或一組電腦的資料。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsComputer** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。

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
<td><p>讓您可在指定傳回電腦 (或多台電腦) 時，使用萬用字元。例如，此命令會傳回具有以字串值 &quot;atl-&quot; 為開頭之 Identity 的所有電腦資訊：-Filter &quot;atl-*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回之電腦的 FQDN。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p>若未指定此參數，則會傳回執行 Lync Server 的所有電腦。</p></td>
</tr>
<tr class="odd">
<td><p><em>Local</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，只會傳回本機電腦的資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>Pool</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>Lync Server 集區的 FQDN。當您使用此參數時，會傳回指定集區之所有電腦的資訊。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsComputer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsComputer** Cmdlet 會傳回 Microsoft.Rtc.Management.Deploy.Internal.Machine 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsComputer](disable-cscomputer.md)  
[Enable-CsComputer](enable-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

