---
title: 針對 Microsoft Lync 用戶端設定連接埠範圍
TOCTitle: 針對 Microsoft Lync 用戶端設定連接埠範圍
ms:assetid: 287d5cea-7ada-461c-9b4a-9da2af315e71
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204760(v=OCS.15)
ms:contentKeyID: 49290395
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Microsoft Lync 用戶端設定連接埠範圍

 

_**上次修改主題的時間：** 2015-03-09_

根據預設，當涉及通訊工作階段時，因為沒有為用戶端啟用特定連接埠範圍，所以 Lync 用戶端應用程式可使用連接埠 1024 及 65535 之間的所有連接埠。然而為了使用服務品質，您必須將各種流量類型重新分派 (音訊、視訊、媒體、應用程式共用及檔案傳輸) 至一系列的唯一連接埠範圍。使用 Set-CsConferencingConfiguration Cmdlet 可達成此目的。

您可以從 Microsoft Lync Server 2013 管理命令介面中執行下列命令，決定通訊工作階段目前要使用哪些連接埠範圍：

    Get-CsConferencingConfiguration

假設您在安裝 Lync Server 2013 之後，尚未對會議設定進行任何變更，應該會收到包含下列屬性值的資訊：

    ClientMediaPortRangeEnabled : False
    ClientAudioPort             : 5350
    ClientAudioPortRange        : 40
    ClientVideoPort             : 5350
    ClientVideoPortRange        : 40
    ClientAppSharingPort        : 5350
    ClientAppSharingPortRange   : 40
    ClientFileTransferPort      : 5350
    ClientTransferPortRange     : 40

若您仔細看前面的輸出，就會注意到兩項重點。首先，ClientMediaPortRangeEnabled 屬性是設為 False：

    ClientMediaPortRangeEnabled : False

其重要之處在於，當此屬性設為 False 時，若涉及通訊工作階段，Lync 用戶端就會使用連接埠 1024 及 65535 之間任一可使用的連接埠；無論使用任何其他連接埠設定 (例如 ClientMediaPort 或 ClientVideoPort)，都依然會產生此情況。若您想要限制特定一組連接埠的流量 (您如果打算實作服務品質時，就會需要這麼做)，就必須先啟用用戶端媒體連接埠範圍。您可使用下列 Windows PowerShell 命令完成此目的：

    Set-CsConferencingConfiguration -ClientMediaPortRangeEnabled $True

前面的命令會啟用全域會議組態設定集合的用戶端媒體連接埠；不過這些設定也可套用至網站範圍及/或服務範圍 (僅限會議伺服器服務)。若要啟用特定網站或伺服器的用戶端媒體連接埠範圍，請在呼叫 Set-CsConferencingConfiguration 時指定該網站或伺服器的識別：

    Set-CsConferencingConfiguration -Identity "site:Redmond" -ClientMediaPortRangeEnabled $True

或者，您也可使用此命令，同時啟用所有會議組態設定的連接埠範圍：

    Get-CsConferencingConfiguration | Set-CsConferencingConfiguration  -ClientMediaPortRangeEnabled $True

您注意到的第二項重點是範例輸出顯示，根據預設，針對每個網路流量類型所設定的媒體連接埠範圍皆為相同：

    ClientAudioPort             : 5350
    ClientVideoPort             : 5350
    ClientAppSharingPort        : 5350
    ClientFileTransferPort      : 5350

為了實作 QoS，其中的每個連接埠範圍皆必須是唯一的連接埠範圍。例如，您可能設定了如下的連接埠範圍：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端流量類型</th>
<th>連接埠開始</th>
<th>連接埠範圍</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>音訊</p></td>
<td><p>50020</p></td>
<td><p>20</p></td>
</tr>
<tr class="even">
<td><p>視訊</p></td>
<td><p>58000</p></td>
<td><p>20</p></td>
</tr>
<tr class="odd">
<td><p>應用程式共用</p></td>
<td><p>42000</p></td>
<td><p>20</p></td>
</tr>
<tr class="even">
<td><p>檔案傳輸</p></td>
<td><p>42020</p></td>
<td><p>20</p></td>
</tr>
</tbody>
</table>


在前面的表格中，用戶端連接埠範圍即為針對您伺服器所設定之連接埠範圍的子網路。例如，在伺服器上將應用程式共用設定為使用連接埠 40803 到 49151；在用戶端電腦上將應用程式共用設定為使用連接埠 42000 到 42019。這麼做也是為了使 QoS 的管理較為容易：其實用戶端連接埠不需要是伺服器使用之連接埠的子網路 (例如，您可在用戶端電腦上將應用程式共用設定為使用連接埠 10000 到 10019)。但仍建議您將用戶端連接埠範圍設為伺服器連接埠範圍的子網路。

此外，您可能還有注意到，在伺服器上針對應用程式共用獨立設定了 8348 個連接埠，但用戶端上的應用程式共用僅獨立設定了 20 個連接埠。雖然這也是推薦的設定，卻不是需要嚴格遵守的規則。一般而言，您可將每個可用的連接埠視為代表單一通訊工作階段：若您在連接埠範圍中有 100 個可用的連接埠，表示先前提到的電腦最多可隨時參與 100 個通訊工作階段。因為伺服器可能會比用戶端參與更多的交談，所以在伺服器上開啟比用戶端更多的連接埠也很合理。為應用程式共用在用戶端上獨立設定 20 個連接埠，表示使用者可在特定裝置上同時參與 20 個應用程式共用工作階段。這對於您絕大多數的使用者而言應該已足夠使用。

若要將先前的連接埠範圍指派給全域會議組態設定集合，可以使用下列 Lync Server 管理命令介面命令：

    Set-CsConferencingConfiguration -Identity global -ClientAudioPort 50020 -ClientAudioPortRange 20 -ClientVideoPort 58000 -ClientVideoPortRange 20 -ClientAppSharingPort 42000 -ClientAppSharingPortRange 20 - ClientFileTransferPort 42020 -ClientFileTransferPortRange 20

或是使用此命令將這些相同的連接埠範圍指派給所有會議組態設定：

    Get-CsConferencingConfiguration | Set-CsConferencingConfiguration -ClientAudioPort 50020 -ClientAudioPortRange 20 -ClientVideoPort 58000 -ClientVideoPortRange 20 -ClientAppSharingPort 42000 -ClientAppSharingPortRange 20 - ClientFileTransferPort 42020 -ClientFileTransferPortRange 20

個別使用者必須登出 Lync，然後再次登入，才能使這些變更生效。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以使用單一命令啟用用戶端媒體連接埠範圍，然後指派這些連接埠範圍，例如：<br />
<code>Set-CsConferencingConfiguration -ClientMediaPortRangeEnabled $True -ClientAudioPort 50020 -ClientAudioPortRange 20 -ClientVideoPort 58000 -ClientVideoPortRange 20 -ClientAppSharingPort 42000 -ClientAppSharingPortRange 20 -ClientFileTransferPort 42020 -ClientFileTransferPortRange 20</code></td>
</tr>
</tbody>
</table>

