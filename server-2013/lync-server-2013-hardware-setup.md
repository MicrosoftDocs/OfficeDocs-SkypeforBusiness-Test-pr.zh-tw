---
title: Lync Server 2013：硬體設定
TOCTitle: 硬體設定
ms:assetid: 37a9f295-cde3-4beb-9a6a-2580082798ab
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425852(v=OCS.15)
ms:contentKeyID: 49290596
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的硬體設定

 

_**上次修改主題的時間：** 2013-02-21_

若要在基礎結構中設定部署拓撲時所需的硬體和其他元件，您必須在 拓撲產生器中發行拓撲之前，執行下列動作：

  - 為以 拓撲產生器 建立並儲存的拓撲設計中的每個元件安裝硬體，包括所有必要電腦 (執行 Lync Server 2013 的伺服器、資料庫伺服器、執行 Internet Information Services (IIS) 的伺服器，以及反向 Proxy 伺服器，視情況而定)、網路介面卡、硬體負載平衡器和儲存裝置 (例如檔案伺服器)。確認已遵照網路介面卡之數量及速度的建議。如果將使用硬體負載平衡器，請確認從廠商取得適當資訊，以設定用於 Lync Server 2013。如果將使用檔案伺服器或其他伺服器，以儲藏 Lync Server 必要的檔案共用，請確認伺服器可用並準備就緒用於檔案共用設定。如需如何定義拓撲以指定部署所需元件的詳細資訊，請參閱＜[在 Lync Server 2013 中定義和設定拓撲](lync-server-2013-defining-and-configuring-the-topology.md)＞。如需伺服器硬體需求的詳細資訊，請參閱支援文件中的＜[Lync Server 2013 的受支援硬體](lync-server-2013-supported-hardware.md)＞。

  - 確定網路基礎結構符合需求。如需詳細資訊，請參閱規劃文件中的＜[網路基礎結構需求](lync-server-2013-network-infrastructure-requirements.md)＞。

  - 設定 Active Directory 網域服務。設定 AD DS 的動作包括準備 AD DS 和定義所有您想在 AD DS 中部署的元件。如需準備 AD DS 的詳細資訊，請參閱部署文件中的＜ [為 Lync Server 2013 準備 Active Directory 網域服務](lync-server-2013-preparing-active-directory-domain-services.md)＞。

  - 設定建立檔案共用所需的權限。當您發行拓撲時，拓撲產生器 會自動設定 Lync Server 2013 對檔案共用的使用權限。但是，用來發行拓撲的使用者帳戶必須具有檔案共用的完整控制權 (讀取/寫入/修改)，拓撲產生器 才能設定必要的權限。為了確保拓撲產生器在發行期間能夠正確管理檔案共用，使用者或使用者所屬網域群組在檔案共用所在電腦上必須是本機 Administrators 群組的成員。在多網域的情況下，則網域 A 的使用者或群組在檔案共用所在網域 B 電腦上必須是本機 Administrators 群組的成員。
    
    如需有關在分散式檔案系統 (DFS) 中使用檔案共用來更新的詳細資訊，請參閱＜ [針對 Lync Server 2013 設定檔案儲存](lync-server-2013-configure-dfs-file-storage.md)＞。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server 2013 Enterprise Edition 的檔案共用不可位於 前端伺服器上。</td>
    </tr>
    </tbody>
    </table>


  - 安裝並設定 Web 服務的硬體負載平衡器。部署網域名稱系統 (DNS) 負載平衡之後，這些集區還是需要使用硬體負載平衡器，但只限 HTTP/HTTPS 流量。硬體負載平衡器用於連接埠 443 和 80 上來自用戶端的 HTTPS 流量。雖然這些集區仍然需要硬體負載平衡器，但其設定和管理主要是針對 HTTP/HTTPS 流量，這也是硬體負載平衡器的系統管理員比較熟悉的領域。

完成本主題所述的所有準備工作後，在發行拓撲前，您還需要：

  - [在伺服器上安裝 Lync Server 2013 的作業系統和必要軟體](lync-server-2013-install-operating-systems-and-prerequisite-software-on-servers.md)

  - [針對 Lync Server 2013 設定 IIS](lync-server-2013-configure-iis.md)

  - [為 Lync Server 2013 設定 SQL Server](lync-server-2013-configure-sql-server-for-lync-server.md)

  - [在 Lync Server 2013 中設定前端集區或 Standard Edition Server 的 DNS 記錄](lync-server-2013-configure-dns-records-for-a-front-end-pool-or-standard-edition-server.md)

