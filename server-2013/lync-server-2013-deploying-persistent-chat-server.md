---
title: Lync Server 2013：部署常設聊天室伺服器
TOCTitle: 部署常設聊天室伺服器
ms:assetid: e3b930fb-6855-47f0-b6b3-7dfae386540d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205357(v=OCS.15)
ms:contentKeyID: 49292606
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中部署常設聊天室伺服器

 

_**上次修改主題的時間：** 2014-03-31_

Lync Server 2013、 常設聊天室伺服器 是 Lync Server 2013 基礎結構的部分。

部署 常設聊天室伺服器，您必須要執行下列工作：

  - 使用 拓撲產生器 來定義、匯入並發佈您要部署的拓撲與元件。

  - 部署 常設聊天室伺服器 元件前的環境準備。

  - 安裝並設定部署的 常設聊天室伺服器 元件。

常設聊天室伺服器 與 Lync Server 2013Enterprise Edition 都可當作獨立集區使用 (未與 Enterprise Edition前端伺服器 共置)。 常設聊天室伺服器 需要 Enterprise Edition 集區中的 SQL Server後端伺服器 來存放聊天室內容及其他相關中繼資料。雖然系統支援在同一個 SQL Server 執行個體上收集 Lync Server 2013後端伺服器 與 **PersistentChatStore**，但還是建議您在專屬的 SQL Server後端伺服器 上安裝 **PersistentChatStore**。

常設聊天室伺服器 也可與 Lync Server 2013Standard Edition 一起部署。在這個條件下， **PersistentChatService**前端伺服器 是共置於 Standard Edition 電腦上，且 **PersistentChatStore**後端伺服器 可以部署到本機 SQL Server Express 執行個體。

若需受支援並存設定的詳細資料，請參閱 [Lync Server 2013 中支援的伺服器組合](lync-server-2013-supported-server-collocation.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們不支援 常設聊天室伺服器Standard Edition 的高可用性。效能與比例將受到限制。此外，我們只支援新 常設聊天室伺服器Standard Edition 伺服器。我們不支援從 Lync Server 2010, 群組聊天伺服器 升級到 Lync Server 2013常設聊天室伺服器Standard Edition。</td>
</tr>
</tbody>
</table>


若貴公司需要規範支援，您可以在 常設聊天室伺服器前端伺服器 安裝 常設聊天室伺服器 規範服務。必須要有個別資料庫才能使用規範。

最低標準是，每個拓撲要有安裝了 Lync Server 2013 的伺服器，以及安裝了 SQL Server 資料庫軟體的伺服器。

使用 拓撲產生器 將 常設聊天室伺服器 新增到 Lync Server 2013 部署。您可以使用 拓撲產生器選擇新增一個以上的 Persistent Chat Server 集區。請依照同一份部署指示，部署多個 Persistent Chat Server 集區，就像為其他集區部署一樣。如需詳細資訊，請參閱部署文件中的 [部署 Lync Server 2013](lync-server-2013-deploying-lync-server.md)。

如需詳細了解可用拓撲及安裝 常設聊天室伺服器 的技術與軟體需求，請參閱規劃文件中的 [在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md)、規劃文件/部署文件或操作文件中的 [Lync Server 2013 中的常設聊天室伺服器運作方式](lync-server-2013-how-persistent-chat-server-works.md)，以及支援能力文件中的 [Lync Server 2013 的受支援硬體](lync-server-2013-supported-hardware.md)。

如需了解取得憑證、建立 SQL Server 資料庫與建立檔案存放區的詳細資訊，請參閱部署文件中的 [部署 Lync Server 2013](lync-server-2013-deploying-lync-server.md)。

一個 常設聊天室伺服器前端伺服器 可支援 20,000 個現用使用者。您擁有的 Persistent Chat Server 集區 可支援多達 4 個作用中的 前端伺服器，共 80,000 個使用者可同時使用。

常設聊天室伺服器在虛擬伺服器中也受支援。若虛擬伺服器符合實體伺服器的規格，則可讓多達 20,000 個使用者同時使用。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>常設聊天室伺服器 必須安裝在 NTFS 檔案系統上，以強制檔案系統安全性。 常設聊天室伺服器 不支援 FAT32 檔案系統。</td>
</tr>
</tbody>
</table>


## 本節內容

  - [Lync Server 2013 中的常設聊天室伺服器運作方式](lync-server-2013-how-persistent-chat-server-works.md)

  - [Lync Server 2013 中的常設聊天室伺服器的部署檢查清單](lync-server-2013-deployment-checklist-for-persistent-chat-server.md)

  - [Lync Server 2013 中常設聊天室伺服器的技術需求](lync-server-2013-technical-requirements-for-persistent-chat-server.md)

  - [在 Lync Server 2013 中設定常設聊天室伺服器的系統與基礎結構](lync-server-2013-setting-up-systems-and-infrastructure-for-persistent-chat-server.md)

  - [在 Lync Server 2013 中將常設聊天室伺服器新增至您的部署](lync-server-2013-adding-persistent-chat-server-to-your-deployment.md)

  - [在 Lync Server 2013 中安裝常設聊天室伺服器](lync-server-2013-installing-persistent-chat-server.md)

  - [在 Lync Server 2013 中新增常設聊天室管理員](lync-server-2013-adding-a-persistent-chat-administrator.md)

  - [在 Lync Server 2013 中設定常設聊天室伺服器](lync-server-2013-configuring-persistent-chat-server.md)

  - [使用 Windows PowerShell Cmdlet 設定常設聊天室伺服器](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md)

  - [在 Lync Server 2013 中使用 Windows PowerShell Cmdlet 疑難排解常設聊天室伺服器設定](lync-server-2013-troubleshooting-persistent-chat-server-configuration-using-windows-powershell-cmdlets.md)

  - [在 Lync Server 2013 中針對高可用性和災害復原設定常設聊天室伺服器](lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md)

  - [Lync Server 2013 中的容錯移轉和容錯回復常設聊天室伺服器](lync-server-2013-failing-over-and-failing-back-persistent-chat-server.md)

