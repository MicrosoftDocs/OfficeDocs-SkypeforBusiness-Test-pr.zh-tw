---
title: Get-CsClsSearchTerm
TOCTitle: Get-CsClsSearchTerm
ms:assetid: 89a6cc1d-5cbe-42ef-b5a0-127068a0f78a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205061(v=OCS.15)
ms:contentKeyID: 49291587
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClsSearchTerm

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之集中式記錄搜尋字詞的資訊。搜尋字詞可用於定義個人的識別資訊，以供技術支援人員搜尋集中式追蹤記錄時使用。搜尋字詞主要是搭配 商務用 Skype Online使用。

Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsClsSearchTerm [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClsSearchTerm [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回目前用於組織的所有搜尋字詞相關資訊。

    Get-CsClsSearchTerm

## 範例 2

範例 2 會傳回單一搜尋字詞的資訊：在全域的集中式記錄組態設定集合中找到的 Phone 搜尋字詞。

    Get-CsClsSearchTerm -Identity "global/Phone"

## 範例 3

範例 3 所示的命令會傳回所有 URI 搜尋字詞的資訊。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsClsSearchTerm** Cmdlet，以傳回所有可用搜尋字詞的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Type 屬性等於 (-eq) URI 的字詞。

    Get-CsClsSearchTerm | Where-Object {$_.Type -eq "URI"}

## 範例 4

範例 4 會傳回所有 Inserts 屬性包含字串值 "ItemE164" 之搜尋字詞的資訊。為了執行此工作，命令會先使用 **Get-CsClsSearchTerm** Cmdlet 傳回所有可用搜尋字詞的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以選取 Inserts 屬性包含 (-match) "ItemE164" 字串值的字詞。

    Get-CsClsSearchTerm | Where-Object {$_.Inserts -match "ItemE164"}

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

在 Lync Server 2013 中，系統管理員可利用搜尋字詞遮罩個人識別資訊，以避免支援人員在檢視記錄檔時看到這些資訊。例如在使用支援主控台時不會顯示使用者名稱 Ken Myer，而會顯示 FIRST1 LAST1。 同樣地，電話號碼 +12065551219 也可能會改為顯示 PHONE1。

**Get-CsClsSearchTerm** Cmdlet 可傳回目前可使用之搜尋字詞的資訊。這些搜尋字詞是基於 Inserts 屬性，該屬性會指定要遮罩的資訊，以及要替代個人識別資訊的遮罩。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClsSearchTerm"}

**Lync Server 控制台：** **Get-CsClsSearchTerm** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>可讓您使用萬用字元來傳回一或多個搜尋字詞。例如，若要傳回所有 CallID 搜尋字詞，無論設定這些字詞所在的範圍為何，請使用下列語法：</p>
<p>-Filter &quot;*CallID*&quot;</p>
<p>同一個命令中不可同時使用 Identity 參數與 Filter 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>所要傳回之搜尋字詞的唯一識別碼。搜尋字詞包含兩個部分：字詞設定所在的範圍 (亦即，可以找到該字詞的集中式記錄組態設定集合) 及字詞名稱。例如：</p>
<p>-Identity &quot;site:Redmond/CallID&quot;</p>
<p>您也可以只指定搜尋字詞範圍；例如：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>在該情況下，將會傳回設定用於 Redmond 網站的所有搜尋字詞。</p>
<p>若未指定此參數， <strong>Get-CsSearchTerm</strong> Cmdlet 會傳回所有集中式記錄搜尋字詞的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取搜尋字詞資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsClsSearchTerm** Cmdlet 不支援管線傳送的輸入。

## 傳回類型

**Get-CsClsSearchTerm** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SearchTerm\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsClsSearchTerm](set-csclssearchterm.md)

