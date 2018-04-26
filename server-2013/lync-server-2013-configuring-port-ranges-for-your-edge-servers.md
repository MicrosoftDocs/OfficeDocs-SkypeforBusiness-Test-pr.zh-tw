---
title: 設定 Edge Server 的連接埠範圍
TOCTitle: 設定 Edge Server 的連接埠範圍
ms:assetid: 6f0ae442-6624-4e3f-849a-5b9e387fb8cf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204996(v=OCS.15)
ms:contentKeyID: 49291273
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Edge Server 的連接埠範圍

 

_**上次修改主題的時間：** 2015-07-24_

有了 Edge 伺服器，您不需要針對音訊、視訊與應用程式共用設定個別連接埠範圍；同樣地，用於 Edge 伺服器的連接埠範圍也無須符合與您會議伺服器、應用程式伺服器以及中繼伺服器搭配使用的連接埠範圍。但是，若要使管理更為容易，您可能會希望繼續變更 Edge Server 連接埠範圍，以符合其他伺服器上的連接埠範圍。例如，假設您已設定會議、應用程式以及中繼伺服器以使用這些連接埠範圍：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>封包類型</th>
<th>起始連接埠</th>
<th>已保留連接埠數目</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>應用程式共用</p></td>
<td><p>40803</p></td>
<td><p>8348</p></td>
</tr>
<tr class="even">
<td><p>音訊</p></td>
<td><p>49152</p></td>
<td><p>8348</p></td>
</tr>
<tr class="odd">
<td><p>視訊</p></td>
<td><p>57500</p></td>
<td><p>8034</p></td>
</tr>
<tr class="even">
<td><p><strong>總數</strong></p></td>
<td><p>--</p></td>
<td><p>24730</p></td>
</tr>
</tbody>
</table>


正如您所看到的，您的音訊、視訊與應用程式共用連接埠範圍始於連接埠 40803，並總共包含 24732 個連接埠。您可依喜好設定某個 Edge Server，透過執行類似下列 Lync Server 管理命令介面命令以使用這些全部的連接埠值：

    Set-CsEdgeServer -Identity EdgeServer:atl-edge-001.litwareinc.com -MediaCommunicationPortStart 40803 -MediaCommunicationPortCount 24730

或者，使用下列命令以在組織中同時設定所有 Edge 伺服器：

    Get-CsService -EdgeServer | ForEach-Object {Set-CsEdgeServer -Identity $_.Identity -MediaCommunicationPortStart 40803 -MediaCommunicationPortCount 24730}

您可使用此 Lync Server 管理命令介面命令驗證 Edge 伺服器目前的連接埠設定：

    Get-CsService -EdgeServer | Select-Object Identity, MediaCommunicationPortStart, MediaCommunicationPortCount

