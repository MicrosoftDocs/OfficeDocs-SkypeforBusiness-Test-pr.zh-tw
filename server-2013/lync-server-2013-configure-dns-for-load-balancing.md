---
title: Lync Server 2013：設定 DNS 負載平衡
TOCTitle: 設定 DNS 負載平衡
ms:assetid: 1b2e8414-8676-4872-8ecf-ea07196f74de
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398251(v=OCS.15)
ms:contentKeyID: 49290246
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 DNS 負載平衡

 

_**上次修改主題的時間：** 2015-03-09_

若要順利完成此程序，您至少應該以 Domain Admins 群組成員或 DnsAdmins 群組成員的身分登入伺服器或網域。

網域名稱系統 (DNS) 負載平衡可以平衡 Lync Server 2013 的特有網路流量，例如 SIP 流量和媒體流量。前端集區、Edge 集區、Director 集區和獨立中繼集區支援 DNS 負載平衡。設定為使用 DNS 負載平衡的集區必須定義兩個完整網域名稱 (FQDN)：一般集區 FQDN，供 DNS 負載平衡使用 (例如 pool1.contoso.com) 和解析為集區中伺服器的實體 IP；以及供集區 Web 服務使用的另一個 FQDN (例如 web1.contoso.net)，會解析為集區的虛擬 IP 位址。如需 DNS 負載平衡的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的 DNS 負載平衡](lync-server-2013-dns-load-balancing.md)＞。

> [!NOTE]  
> 用戶端到伺服器的 HTTPS 流量仍需要硬體負載平衡。



您必須先進行下列步驟，才能使用 DNS 負載平衡：

1.  覆寫內部 Web 服務集區 FQDN。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果決定使用自行定義的 FQDN 來覆寫內部 Web 服務，每個 FQDN 都必須是唯一的，用於區分其他的 前端集區、 Director 或 Director 集區。</td>
    </tr>
    </tbody>
    </table>


2.  建立 DNS A 主機記錄，以便將集區 FQDN 解析為集區中所有伺服器的 IP 位址。

3.  啟用 IP 位址隨機化，或針對 Windows Server DNS 啟用循環配置資源。
    
    > [!NOTE]  
    > 預設應啟用循環配置資源。
    


## 覆寫內部 Web 服務 FQDN

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  從主控台樹狀目錄展開 Enterprise Edition 前端集區節點。

3.  以滑鼠右鍵按一下集區、按一下 **\[編輯內容\]** ，然後按一下 **\[Web 服務\]** 。

4.  在 **\[內部 Web 服務\]** 下方，選取 **\[覆寫 FQDN\]** 核取方塊。

5.  輸入用於解析為集區伺服器之實體 IP 位址的集區 FQDN。

6.  在 **\[外部 Web 服務\]** 下方，輸入用於解析為集區虛擬 IP 位址的外部集區 FQDN，然後按一下 **\[確定\]** 。

7.  在主控台樹狀目錄中，按一下 \[ Lync Server 2013\] ，然後在 \[動作\] 窗格中，按一下 \[發行拓撲\] 。

## 建立所有內部集區伺服器的 DNS 主機 (A) 記錄

1.  依序按一下 **\[開始\]** 、 **\[所有程式\]** 、 **\[系統管理工具\]** 和 **\[DNS\]** 。

2.  在 **\[DNS 管理員\]** 中，按一下管理記錄的 DNS 伺服器，將其展開。

3.  按一下 **\[正向對應區域\]** 將其展開。

4.  以滑鼠右鍵按一下您要新增記錄的 DNS 網域，然後按一下 **\[新增主機 (A 或 AAAA)\]** 。

5.  在 **\[名稱\]** 方塊中輸入主機記錄的名稱 (網域名稱會自動附加上去)。

6.  在 \[IP 位址\] 方塊中，輸入個別前端伺服器的 IP 位址，然後選取 **\[建立關聯的指標 (PTR) 記錄\]** 或 **\[允許已驗證的使用者更新相同擁有者名稱的 DNS 記錄\]** (如果適用的話)。

7.  繼續為其他將參與 DNS 負載平衡的所有成員前端伺服器建立記錄。
    
    例如，如果您有個名為 pool1.contoso.com 的集區以及三個前端伺服器，您可以建立下列 DNS 項目：
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>FQDN</th>
    <th>類型</th>
    <th>資料</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Pool1.contoso.com</p></td>
    <td><p>主機 (A)</p></td>
    <td><p>192.168.1.1</p></td>
    </tr>
    <tr class="even">
    <td><p>Pool1.contoso.com</p></td>
    <td><p>主機 (A)</p></td>
    <td><p>192.168.1.2</p></td>
    </tr>
    <tr class="odd">
    <td><p>Pool1.contoso.com</p></td>
    <td><p>主機 (A)</p></td>
    <td><p>192.168.1.3</p></td>
    </tr>
    </tbody>
    </table>
    
    如需建立 DNS 主機 (A) 記錄的詳細資訊，請參閱＜ [為 Lync Server 2013 設定 DNS 主機記錄](lync-server-2013-configure-dns-host-records.md)＞。

## 啟用 Windows Server 的循環配置資源

1.  依序按一下 **\[開始\]** 、 **\[所有程式\]** 、 **\[系統管理工具\]** 和 **\[DNS\]** 。

2.  展開 **\[DNS\]** ，以滑鼠右鍵按一下您要設定的 DNS 伺服器，然後按一下 **\[內容\]** 。

3.  按一下 **\[進階\]** 索引標籤，選取 **\[啟用循環配置資源\]** 和 **\[啟用網路遮罩次序\]** ，然後按一下 **\[確定\]** 。
    
    ![DNS 循環配置資源對話方塊](images/Gg398251.e7bf6125-8d78-4460-8401-0a8e7e21d305(OCS.15).jpg "DNS 循環配置資源對話方塊")

> [!NOTE]  
> 預設應啟用此功能。



## 請參閱

#### 概念

[Lync Server 2013 中的 DNS 負載平衡](lync-server-2013-dns-load-balancing.md)

