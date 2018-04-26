---
title: Lync Server 2013：建立並驗證 DNS SRV 記錄
TOCTitle: 建立並驗證 DNS SRV 記錄
ms:assetid: 86888c7e-1401-458f-9a7b-08ac726deeec
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398680(v=OCS.15)
ms:contentKeyID: 49291556
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立並驗證 DNS SRV 記錄

 

_**上次修改主題的時間：** 2013-02-21_

若要順利完成此程序，您至少應該以 Domain Admins 群組成員或 DnsAdmins 群組成員的身分登入伺服器或網域。

本主題說明如何設定所有的 Lync Server 2013 部署中都必須建立的網域名稱系統 (DNS) 記錄，以及自動用戶端登入所需的 DNS 記錄。當您建立 前端集區 時，安裝程式會針對集區建立 Active Directory 物件和設定，包括集區的完整網域名稱 (FQDN)。亦會針對 Standard Edition 伺服器 建立相似的物件和設定。為了要讓用戶端能夠連接到集區或 Standard Edition 伺服器，此集區或 Standard Edition 伺服器 的 FQDN 必須在 DNS 中註冊。您必須為每個 SIP 網域在內部 DNS 中建立 DNS SRV 記錄。此程序假設您的內部 DNS 具有 SIP 使用者網域的區域。

## 設定 DNS SRV 記錄

1.  在 DNS 伺服器上，依序按一下 \[開始\] 、\[系統管理工具\] 和 \[DNS\] 。

2.  在 SIP 網域的主控台樹狀目錄中，展開 \[正向對應區域\] ，然後在要安裝 Lync Server 2013 的 SIP 網域上按一下滑鼠右鍵。

3.  按一下 \[新增其他記錄\] 。

4.  在 **\[選擇資源記錄類型\]** 中，按一下 **\[服務位置 (SRV)\]** ，然後按一下 **\[建立記錄\]** 。

5.  按一下 **\[服務\]** ，然後輸入 **\_sipinternaltls** 。

6.  按一下 \[通訊協定\]，然後輸入 **\_tcp**。

7.  按一下 \[連接埠號碼\]，然後輸入 **5061**。

8.  按一下 **\[提供這項服務的主機\]** ，然後輸入集區或 Standard Edition 伺服器 的 FQDN。

9.  按一下 \[確定\] ，然後再按一下 \[完成\] 。

## 若要確認 DNS SRV 記錄的建立

1.  以 Authenticated Users 群組成員的帳戶或具有相等權限的帳戶，登入網域中的用戶端電腦。

2.  按一下 \[開始\] ，然後再按一下 \[執行\] 。

3.  在 \[開啟\] 方塊中輸入 **cmd** ，然後按一下 \[確定\] 。

4.  在命令提示字元下，輸入 **nslookup** ，然後按 ENTER。

5.  輸入 **set type=srv** ，然後按 ENTER。

6.  輸入 **\_sipinternaltls.\_tcp.contoso.com** ，然後按 ENTER。所顯示的傳輸層安全性 (TLS) 記錄輸出如下：
    
    Server: *\<dns server\>*.contoso.com
    
    Address: *\<IP address of DNS server\>*
    
    Non-authoritative answer:
    
    \_sipinternaltls.\_tcp.contoso.com SRV service location:
    
    priority = 0
    
    weight = 0
    
    port = 5061
    
    svr hostname = poolname.contoso.com (或 Standard Edition server A record)
    
    poolname.contoso.com internet address = *\<virtual IP Address of the load balancer\>* 或 *\<IP address of a single Enterprise Edition server for pools with only one Enterprise Edition server\>* 或 *\<IP address of the Standard Edition server\>*

7.  完成時，在命令提示字元下輸入 **exit** ，然後按 ENTER。

## 確認可以解析前端集區或 Standard Edition Server 的 FQDN

1.  登入網域中的用戶端電腦。

2.  按一下 \[開始\] ，然後再按一下 \[執行\] 。

3.  在 \[開啟\] 方塊中輸入 **cmd** ，然後按一下 \[確定\] 。

4.  在命令提示字元中，輸入 **nslookup***\<FQDN of the Front End pool\>* 或 *\<FQDN of the Standard Edition server\>*，然後按下 ENTER。

5.  確認您收到回覆，且可解析為 FQDN 的適當 IP 位址。

