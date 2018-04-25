---
title: Set-CsClsSearchTerm
TOCTitle: Set-CsClsSearchTerm
ms:assetid: 57ccaf25-31ab-4059-8dc4-144f29f3af68
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204911(v=OCS.15)
ms:contentKeyID: 49290970
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClsSearchTerm

 

_**上次修改主題的時間：** 2015-03-09_

修改一或多個集中式記錄搜尋字詞。搜尋字詞可用於定義個人的識別資訊，以供技術支援人員搜尋集中式追蹤記錄時使用。搜尋字詞適合搭配 商務用 Skype Online 使用。

Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsClsSearchTerm [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClsSearchTerm [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Inserts <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例所示的命令會設定搜尋字詞 "site:Redmond/IP" 的 Inserts 屬性。此範例只會設定一個 Insert：ItemURI。

    Set-CsClsSearchTerm -Identity "site:Redmond/IP" -Inserts "ItemURI"

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

在 商務用 Skype Online 中，系統管理員可利用搜尋字詞遮罩個人識別資訊，以避免支援人員在檢視記錄檔時看到這些資訊。例如在使用支援主控台時不會顯示使用者名稱 Ken Myer，而會顯示 FIRST1 LAST1。同樣地，電話號碼 +12065551219 也可能會改為顯示 PHONE1。

**Set-CsClsSearchTerm** Cmdlet 可讓您修改目前指派給集中式記錄組態設定集合的任何搜尋字詞。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClsSearchTerm"}

**Lync Server 控制台：** **Set-CsClsSearchTerm** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之搜尋字詞的唯一識別碼。搜尋字詞包含兩個部分：字詞設定所在的範圍 (亦即，可以找到該字詞的集中式記錄組態設定集合) 及字詞名稱。例如：</p>
<p>-Identity &quot;site:Redmond/CallID&quot;</p>
<p>您無法在指定 Identity 時使用萬用字元。</p></td>
</tr>
<tr class="even">
<td><p><em>Inserts</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>指定在檢視記錄檔時，個人身分資訊的遮罩方式。例如，Insert 為 &quot;ItemURI&quot; 表示使用者 URI 資訊應設定遮罩。如此一來，使用者 URI (例如 sip:kenmyer@litwareinc.com) 就會顯示成一般 URI，隱藏使用者名稱，但保留網域名稱：</p>
<p>Sip:USER1@litwareinc.com</p>
<p>插入遮罩，例如使用者名稱和電腦名稱、電話號碼，以及 IP 位址等等。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您傳遞物件參考，而不設定個別的參數值。</p></td>
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

**Set-CsClsSearchTerm** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SearchTerm\#Decorated 物件執行個體。

## 傳回類型

無。反之， **Set-CsClsSearchTerm** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SearchTerm\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsClsSearchTerm](get-csclssearchterm.md)

