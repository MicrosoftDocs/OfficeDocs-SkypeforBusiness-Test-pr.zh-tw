---
title: Lync Server 2013：針對與主控 Exchange UM 的整合建立 DNS SRV 記錄
TOCTitle: 針對與主控 Exchange UM 的整合建立 DNS SRV 記錄
ms:assetid: 8ea590ae-58ea-4ca5-9853-e0708b3ea760
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh500728(v=OCS.15)
ms:contentKeyID: 49291622
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對與主控 Exchange UM 的整合建立 DNS SRV 記錄

 

_**上次修改主題的時間：** 2013-02-20_

本主題說明如何設定所需的網域名稱系統 (DNS) SRV 記錄，以供 Lync Server 2013  Edge Server 路由傳送到裝載的 Exchange 服務，例如 Microsoft Exchange Online。

## 為裝載的 Exchange 服務建立外部 DNS SRV 記錄

1.  以 DnsAdmins 群組成員的身分登入外部 DNS 伺服器。

2.  依序按一下 \[開始\] 、\[系統管理工具\] 和 \[DNS\] 。

3.  在 SIP 網域的主控台樹狀目錄中，展開 \[正向對應區域\] ，然後選取要安裝 Lync Server 2013 的 SIP 網域。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您必須在已安裝或將要安裝 Lync Server 的 SIP 網域中，建立 DNS SRV 記錄。當您建立 SRV 記錄時，用於提供此服務欄位之主機的 FQDN，必須是 Edge 集區的外部 FQDN。例如，如果 Edge 集區的外部 FQDN 是 edge01.contoso.net，則輸入該值。這也必須在與 DNS 主機 (A) 記錄相同的網域中。</td>
    </tr>
    </tbody>
    </table>


4.  用滑鼠右鍵按一下選取的網域，然後按一下 \[新增其他記錄\] 。

5.  在 \[資源記錄類型\] 中，按一下 \[服務位置 (SRV)\] ，然後按一下 \[建立記錄\] 。

6.  在 \[新增資源記錄\] 中，按一下 \[服務\] ，然後輸入 **\_sipfederationtls** 。

7.  按一下 \[通訊協定\] ，然後輸入 **\_tcp** 。

8.  按一下 \[連接埠號碼\] ，然後輸入 **5061** 。

9.  按一下 \[提供這項服務的主機\] ，然後輸入為信任的外部用戶端提供 Lync Server 2013 系統存取權之 Lync Server 2013  Edge 集區的完整網域名稱 (FQDN)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>網域也必須在您的 Exchange Online 設定中，設定為系統授權、接受的網域。如需詳細資訊，請參閱＜建立公認的網域＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=229762%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=229762&amp;clcid=0x404</a>。</td>
    </tr>
    </tbody>
    </table>


10. 按一下 \[確定\] ，然後再按一下 \[完成\] 。

## 確認已成功建立 DNS SRV 記錄

1.  登入網域中的用戶端電腦。

2.  按一下 \[開始\] ，然後再按一下 \[執行\] 。

3.  在命令提示字元中執行下列命令：
    
        nslookup <FQDN Lync Edge Pool>

4.  確認您收到回覆，且可解析為 FQDN 的適當 IP 位址。

## 請參閱

#### 概念

[在 Lync Server 2013 中建立反向 Proxy 伺服器的 DNS 記錄](lync-server-2013-create-dns-records-for-reverse-proxy-servers.md)

