---
title: 'Lync Server 2013: Scanning for viruses and checking virus definitions'
TOCTitle: Scanning for viruses and checking virus definitions
ms:assetid: 287c0f43-82d1-4c1d-b08f-77112fcb5bfa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn720909(v=OCS.15)
ms:contentKeyID: 62240014
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Scanning for viruses and checking virus definitions in Lync Server 2013

 

_**上次修改主題的時間：** 2014-05-01_

We highly recommend installing an IM-level antivirus product. IM is a well-known source for quickly spreading both virus and malicious software throughout an organization. Microsoft Forefront® Security for Lync Server provides multi-engine scanning with virus, malicious software, file and keyword filter protection and seamless integration with Office Communications Server.

In addition to Forefront Security for Lync Server, we also highly recommend installing a file-level, antivirus solution to protect the server’s file system.

Keeping scanner engines and virus definitions updated is very important. Configuring and monitoring the health of the updates makes sure that the most current scanning information is being used to protect both Office Communications Server and file-system.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>When using a third-party, file-level antivirus software on a server that runs Lync Server 2013 and Forefront Security for Lync Server, make sure that the folders in which Forefront Security for Lync Server and the Lync Server are installed are not scanned, to prevent their corruption. For the full list of exclusions, see <a href="http://support.microsoft.com/kb/943620" class="uri">http://support.microsoft.com/kb/943620</a>.</td>
</tr>
</tbody>
</table>

