---
title: 針對會議、應用程式及中繼伺服器設定連接埠範圍
TOCTitle: 針對會議、應用程式及中繼伺服器設定連接埠範圍
ms:assetid: 4d6eaa5d-0127-453f-be6a-e55384772d83
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204872(v=OCS.15)
ms:contentKeyID: 49290867
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對會議、應用程式及中繼伺服器設定連接埠範圍

 

_**上次修改主題的時間：** 2015-04-30_

為了實作服務品質 (QoS) ，您應該為在會議、應用程式和中繼伺服器上共用的音訊、視訊和應用程式共用，設定完全相同的連接埠範圍；此外，這些連接埠範圍不得以任何方式重疊。舉個簡單的例子，假設您針對會議伺服器上的視訊使用連接埠 10000 到 10999。這表示您也必須為應用程式和中繼伺服器上的視訊保留連接埠 10000 到 10999。如果沒有，服務品質 (QoS) 將無法如預期般運作。

同樣地，假設您為視訊保留連接埠 10000 到 10999，但接著為音訊保留連接埠 10500 到 11999。這樣會造成服務品質的問題，因為連接埠範圍重疊。使用服務品質 (QoS) 時，每一種模式都必須有一組唯一的連接埠：如果您對視訊使用連接埠 10000 到 10999，則必須使用不同的範圍 (例如，對音訊使用 11000 到 11999)。

依預設，音訊和視訊連接埠範圍在 Microsoft Lync Server 2013 中不會重疊；不過，指派給應用程式共用的連接埠範圍則會同時與音訊和視訊連接埠範圍重疊 (也就是說，這些範圍都不是唯一的)。您可以從 Lync Server 2013 管理命令介面中執行下列三個命令，確認您的會議、應用程式和中繼伺服器的現有連接埠範圍：

    Get-CsService -ConferencingServer | Select-Object Identity, AudioPortStart, AudioPortCount, VideoPortStart, VideoPortCount, AppSharingPortStart, AppSharingPortCount
    
    Get-CsService -ApplicationServer | Select-Object Identity, AudioPortStart, AudioPortCount
    
    Get-CsService -MediationServer | Select-Object Identity, AudioPortStart, AudioPortCount

<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如同您在上述命令中所見，每一種連接埠類型 (音訊、視訊和應用程式共用) 都會被指派兩個不同的屬性值：連接埠起點和連接埠計數。連接埠起點指出用於該形式的第一個連接埠；例如，如果音訊連接埠起點等於 50000，表示用於音訊流量的第一個連接埠是連接埠 50000。如果音訊連接埠計數是 2 (這不是有效值，在這裡是作為說明之用) 表示只為音訊配置 2 個連接埠。如果第一個連接埠是連接埠 50000，且總共有兩個連接埠，表示第二個連接埠一定是連接埠 50001 (連接埠範圍必須是連續的)。因此，音訊的連接埠範圍將會是連接埠 50000 到 50001 (含)。<br />
另請注意，應用程式伺服器和中繼伺服器只支援音訊的服務品質；您不需要在應用程式伺服器或中繼伺服器中變更視訊或應用程式共用連接埠。</td>
</tr>
</tbody>
</table>


如果您執行上述三個命令，會看到 Lync Server 2013 的預設連接埠值設定如下：


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>會議伺服器</th>
<th>應用程式伺服器</th>
<th>中繼伺服器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AudioPortStart</p></td>
<td><p>49152</p></td>
<td><p>49152</p></td>
<td><p>49152</p></td>
</tr>
<tr class="even">
<td><p>AudioPortCount</p></td>
<td><p>8348</p></td>
<td><p>8348</p></td>
<td><p>8348</p></td>
</tr>
<tr class="odd">
<td><p>VideoPortStart</p></td>
<td><p>57501</p></td>
<td><p>--</p></td>
<td><p>--</p></td>
</tr>
<tr class="even">
<td><p>VideoPortCount</p></td>
<td><p>8034</p></td>
<td><p>--</p></td>
<td><p>--</p></td>
</tr>
<tr class="odd">
<td><p>ApplicationSharingPortStart</p></td>
<td><p>49152</p></td>
<td><p>--</p></td>
<td><p>--</p></td>
</tr>
<tr class="even">
<td><p>ApplicationSharingPortCount</p></td>
<td><p>16383</p></td>
<td><p>--</p></td>
<td><p>--</p></td>
</tr>
</tbody>
</table>


如前所述，在為服務品質設定 Lync Server 連接埠時，您應該要確定：1) 您的會議、應用程式和中繼伺服器上的音訊連接埠設定都是完全相同的；以及 2) 連接埠範圍沒有重疊。如果您仔細查看上表，會看到三種伺服器類型的連接埠範圍是完全相同的。例如，每種伺服器類型的起始音訊連接埠都是設定為連接埠 49152，而在每部伺服器中為音訊保留的連接埠總數也是相同的：8348。然而，連接埠範圍卻有重疊：音訊連接埠從連接埠 49152 開始，但為應用程式共用預留的連接埠也是一樣。為了善加利用服務品質，應用程式共用應該重新設定為使用唯一的連接埠範圍。例如，您可以將應用程式共用設定為從連接埠 40803 開始，以及使用 8348 個連接埠。(為什麼是 8348 個連接埠？如果您加總這些值 -- 40803 + 8348 -- 表示應用程式共用將會使用連接埠 40803 到連接埠 49151。由於音訊連接埠是從連接埠 49152 開始，因此您不再會有任何重疊的連接埠範圍。)

在為應用程式共用選取新的連接埠範圍之後，可以使用 Set-CsConferencingServer Cmdlet 進行變更。您不需要在應用程式伺服器或中繼伺服器上進行這項變更，因為這些伺服器不會處理應用程式共用流量。如果您決定要重新指派用於音效流量的連接埠，只要在這些伺服器上變更連接埠值即可。

如果要修改單一會議伺服器上應用程式共用的連接埠值，請從 Lync Server 管理命令介面中執行類似下列的命令：

    Set-CsConferenceServer -Identity ConferencingServer:atl-cs-001.litwareinc.com -AppSharingPortStart 40803 -AppSharingPortCount 8348

如果您要在所有的會議伺服器上進行這些變更，可以改為執行下列命令：

    Get-CsService -ConferencingServer | ForEach-Object {Set-CsConferenceServer -Identity $_.Identity -AppSharingPortStart 40803 -AppSharingPortCount 8348}

在變更連接埠設定之後，您應該要先停止，然後再重新啟動每一項受到變更影響的服務。

您的會議伺服器、應用程式伺服器和中繼伺服器並不是一定要共用完全相同的連接埠範圍；唯一必要的需求是您要在所有的伺服器上預留唯一的連接埠範圍。不過，如果您在所有伺服器上使用同一組連接埠，通常會讓管理工作更為輕鬆。

