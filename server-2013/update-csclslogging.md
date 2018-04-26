---
title: Update-CsClsLogging
TOCTitle: Update-CsClsLogging
ms:assetid: 104ecc02-789d-4538-8203-0451448d4301
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619170(v=OCS.15)
ms:contentKeyID: 49290117
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsClsLogging

 

_**上次修改主題的時間：** 2015-03-09_

更新所有使用中集中式記錄案例的持續期間。集中式記錄提供一種方法，讓管理員同時啟用或停用多部電腦上的 Lync Server 2013 追蹤功能。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Update-CsClsLogging -Duration <String> [-AsXml <SwitchParameter>] [-Computers <String[]>] [-Pools <String[]>]

## 範例

## 範例 1

範例 1 所示的命令會針對拓撲中的伺服器修改記錄持續期間。

    Update-CsClsLogging -Duration 60

## 範例 2

在範例 2 中，會針對集區 atl-cs-001.litwareinc.com 中的所有伺服器修改持續期間。

    Update-CsClsLogging -Duration 60 -Pools "atl-cs-001.litwareinc.com"

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

集中式記錄是以一系列預先定義的案例為主來建立，可提供比舊版 Lync Server 更精確的記錄方法。這些案例可為您預先決定伺服器元件與記錄功能；因此，啟用 RGS 案例的管理員確信將只會記錄與「回應群組」服務有關的資訊，而非不相關的服務，例如音訊會議提供者服務。

您也可以使用 [New-CsClsScenario](new-csclsscenario.md) Cmdlet，定義自訂的案例。

根據預設，記錄作業會在執行 4 小時 (240 分鐘) 後自動停止；不過，管理員可以在開始記錄時，選擇指定不同的持續期間。此外，管理員也可以使用 **Update-CsClsLogging** Cmdlet 針對目前正在記錄的所有案例來變更持續期間。

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
<td><p><em>Duration</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>記錄作業應要執行的時間。例如，以下語法會使得記錄作業執行 2 小時 (120 分鐘)，然後才停止：</p>
<p>-Duration 120</p>
<p>下列語法會將持續時間指定為 3 小時 14 分鐘：</p>
<p>-Duration 3:15</p>
<p>下列語法會將持續時間指定為 6 天 5 小時 12 分鐘：</p>
<p>-Duration 6.5:12</p>
<p>預設值是 30 分鐘。</p></td>
</tr>
<tr class="even">
<td><p><em>AsXml</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定時，會使用 XML 傳回資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Computers</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>可讓管理員在指定的伺服器或一組伺服器上更新集中式記錄服務。若要更新單一伺服器，請指定該伺服器的完整網域名稱。例如：</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;</p>
<p>您可以使用逗號分隔電腦的 FQDN 來指定多個伺服器：</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;,&quot;red-server-002.litwareinc.com&quot;</p>
<p>如果未加上 Computers 參數或 Pools 參數，Update-CsClsLogging 將針對拓撲中的電腦自動執行。</p></td>
</tr>
<tr class="even">
<td><p><em>Pools</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>可讓管理員在集區中的每個伺服器上更新集中式記錄服務。若要更新集區中的伺服器，請指定該集區的完整網域名稱。例如：</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;</p>
<p>您可以使用逗號分隔集區的 FQDN 來指定多個集區：</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;,&quot;red-cs-002.litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Update-CsClsLogging** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

字串值。

## 請參閱

#### 其他資源

[Search-CsClsLogging](search-csclslogging.md)  
[Show-CsClsLogging](show-csclslogging.md)  
[Start-CsClsLogging](start-csclslogging.md)  
[Stop-CsClsLogging](stop-csclslogging.md)  
[Sync-CsClsLogging](sync-csclslogging.md)

