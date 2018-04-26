---
title: Show-CsClsLogging
TOCTitle: Show-CsClsLogging
ms:assetid: 19b2de51-5c14-4a8b-97e5-573c3285b174
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619173(v=OCS.15)
ms:contentKeyID: 49290237
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Show-CsClsLogging

 

_**上次修改主題的時間：** 2015-03-09_

顯示目前的集中式記錄服務狀態 (亦即，顯示目前使用中的集中式記錄案例)。集中式記錄提供一種方法，讓管理員同時啟用或停用多部電腦上的 Lync Server 2013 追蹤功能。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Show-CsClsLogging [-AsXml <SwitchParameter>] [-Computers <String[]>] [-Pools <String[]>]

## 範例

## 範例 1

範例 1 所示的命令會傳回目前正在拓撲中的電腦上記錄之案例的相關資訊。

    Show-CsClsLogging

## 範例 2

在範例 2 中，會傳回集區 atl-cs-001.litwareinc.com 中所有伺服器的記錄資訊。

    Show-CsClsLogging -Pools "atl-cs-001.litwareinc.com"

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

集中式記錄是以一系列預先定義的案例為主來建立，可提供比舊版 Lync Server 更精確的記錄方法。這些案例可為您預先決定伺服器元件與記錄功能；因此，啟用 RGS 案例的管理員確信將只會記錄與「回應群組」服務有關的資訊，而非不相關的服務，例如音訊會議提供者服務。

您也可以使用 [New-CsClsScenario](new-csclsscenario.md) Cmdlet，定義自訂的案例。

**Show-CsClsLogging** Cmdlet 會傳回一個或一組電腦上目前正在記錄之所有案例的相關資訊；此資訊包括每個使用者案例的名稱與持續時間，以及記錄開始的日期與時間。

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
<td><p><em>AsXml</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定時，會使用 XML 傳回資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>Computers</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>可讓管理員傳回所指定伺服器或一組伺服器中的記錄資訊。若要傳回單一伺服器中的資訊，請指定該伺服器的完整網域名稱。例如：</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;</p>
<p>您可以使用逗號分隔電腦的 FQDN 來指定多個伺服器：</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;,&quot;red-server-002.litwareinc.com&quot;</p>
<p>如果未加上 Computers 參數或 Pools 參數， <strong>Show-CsClsLogging</strong> Cmdlet 會顯示拓撲中所有 Computers 的狀態。</p></td>
</tr>
<tr class="odd">
<td><p><em>Pools</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>可讓管理員傳回集區中每個伺服器的記錄資訊。若要傳回集區的資訊，請指定該集區的完整網域名稱。例如：</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;</p>
<p>您可以使用逗號分隔集區的 FQDN 來指定多個集區：</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;,&quot;red-cs-002.litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Show-CsClsLogging** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

字串值或 XML 輸出。**Show-CsClsLogging** Cmdlet 不會傳回物件。

## 請參閱

#### 其他資源

[Search-CsClsLogging](search-csclslogging.md)  
[Start-CsClsLogging](start-csclslogging.md)  
[Stop-CsClsLogging](stop-csclslogging.md)  
[Sync-CsClsLogging](sync-csclslogging.md)  
[Update-CsClsLogging](update-csclslogging.md)

