---
title: 設定試驗集區部署的 DNS 記錄
TOCTitle: 設定試驗集區部署的 DNS 記錄
ms:assetid: eb421bad-4bf1-4837-a077-7795094692d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721921(v=OCS.15)
ms:contentKeyID: 49890367
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定試驗集區部署的 DNS 記錄

 

_**上次修改主題的時間：** 2012-09-29_

部署 Lync Server 2013 試驗集區前，您必須更新試驗集區的 DNS 主機 A 項目。若要順利完成此程序，您應該以 Domain Admins 群組成員或 DnsAdmins 群組成員的身分登入伺服器或網域。

**若要設定 DNS 主機 A 記錄**

1.  在網域名稱系統 (DNS) 伺服器上，依序按一下 \[開始\] 、\[系統管理工具\] 和 \[DNS\] 。

2.  在網域的主控台樹狀目錄中，展開 \[正向對應區域\] ，然後在要安裝 Lync Server 2013 的網域上按一下滑鼠右鍵。

3.  按一下 \[新增主機 (A 或 AAAA)\] 。

4.  按一下 \[名稱\] ，然後輸入 Lync Server 2013 集區的主機名稱 (網域名稱會以記錄定義所在的區域來假設，而不需輸入為 A 記錄的一部分)。

5.  按一下 \[IP 位址\] ，輸入 前端集區的 IP 位址。

6.  按一下 \[新增主機\] ，然後按一下 \[確定\] 。

7.  完成時，按一下 \[完成\] 。

