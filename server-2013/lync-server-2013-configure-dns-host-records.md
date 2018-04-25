---
title: Lync Server 2013：設定 DNS 主機記錄
TOCTitle: 設定 DNS 主機記錄
ms:assetid: 78a1afcf-41c8-4da5-8740-c6570c19078c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398593(v=OCS.15)
ms:contentKeyID: 49291387
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 為 Lync Server 2013 設定 DNS 主機記錄

 

_**上次修改主題的時間：** 2012-10-01_

若要順利完成此程序，您至少應以 Domain Admins 群組成員或 DnsAdmins 群組成員的身分登入伺服器或網域。

## 若要設定 DNS 主機 A 記錄

1.  在網域名稱系統 (DNS) 伺服器上，依序按一下 \[開始\] 、\[系統管理工具\] 和 \[DNS\] 。

2.  在網域的主控台樹狀目錄中，展開 \[正向對應區域\] ，然後在要安裝 Lync Server 2013 的網域上按一下滑鼠右鍵。

3.  按一下 \[新增主機 (A 或 AAAA)\] 。

4.  按一下 **\[名稱\]** ，然後輸入集區的主機名稱 (網域名稱會以記錄定義所在的區域來假設，而不需輸入為 A 記錄的一部分)。

5.  按一下 **\[IP 位址\]** ，然後為 前端集區的負載平衡器輸入虛擬 IP (VIP)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在使用 Director 集區的部署中，簡單 URL 的主機 (A) 記錄應指向 Director 負載平衡器的 VIP。</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您僅部署一個不使用負載平衡器就連線至拓撲的 Enterprise Edition Server 或 Director，或是您部署了一部 Standard Edition Server，請輸入 Enterprise Edition Server、Standard Edition Server 或 Director 的 IP 位址。如果您要在集區中部署多個 Enterprise Edition Server 或 Director，則需要負載平衡器。負載平衡器無法用於 Standard Edition Server。</td>
    </tr>
    </tbody>
    </table>


6.  按一下 \[新增主機\] ，然後按一下 \[確定\] 。

7.  如果要建立其他的 A 記錄，請重複步驟 4 和 5。

8.  完成建立所需的所有 A 記錄時，按一下 **\[完成\]** 。

