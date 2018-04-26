---
title: 更新 DNS SRV 記錄
TOCTitle: 更新 DNS SRV 記錄
ms:assetid: a29149aa-30cc-4a59-af98-fb95c2385cce
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688161(v=OCS.15)
ms:contentKeyID: 49890239
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 更新 DNS SRV 記錄

 

_**上次修改主題的時間：** 2012-09-29_

若要順利完成此程序，您應該以 Domain Admins 群組成員或 DnsAdmins 群組成員的身分登入伺服器或網域。

本主題說明如何在移轉至 Lync Server 2013 之後更新網域名稱系統 (DNS) 記錄。在所有使用者移到 Lync Server 2013 之後，但在解除委任舊版 Office Communications Server 2007 R2 集區或 Director 之前，您必須在每一個 SIP 網域的內部 DNS 中更新 DNS SRV 記錄。此程序假設您的內部 DNS 具有 SIP 使用者網域的區域。

**設定 DNS SRV 記錄**

1.  在 DNS 伺服器上，依序按一下 \[開始\] 、\[系統管理工具\] 和 \[DNS\] 。

2.  在 SIP 網域的主控台樹狀目錄中，依序展開 \[正向對應區域\] 和安裝 Lync Server 2013 的 SIP 網域，然後瀏覽至 \[\_tcp\] 設定。

3.  在右窗格中，用滑鼠右鍵按一下 **\_sipinternaltls** 並選取 \[內容\] 。

4.  在 \[提供這項服務的主機\] 中，更新主機 FQDN 以指向 Lync Server 2013 集區。

5.  按一下 \[確定\] 。

**確認可以解析前端集區或 Standard Edition Server 的 FQDN**

1.  登入網域中的用戶端電腦。

2.  按一下 \[開始\] ，然後再按一下 \[執行\] 。

3.  在 \[開啟\] 方塊中輸入 **cmd** ，然後按一下 \[確定\] 。

4.  在命令提示字元中，輸入 **nslookup***\<FQDN of the Front End pool\>* 或 *\<FQDN of the Standard Edition server\>*，然後按下 ENTER。

5.  確認您收到回覆，且可解析為 FQDN 的適當 IP 位址。

