---
title: 還原檔案存放區
TOCTitle: 還原檔案存放區
ms:assetid: 89916fc6-31d3-4c7f-9eaf-c02584761ef4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202180(v=OCS.15)
ms:contentKeyID: 52056166
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 還原檔案存放區

 

_**上次修改主題的時間：** 2013-02-18_

Standard Edition 的檔案存放區通常位於 Standard Edition 伺服器中。Enterprise Edition 的檔案存放區通常位於檔案伺服器或叢集中。以下程序說明如何還原檔案存放區。

## 還原檔案存放區

1.  若檔案存放區故障，請從 $Backup\\ 將合適的檔案存放區複製到檔案伺服器或 Standard Edition 伺服器 上的檔案存放區所在位置，然後共用該資料夾。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>還原後之檔案存放區的路徑與檔案名稱應與備份的檔案存放區完全相同，如此使用該檔案的元件才可存取使用。</td>
    </tr>
    </tbody>
    </table>


2.  如有需要，可為檔案存放區設定存取控制清單 (ACL)。在命令列中輸入：
    
        Enable-CsTopology
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若在還原程序期間未執行拓撲產生器，您才需要操作此步驟。</td>
    </tr>
    </tbody>
    </table>

