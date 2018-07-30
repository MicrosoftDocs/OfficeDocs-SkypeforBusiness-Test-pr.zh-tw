---
title: 設定自動探索的 DNS
TOCTitle: 設定自動探索的 DNS
ms:assetid: f07a634c-3cf3-4958-8556-84596319ef54
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945656(v=OCS.15)
ms:contentKeyID: 52056258
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定自動探索的 DNS

 

_**上次修改主題的時間：** 2012-12-12_

若要支援 Lync 用戶端的自動探索，您必須建立下列網域名稱系統 (DNS) 記錄：

  - 用以支援從組織網路內部連線之Lync 用戶端的內部 DNS 記錄

  - 用以支援從網際網路連線之 Lync 用戶端的外部 (或公用) DNS 記錄

您必須針對每個 SIP 網域建立內部 DNS 記錄和外部 DNS。

DNS 記錄可以是 A (主機) 記錄或 CNAME 記錄，這取決於您建立具有其他主體替代名稱 (SAN) 之新憑證的能力。如果您無法要求和部署具有 lyncdiscover.\<網域名稱\> SAN 之新的外部 (公用) 憑證，請使用程序以使用連接埠 HTTP/TCP 80。下列程序說明如何建立內部和外部 DNS 記錄。

## 建立 DNS CNAME 記錄

1.  登入 DNS 伺服器，如下所示：
    
      - 建立內部 DNS 記錄，以 Domain Admins 群組或 DnsAdmins 群組成員身分登入網路中的 DNS 伺服器。
    
      - 若要建立外部 DNS 記錄，請連線至公用 DNS 提供者。

2.  開啟 DNS 系統管理嵌入式管理單元：依序按一下 \[開始\]、\[系統管理工具\] 和 \[DNS\]。

3.  請執行下列其中一項動作：
    
      - 若為內部 DNS 記錄，在 DNS 伺服器的主控台樹狀目錄中展開 Active Directory 網域 (例如 contoso.local) 的 \[正向對應區域\]。
        
        > [!NOTE]  
        > 此網域是 Lync Server 2013 Director 集區和前端集區安裝所在的 Active Directory 網域。
        
    
      - 若為外部 DNS 記錄，在 DNS 伺服器的主控台樹狀目錄中展開 SIP 網域 (例如 contoso.com) 的 \[正向對應區域\]。

4.  確認 Director 集區的主機 A 記錄存在，如下所示：
    
      - 若為內部 DNS 記錄，Director 集區的內部 Web 服務完整網域名稱 (FQDN) 應有主機 A 記錄存在 (例如 lyncwebdir01.contoso.local)。
    
      - 若為外部 DNS 記錄，Director 集區的外部 Web 服務完整網域名稱 (FQDN) 應有主機 A 記錄存在 (例如 lyncwebextdir.contoso.com)。

5.  確認前端集區的主機 A 記錄存在，如下所示：
    
      - 若為內部 DNS 記錄，前端集區的內部 Web 服務完整網域名稱 (FQDN) 應有主機 A 記錄存在 (例如 lyncwebpool01.contoso.local)。
    
      - 若為外部 DNS 記錄，前端集區的內部 Web 服務完整網域名稱 (FQDN) 應有主機 A 記錄存在 (例如 lyncwebextpool01.contoso.com)。

6.  若為內部 DNS 記錄，在 DNS 伺服器的主控台樹狀目錄中，展開 SIP 網域 (例如 contoso.com) 的 \[正向對應區域\]。
    
    > [!NOTE]  
    > 如果您正在建立外部 DNS 記錄，從步驟 3 就已展開 SIP 網域的 [正向對應區域]。
    


7.  在 SIP 網域名稱上按一下滑鼠右鍵，然後按一下 \[新增別名 (CNAME)\]。

8.  在 \[別名\] 中，輸入下列其中一項：
    
      - 若為內部 DNS 記錄，輸入 lyncdiscoverinternal 做為內部自動探索服務 URL 的主機名稱。
    
      - 若為外部 DNS 記錄，輸入 lyncdiscover 做為外部自動探索服務 URL 的主機名稱。

9.  在 \[目標主機完整網域名稱 (FQDN)\] 中，執行下列其中一項動作：
    
      - 若為內部 DNS 記錄，輸入或瀏覽 Director 集區的內部 Web 服務 FQDN (例如 lyncwebdir01.contoso.local)，然後按一下 \[確定\]。
    
      - 若為外部 DNS 記錄，輸入或瀏覽 Director 集區的外部 Web 服務 FQDN (例如 lyncwebextdir.contoso.com)，然後按一下 \[確定\]。
    
    > [!NOTE]  
    > 如果您沒有使用 Director，請使用前端集區的內部和外部 Web 服務 FQDN，或者，若為單一伺服器，請使用前端伺服器或 Standard Edition 伺服器的 FQDN。
    
    
    > [!IMPORTANT]  
    > 您必須在 Lync Server 2013 環境中，針對您所支援之每個 SIP 網域的正向對應區域，建立新的自動探索 CNAME 記錄。
    


