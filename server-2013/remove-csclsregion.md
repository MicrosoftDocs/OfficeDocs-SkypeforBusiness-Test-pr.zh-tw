---
title: Remove-CsClsRegion
TOCTitle: Remove-CsClsRegion
ms:assetid: 6ab1596e-0e27-44e7-8cbc-efd4064ba58b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204971(v=OCS.15)
ms:contentKeyID: 49291215
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClsRegion

 

_**上次修改主題的時間：** 2015-03-09_

移除一或多個集中式記錄組態區域。集中式記錄讓系統管理員可以同時啟用或停用多部電腦上的事件追蹤。集中式記錄區域適合搭配 商務用 Skype Online 使用。

Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsClsRegion -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除 Identity 為 global/US 的集中式記錄區域。

    Remove-CsClsRegion -Identity "global/US"

## 範例 2

範例 2 會移除在全域範圍設定的所有集中式記錄區域。為達成此目的，命令會先呼叫 **Get-CsClsRegion** Cmdlet 並搭配 Filter 參數；篩選值 "global/\*" 可將傳回的資料限制為全域範圍中所設定的區域。然後再將這些區域管線傳送到 **Remove-CsClsRegion** Cmdlet 加以刪除。

    Get-CsClsRegion -Filter "global/*" | Remove-CsClsRegion 

## 範例 3

範例 3 會刪除安全性群組尾碼為 EMEA 的所有集中式記錄區域。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsClsRegion** Cmdlet，以傳回設定供組織使用之所有集中式記錄區域的集合。然後，此集合會管線傳送到 Where-Object Cmdlet，這會只挑出 SecurityGroupSuffix 屬性等於 (-eq) EMEA 的區域。接著將該區域的子集合管線傳送到 **Remove-CsClsRegion** Cmdlet，以刪除子集合中的每個區域。

    Get-CsClsRegion | Where-Object {$_.SecurityGroupSuffix -eq "EMEA" | Remove-CsClsRegion

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 商務用 Skype Online 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

透過 商務用 Skype Online，區域可用於指定有權存取寫入記檔中之個人資訊的使用者。區域會在使用 [New-CsClsRegion](new-csclsregion.md) Cmdlet 建立後，才新增至集中式記錄組態設定的集合。您之後可以使用 **Remove-CsClsRegion** Cmdlet 移除新增至這些集合中的區域。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClsRegion"}

**Lync Server 控制台：** **Remove-CsClsRegion** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要移除之集中式記錄區域的唯一識別碼。區域識別包含區域建立所在的範圍，後接區域名稱。例如，若要刪除在全域範圍建立名為 US 的區域，請使用下列語法：</p>
<p>-Identity &quot;global/US&quot;</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Remove-CsClsRegion** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Region\#Decorated 物件執行個體。

## 傳回類型

無。反之， **Remove-CsClsRegion** 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Region\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsClsRegion](get-csclsregion.md)  
[New-CsClsRegion](new-csclsregion.md)  
[Set-CsClsRegion](set-csclsregion.md)

