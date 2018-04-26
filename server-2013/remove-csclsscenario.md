---
title: Remove-CsClsScenario
TOCTitle: Remove-CsClsScenario
ms:assetid: 747bd4d6-797e-4088-9303-6ceb65f66183
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205010(v=OCS.15)
ms:contentKeyID: 49291336
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClsScenario

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的集中式記錄組態案例。案例代表系統管理員可啟用或停用追蹤的特定 Lync Server 2013元件或狀況 (例如 IM 和目前狀態)。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsClsScenario -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從全域的集中式記錄組態設定集合移除 WAC 案例。

    Remove-CsClsScenario -Identity "site:Redmond/WAC"

## 範例 2

範例 2 會從組織所使用的所有集中式記錄組態設定中移除 HybridVoice 案例。為達成此目的，會先呼叫不含任何參數的 **Get-CsClsScenario** Cmdlet，以傳回所有可用案例的集合。然後，此集合會管線傳送到 Where-Object Cmdlet，這會挑出 Name 屬性等於 (-eq) HybridVoice 的所有案例。接著將 HybridVoice 案例管線傳送到 **Remove-CsClsScenario** Cmdlet 加以刪除。

    Get-CsClsScenario | Where-Object {$_.Name -eq "HybridVoice" | Remove-CsClsScenario

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

集中式記錄是以一系列預先定義的案例為主來建立，可提供比舊版 Lync Server 更精確的記錄方法。這些案例可為您預先決定伺服器元件與記錄功能；因此，啟用 RGS 案例的管理員確信將只會記錄與「回應群組」服務有關的資訊，而非不相關的服務，例如音訊會議提供者服務。

**Remove-CsClsScenario** Cmdlet 可讓您移除集中式記錄組態設定中的案例。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClsScenario"}

Lync Server 控制台：**Remove-CsClsScenario** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>所要移除之案例的唯一識別碼。案例包含兩個部分：案例設定所在的範圍 (亦即，可以找到該案例的集中式記錄組態設定集合) 及案例名稱。例如：</p>
<p>-Identity &quot;site:Redmond/AddressBook&quot;</p>
<p>您也可以只指定案例範圍；例如：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>但是如果這麼做，將會移除指定範圍的整個集中式記錄組態設定集合，而不只是該案例。</p></td>
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

**Remove-CsClsScenario** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Scenario\#Decorated 物件執行個體。

## 傳回類型

無。反之， **Remove-CsClsScenario** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Scenario\#Decorated 物件執行個體。