## 建立 DNS A 記錄

1.  登入 DNS 伺服器，如下所示：
    
      - 建立內部 DNS 記錄，以 Domain Admins 群組或 DnsAdmins 群組成員身分登入網路中的 DNS 伺服器。
    
      - 若要建立外部 DNS 記錄，請連線至公用 DNS 提供者或外部 DNS 伺服器。

2.  開啟 DNS 系統管理嵌入式管理單元：依序按一下 \[開始\]、\[系統管理工具\] 和 \[DNS\]。

3.  請執行下列其中一項動作：
    
      - 若為內部 DNS 記錄，在 DNS 伺服器的主控台樹狀目錄中展開 Active Directory 網域 (例如 contoso.local) 的 \[正向對應區域\]。
        
        > [!NOTE]  
        > 此網域是 Lync Server 2013 Director 集區和前端集區安裝所在的 Active Directory 網域。
        
    
      - 若為外部 DNS 記錄，在 DNS 伺服器的主控台樹狀目錄中展開 SIP 網域 (例如 contoso.com) 的 \[正向對應區域\]。

4.  確認 Director 集區的主機 A (IPv6 為 AAAA) 記錄存在，如下所示：
    
      - 若為內部 DNS 記錄，Director 集區的內部 Web 服務 FQDN (例如 lyncwebdir01.contoso.local) 應有主機 A (IPv6 為 AAAA) 記錄存在。
    
      - 若為外部 DNS 記錄，Director 集區的外部 Web 服務 FQDN (例如 lyncwebextdir.contoso.com) 應有主機 A (IPv6 為 AAAA) 記錄存在。

5.  確認前端集區的主機 A (IPv6 為 AAAA) 記錄存在，如下所示：
    
      - 若為內部 DNS 記錄，前端集區的內部 Web 服務 FQDN (例如 lyncwebpool01.contoso.local) 應有主機 A (IPv6 為 AAAA) 記錄存在。
    
      - 若為外部 DNS 記錄，前端集區的外部 Web 服務 FQDN (例如 lyncwebextpool01.contoso.com) 應有主機 A (IPv6 為 AAAA) 記錄存在。

6.  若為內部 DNS 記錄，在 DNS 伺服器的主控台樹狀目錄中，展開 SIP 網域 (例如 contoso.com) 的 \[正向對應區域\]。
    
    > [!NOTE]  
    > 如果您正在建立外部 DNS 記錄，從步驟 3 就已展開 SIP 網域的 [正向對應區域]。
    


7.  在 SIP 網域名稱上按一下滑鼠右鍵，然後按一下 \[新增主機 (A 或 AAAA)\]。

8.  在 \[名稱\] 中，輸入主機名稱，如下所示：
    
      - 若為內部 DNS 記錄，輸入 lyncdiscoverinternal 做為內部自動探索服務 URL 的主機名稱。
    
      - 若為外部 DNS 記錄，輸入 lyncdiscover 做為外部自動探索服務 URL 的主機名稱。
    
    > [!NOTE]  
    > 網域名稱是從定義記錄所在的區域取得，因此，不需要輸入為 A 記錄的一部分。
    


9.  在 \[IP 位址\] 中，輸入 IP 位址，如下所示：
    
      - 若為內部 DNS 記錄，輸入 Director 的內部 Web 服務 IP 位址 (或者，如果您使用負載平衡器，則輸入 Director 負載平衡器的虛擬 IP (VIP))。
        
        > [!NOTE]  
        > 如果您沒有使用 Director，請輸入前端伺服器或 Standard Edition 伺服器 IP 位址，或者，如果您使用負載平衡器，則輸入前端集區負載平衡器的 VIP。
        
    
      - 若為外部 DNS 記錄，輸入反向 Proxy 的外部或公用 IP 位址。

10. 按一下 \[新增主機\]，然後按一下 \[確定\]。

11. 若要建立其他 A 記錄，請重複步驟 8 至 10。
    
    > [!IMPORTANT]  
    > 您必須在 Lync Server 2013 環境中，針對您所支援之每個 SIP 網域的正向對應區域，建立新的 lyncdiscover 和 lyncdiscoverinternal A 記錄。
    


12. 完成建立 A (IPv6 為 AAAA) 記錄後，按一下 \[完成\]。

