---
title: Lync Server 2013：發行拓撲
TOCTitle: 發行拓撲
ms:assetid: bfed3829-7a54-4b5c-a7cb-28871acd35e7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412935(v=OCS.15)
ms:contentKeyID: 49292197
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中發行拓撲

 

_**上次修改主題的時間：** 2012-09-08_

每次使用 拓撲產生器建置拓撲後，都必須將拓撲發行至 中央管理存放區中的資料庫，資料才能用於部署 Lync Server 2013。請使用下列程序發行拓撲。

## 若要發行拓撲

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  在 拓撲產生器的主控台樹狀目錄中，以滑鼠右鍵按一下 \[ Lync 2013\] ，然後按一下 \[發行拓撲\] 。

3.  在精靈的 **\[歡迎使用\]** 頁面上，按 **\[下一步\]** 。

4.  在 **\[拓撲產生器找到 CMS 存放區\]** 頁面上，按 **\[下一步\]** 。

5.  在 **\[建立其他資料庫\]** 頁面上，按 **\[下一步\]** 。

6.  當狀態表示已成功建立資料庫時，執行下列操作：
    
      - 若要檢視記錄檔，請按一下 **\[檢視記錄檔\]** 。
    
      - 按一下 **\[完成\]** ，關閉精靈。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果這是全新安裝 Edge Server 或 Edge 集區，您必須從現有 前端伺服器、 前端集區或 Standard Edition 伺服器 匯出 Edge Server 組態。若要匯出組態，請參閱＜ <a href="lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md">匯出 Lync Server 2013 拓撲並將拓撲複製到 Edge 安裝的外部媒體</a>＞。您將在 Edge Server 的設定和部署階段，透過 Lync Server 部署精靈從外部媒體或網路共用匯入組態檔案。<br />
        Edge Server 可運作且本機組態管理存放區資料庫已複寫內部部署後，就會發行後續的 Lync Server 2013 組態更新並複寫至 Edge Server。</td>
        </tr>
        </tbody>
        </table>

