---
title: Get-CsClsRegion
TOCTitle: Get-CsClsRegion
ms:assetid: 4f38e966-8e92-4549-8124-097c236c0165
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204879(v=OCS.15)
ms:contentKeyID: 49290891
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClsRegion

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之集中式記錄組態區域的資訊。集中式記錄讓系統管理員可以同時啟用或停用多部電腦上的事件追蹤。集中式記錄區域主要會在 商務用 Skype Online 上使用。

Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsClsRegion [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClsRegion [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有集中式記錄區域的資訊。

    Get-CsClsRegion

## 範例 2

範例 2 只會傳回 Identity 為 global/US 之集中式記錄區域的資訊。

    Get-CsClsRegion -Identity "global/US"

## 範例 3

範例 3 會傳回在全域範圍設定之所有集中式記錄區域的資訊。作法是呼叫 **Get-CsClsRegion** Cmdlet 搭配 Filter 參數；篩選值 "global/\*" 可將傳回的資料限制在全域範圍設定的區域。

    Get-CsClsRegion -Filter "global/*"

## 範例 4

範例 4 所示的命令會針對允許歐洲區域存取的所有集中式記錄區域傳回資訊。為達成此目的，命令會先使用 **Get-CsClsRegion** Cmdlet 傳回目前所使用之所有集中式記錄區域的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 OtherRegionAccess 屬性包含 "Europe" 字串值的區域。

    Get-CsClsRegion | Where-Object {$_.OtherRegionAccess -match "Europe"}

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

在 Office 365 版的 Lync Server 中，區域可用於指定有權存取寫入記檔中之個人資訊的使用者。區域會在使用 [New-CsClsRegion](new-csclsregion.md) Cmdlet 建立後，才新增至集中式記錄組態設定的集合。您可以使用 **Get-CsClsRegion** Cmdlet 傳回集中式記錄區域的資訊。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClsRegion"}

**Lync Server 控制台：** **Get-CsClsRegion** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>System.Strkng</p></td>
<td><p>可讓您使用萬用字元傳回集中式記錄區域。例如，若要傳回在全域範圍設定之所有設定的集合，請使用下列語法：</p>
<p>-Filter &quot;global/*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之集中式記錄區域的唯一識別碼。區域識別包含區域建立所在的範圍，後接區域名稱。例如，若要傳回在全域範圍建立名為 US 的區域，請使用下列語法：</p>
<p>-Identity &quot;global/US&quot;</p>
<p>如果沒有指定此參數， <strong>Get-CsClsRegion</strong> Cmdlet 就會傳回所有集中式記錄區域的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區的本機複本擷取集中式記錄組態資料，而非從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsClsRegion** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsClsRegion** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Region\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsClsRegion](new-csclsregion.md)  
[Remove-CsClsRegion](remove-csclsregion.md)  
[Set-CsClsRegion](set-csclsregion.md)

