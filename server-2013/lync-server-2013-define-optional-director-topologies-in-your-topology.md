---
title: Lync Server 2013：在拓撲中定義選用的 Director 拓撲
TOCTitle: 在拓撲中定義選用的 Director 拓撲
ms:assetid: 8e9a659d-23b0-401d-b296-59c7df414d49
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398717(v=OCS.15)
ms:contentKeyID: 49291621
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 在拓撲中定義選用的 Director 拓撲

 

_**上次修改主題的時間：** 2012-09-08_

Lync Server 2013 Director 可以是單一執行個體伺服器，也能安裝為由多個 Director 構成的負載平衡集區，以提供更高的可用性和更大的容量。硬體負載平衡和網域名稱系統 (DNS) 負載平衡均可支援。本主題說明如何為 Director 集區設定 DNS 負載平衡。

若要在新增或移除伺服器角色時成功發行、啟用或停用拓撲，您應以 **RTCUniversalServerAdmins** 和 **Domain Admins** 等群組成員的使用者身分登入。您也可以委派適當的系統管理員權限用於新增伺服器角色。如需詳細資訊，請參閱 Standard Edition Server 或 Enterprise Edition Server 部署文件中的＜ [在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)＞。若要進行其他組態變更，則僅需要 **RTCUniversalServerAdmins** 群組的成員資格。

本主題說明用來定義和發行適用於兩個 Director 拓撲之拓撲的步驟：

  - 定義 Director (單一執行個體)

  - 定義 Director (多個 Director 集區)

## 定義 Director (單一執行個體)

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  按一下歡迎頁面中的 \[從現有部署下載拓撲\] 。

3.  在 \[另存拓撲\] 對話方塊中，輸入現有拓撲之本機複本的名稱和位置，然後按一下 \[儲存\] 。

4.  展開計畫要新增 Director 的網站，以滑鼠右鍵按一下 \[Director 集區\] ，然後按一下 \[新增 Director 集區\] 。

5.  在 \[定義 Director 集區 FQDN\] 對話方塊中，執行以下動作：
    
      - 在 \[集區 FQDN\] 中，輸入 Director 集區的 FQDN。
    
      - 按一下 **\[單一電腦集區\]** ，然後按 **\[下一步\]** 。

6.  在 \[定義檔案共用\] 對話方塊中，執行下列其中一項動作：
    
    1.  若要使用現有的檔案共用，請按一下 \[使用先前定義的檔案共用\] 並從清單中選取檔案共用，然後按 \[下一步\] 。
    
    2.  若要建立新的檔案共用，請按一下 \[定義新的檔案共用\] 、在 \[檔案伺服器 FQDN\] 中輸入檔案共用之位置的 FQDN、在 \[檔案共用\] 中輸入共用的名稱，然後按 \[下一步\] 。
    
    > [!IMPORTANT]  
    > 於此步驟指定或建立的檔案共用必須已存在，或是在發行拓撲之前完成建立。<br />
    > 系統實際上不會使用指派給 Director 的檔案共用，因此您可以指派組織中任何集區的檔案共用。


7.  在 \[指定 Web 服務 URL\] 對話方塊的 \[外部基底 URL\] 中，指定 Director 的 FQDN，然後按一下 \[完成\] 。
    
    > [!IMPORTANT]  
    > 名稱必須可從網際網路 DNS 伺服器解析，且必須指向反向 Proxy 的公用 IP 位址。反向 Proxy 會接聽該 URL 的 HTTP/HTTPS 要求，並代為將 URL 傳送至 Director 上的外部 Web 服務虛擬目錄。
    
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您有一個以上的 前端集區或 前端伺服器，則外部 Web 服務 FQDN 必須是唯一的。例如，如果您將 前端伺服器的外部 Web 服務 FQDN 定義為 <strong>pool01.contoso.com</strong>，便無法針對其他的 前端集區或 前端伺服器使用 <strong>pool01.contoso.com</strong>。如果您同時部署了 Director，則針對任何 Director 或 Director 集區定義的外部 Web 服務 FQDN，在任何其他 Director 或 Director 集區以及任何 前端集區或 前端伺服器中必須是唯一的。如果決定以自我定義的 FQDN 覆寫內部 Web 服務，各個 FQDN 必須與其他任何 前端集區、 Director 或 Director 集區各不相同。</td>
    </tr>
    </tbody>
    </table>


8.  發行拓撲。

## 定義 Director (多個 Director 集區)

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  按一下歡迎頁面中的 \[從現有部署下載拓撲\] 。

3.  在 \[另存拓撲\] 對話方塊中，輸入現有拓撲之本機複本的名稱和位置，然後按一下 \[儲存\] 。

4.  展開計畫要新增 Director 的網站，以滑鼠右鍵按一下 \[Director 集區\] ，然後按一下 \[新增 Director 集區\] 。

5.  在 \[定義 Director 集區 FQDN\] 對話方塊中，執行以下動作：
    
      - 在 \[集區 FQDN\] 中，輸入 Director 集區的 FQDN。
    
      - 按一下 \[多部電腦集區\] ，然後按 \[下一步\] 。

6.  在 \[定義此集區中的電腦\] 對話方塊中，執行下列動作：
    
      - 指定第一個集區成員的電腦 FQDN，然後按一下 \[新增\] 。
    
      - 針對每部想要新增的電腦重複先前的步驟。完成時，按 \[下一步\] 。

7.  在 \[定義檔案共用\] 對話方塊中，執行下列其中一項動作：
    
      - 若要使用現有的檔案共用，請按一下 \[使用先前定義的檔案共用\] 並從清單中選取檔案共用，然後按 \[下一步\] 。
    
      - 若要建立新的檔案共用，請按一下 \[定義新的檔案共用\] 、在 \[檔案伺服器 FQDN\] 中輸入檔案共用之位置的 FQDN、在 \[檔案共用\] 中輸入共用的名稱，然後按 \[下一步\] 。
    
    > [!IMPORTANT]  
    > 於此步驟指定或建立的檔案共用必須已存在，或是在發行拓撲之前完成建立。<br />
    > 系統實際上不會使用指派給 Director 的檔案共用，因此您可以指派組織中任何集區的檔案共用。


8.  在 \[指定 Web 服務 URL\] 對話方塊的 \[外部基底 URL\] 中，指定 Director 的 FQDN，然後按一下 \[完成\] 。
    
    > [!IMPORTANT]  
    > 名稱必須可以從網際網路 DNS 伺服器解析，並指向反向 Proxy 的公用 IP 位址，反向 Proxy 會接聽傳送至該 URL 的 HTTP/HTTPS 要求，並將它們 Proxy 至該 Director 集區上的外部 Web 服務虛擬目錄。
    
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您有一個以上的 前端集區或 前端伺服器，則外部 Web 服務 FQDN 必須是唯一的。例如，如果您將 前端伺服器的外部 Web 服務 FQDN 定義為 <strong>pool01.contoso.com</strong>，便無法針對其他的 前端集區或 前端伺服器使用 <strong>pool01.contoso.com</strong>。如果您同時部署了 Director，則針對任何 Director 或 Director 集區定義的外部 Web 服務 FQDN，在任何其他 Director 或 Director 集區以及任何 前端集區或 前端伺服器中必須是唯一的。如果決定以自我定義的 FQDN 覆寫內部 Web 服務，各個 FQDN 必須與其他任何 前端集區、 Director 或 Director 集區各不相同。</td>
    </tr>
    </tbody>
    </table>


9.  發行拓撲。

