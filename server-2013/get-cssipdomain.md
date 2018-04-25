---
title: Get-CsSipDomain
TOCTitle: Get-CsSipDomain
ms:assetid: 8a8def42-7b14-40c3-be5a-57905069b405
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398701(v=OCS.15)
ms:contentKeyID: 49291591
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsSipDomain

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之 SIP 網域的資訊。SIP 網域是有權傳送及接收 SIP 流量的網域，會在指派 SIP 位址給使用者時使用。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsSipDomain [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsSipDomain [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## 範例

## 範例 1

範例 1 會呼叫不含任何參數的 **Get-CsSipDomain** Cmdlet，以傳回設定供組織使用之所有 SIP 網域的資訊。

    Get-CsSipDomain

## 範例 2

範例 2 所示的命令會傳回 Identity 為 fabrikam.com 之 SIP 網域的資訊。由於 SIP 網域 Identity 必須是唯一的，因此這個命令永遠不會傳回多於一個項目。

    Get-CsSipDomain -Identity fabrikam.com

## 範例 3

範例 3 會使用 **Get-CsSipDomain** Cmdlet 和 Filter 參數，以傳回 Identity 以 "f" 字母開頭的所有 SIP 網域相關資訊。例如：fabrikam.com、fabrikam.org、fabrikam-users.com 等等。

    Get-CsSipDomain -Filter "f*"

## 範例 4

範例 4 所示的命令會傳回預設 SIP 網域的資訊。為達成此目的，會先呼叫不含任何參數的 **Get-CsSipDomain** Cmdlet，以傳回設定供組織使用之所有 SIP 網域的集合。然後，將此集合管線傳送至 **Where-Object** Cmdlet，以選取 IsDefault 屬性等於 True 的一個網域。

    Get-CsSipDomain | Where-Object {$_.IsDefault -eq $True}

## 詳細描述

為了設定 SIP 位址給您的使用者 (進而讓他們能夠使用 Lync 2013 之類的 SIP 相關軟體)，您需要兩項資訊：使用者 ID (例如 Ken.Myer) 和 SIP 網域 (例如 litwareinc.com)。用來建構 SIP 位址的 SIP 網域必須是您 Active Directory 樹系內有權傳送及接收流量的網域。例如，假設您有名為 litwareinc.com、fabrikam.com 和 contoso.com 的網域，但是只有 litwareinc.com 已識別為 SIP 網域。在此情況下，您無法使用 sip:Ken.Myer@fabrikam.com 或 sip:Ken.Myer@contoso.com 這類的 SIP 位址，除非將 fabrikam.com 和 contoso.com 設為有效的 SIP 網域。這就是執行 **New-CsSipDomain** Cmdlet 的作用之一。

**Get-CsSipDomain** Cmdlet 可讓您傳回獲授權供組織使用之 SIP 網域的資訊。**Get-CsSipDomain** Cmdlet 也會識別組織的預設 SIP 網域；這是未指定 SIP 網域時，Lync Server 預設會使用的網域。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsSipDomain** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsSipDomain"}

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
<td><p>可讓您在指定要傳回之 SIP 網域的 Identity 時使用萬用字元。例如，篩選值 &quot;*.org&quot; 會傳回其 Identity 以字串值 &quot;.org&quot; 結尾之所有授權 SIP 網域的集合。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回之 SIP 網域的完整網域名稱 (FQDN) (例如 fabrikam.com)。如果既未指定此參數也未指定 Filter 參數，則會傳回所有已授權在您組織中使用的 SIP 網域。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsSipDomain** Cmdlet 不接受管線傳送的資料。

## 傳回類型

**Get-CsSipDomain** Cmdlet 會傳回 Microsoft.Rtc.Management.Xds.SipDomain 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsSipDomain](new-cssipdomain.md)  
[Remove-CsSipDomain](remove-cssipdomain.md)  
[Set-CsSipDomain](set-cssipdomain.md)

