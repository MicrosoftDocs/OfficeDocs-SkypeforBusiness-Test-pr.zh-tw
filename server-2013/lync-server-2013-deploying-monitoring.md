---
title: 在 Lync Server 2013 中部署監控
TOCTitle: 在 Lync Server 2013 中部署監控
ms:assetid: 117f4a3e-0670-4388-a553-b9854921145f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398199(v=OCS.15)
ms:contentKeyID: 49290129
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中部署監控

 

_**上次修改主題的時間：** 2013-12-17_

Microsoft Lync Server 2013 監視基礎結構有了重大變革，首先就是棄用了監控伺服器角色。監視服務現在已組合在各前端伺服器上，不再是個別的監控伺服器角色 (通常需要組織設定專用電腦來作為監控伺服器)。此變更的優點之一，就是有助於：

  - 減少實作 Lync Server 2013 時所需的伺服器角色數量。在此情況下，減少監控伺服器的伺服器角色也有助於減少成本，因為不需要維護用來監視的專用伺服器。

  - 降低 Lync Server 安裝及管理的複雜性。因為監視服務會自動組合在各前端伺服器上，所以您不再需要安裝、設定及管理監控伺服器角色。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 2013 中也棄用了封存伺服器角色。就像監視服務一樣，Lync Server 2013 封存服務現在也是組合在各前端伺服器上。這很值得注意，因為監視和封存經常共用相同的 SQL Server 資料庫執行個體。</td>
</tr>
</tbody>
</table>


如您所預期，這些變更對於安裝及管理監視服務的方式有著重大影響。例如，由於監控伺服器角色已不存在，所以監控伺服器節點已從 Lync Server 拓撲產生器中移除；這也表示您不會再使用拓撲產生器的 \[新增監控伺服器精靈\] 來新增監控伺服器至拓撲 (該精靈已不存在)。反之，您通常會藉由完成下列兩個步驟，在拓撲中實作監視服務：

1.  在設定新 Lync Server 集區的同時，啟用監視 (在 Lync Server 2013 中，會依各集區的狀況啟用或停用監視)。請注意，您可以為集區啟用監視，而不需實際收集監視資料，本文件中的＜設定詳細通話記錄和經驗品質設定＞一節將說明此程序。

2.  將監控存放區 (也就是監控資料庫) 與新集區建立關聯。請注意，單一監控存放區可與多個集區建立關聯。依據安置在登錄器集區的使用者數目，這表示您不需要為每個集區設定個別的監控資料庫。單一監控存放區即可供多集區使用。

雖然在您建立新集區的同時啟用監視通常會比較容易，但也可能會建立停用監視的新集區。如果您這麼做，可以在稍後使用拓撲產生器來啟用服務：拓撲產生器有提供一種方法，可為集區啟用或停用監視，或是將集區與不同的監控存放區建立關聯。請記得，雖然已經沒有監控伺服器角色了，您還是需要建立一或多個監控存放區：用來儲存監視服務所收集之資料的後端資料庫。這些後端資料庫可以用 Microsoft SQL Server 2008 R2 或 Microsoft SQL Server 2012 來建立。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果已為集區啟用監視，您可以停用收集監視資料的程序，而不需變更拓撲：Lync Server 管理命令介面有提供一種方法，可讓您停用 (之後再重新啟用) 詳細通話記錄 (CDR) 和經驗品質 (QoE) 資料收集。如需詳細資訊，請參閱本文件中的＜設定詳細通話記錄和經驗品質設定＞一節。</td>
</tr>
</tbody>
</table>


針對 Lync Server 2013 中的監視作業，另一項重要的增強功能就是 Lync Server 監視報告現在可支援 IPv6：使用 \[IP 位址\] 欄位的報告將會依據下列條件顯示 IPv4 或 IPv6 位址：1) 所使用的 SQL 查詢；以及 2) IPv6 位址是否儲存在監控資料庫中。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>確保 SQL Server Agent 服務的 [啟動類型] 為 [自動]，而且 SQL Server Agent 服務是針對存放監控資料庫的 SQL 執行個體執行，以便預設監控 SQL Server 維護工作可以在 SQL Server Agent 服務的控制下依其排程執行。</td>
</tr>
</tbody>
</table>


本文件將帶領您完成為 Lync Server 2013 安裝及設定監視作業和監視報告的程序。文件中提供逐步指示，將可協助您：

  - 在拓撲中啟用監視，以及將監控存放區與前端集區建立關聯。

  - 安裝 SQL Server Reporting Services 及 Lync Server 監視報告。監視報告是預先設定的報告，針對儲存在監控資料庫中資訊提供不同的觀點。

  - 設定詳細通話記錄 (CDR) 和經驗品質 (QoE) 資料收集。詳細通話記錄讓您能夠追蹤 Lync Server 功能的使用狀況，這些功能包括 Voice over IP (VoIP) 通話、立即訊息、檔案傳輸、音訊/視訊 (A/V) 會議，以及應用程式分享工作階段。QoE 計量追蹤在組織中建立的音訊和視訊通話品質，包括遺失的網路封包數量、背景雜訊和「抖動」(封包延遲差異) 量。

  - 從監控資料庫手動清除 CDR 及/或 QoE 記錄。

