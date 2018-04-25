---
title: 設定 Microsoft Lync Phone Edition 裝置上的服務品質
TOCTitle: 設定 Microsoft Lync Phone Edition 裝置上的服務品質
ms:assetid: a6eb2620-a512-4ab6-bdfd-eb76be43bbfe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205137(v=OCS.15)
ms:contentKeyID: 49291918
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Microsoft Lync Phone Edition 裝置上的服務品質

 

_**上次修改主題的時間：** 2012-11-01_

雖然 iPhone 等裝置並未預設啟用服務品質 (QoS)，但執行 Lync Phone Edition 的裝置預設會啟用 Qos (這些裝置通常是指 UC 或整合通訊電話)。若要進行確認，請在 Lync Server 管理命令介面中執行下列 Windows PowerShell 命令：

    Get-CsUCPhoneConfiguration

如果您尚未變更 UC 電話組態設定，則會收到如下的資訊：

    Identity             : Global
    CalendarPollInterval : 00:03:00
    EnforcePhoneLock     : True
    PhoneLockTimeout     : 00:10:00
    MinPhonePinLength    : 6
    SIPSecurityMode      : High
    VoiceDiffServTag     : 40
    Voice8021p           : 0
    LoggingLevel         : Off

就服務品質而言，只有其中一個內容有幫助：VoiceDiffServTag。VoiceDiffServTag 代表指派給從 Lync Phone Edition 裝置發出之語音流量的 DSCP 值。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 2013 不再支援 Voice8021p 參數。此參數仍然有效，具備 Microsoft Lync Server 2010 的回溯相容性；但是，對搭配 Lync Server 2013 使用的裝置沒有作用。</td>
</tr>
</tbody>
</table>


在大多數網路中，將 Lync Phone Edition 封包的 VoiceDiffServTag 標示為 40 不該造成任何問題。但是，40 不是通常用於音訊流量的值；音訊流量幾乎是以 DSCP 代碼 46 來標示。為了維護您整個網路的一致性，可以將 UC 電話的 VoiceDiffServTag 內容變更為 46。

您可以使用 Windows PowerShell 或 Lync Server 控制台來執行此作業。若要使用 Windows PowerShell 修改 VoiceDiffServTag 值，請在 Lync Server 管理命令介面中執行下列命令：

    Set-CsUCPhoneConfiguration -VoiceDiffServTag 46

上述命令會修改 UC 電話組態設定的全域集合。請注意，也可以將 UC 電話設定指派到網站範圍。若要修改網站範圍的 UC 電話組態設定，您必須指定網站身分。例如：

    Set-CsUCPhoneConfiguration -Identity "site:Redmond" -VoiceDiffServTag 46

您也可以使用下列命令同時修改所有 UC 電話組態設定：

    Get-CsUCPhoneConfiguration | Set-CsUCPhoneConfiguration -VoiceDiffServTag 46

如果您偏好使用 Lync Server 控制台來進行此變更，則請啟動 \[控制台\]，然後完成下列程序：

1.  按一下 \[用戶端\]，然後按一下 \[裝置組態\]。

2.  在 \[裝置組態\] 索引標籤上，按兩下要修改的設定集合 (例如，\[全域\])。

3.  在 \[編輯裝置組態\] 對話方塊中，將 \[語音服務品質 (QoS)\] 方塊的值設定為 \[46\]，然後按一下 \[認可\]。

如果有多個集合，您必須針對每個 UC 電話設定集合重複執行此程序。Lync Server 控制台不允許您同時修改多個設定集合。

如果組織中有些裝置並非使用 Windows 作業系統 (例如 iPhone)，則變更 VoiceDiffServTag 設定不會影響這些裝置。如果您要變更這些裝置的 DSCP 值，您必須參考各裝置類型的系統管理手冊。

