---
title: Lync Server 2013：設定系統平台
TOCTitle: 設定系統平台
ms:assetid: 2e72e49d-2737-4b5b-8c0a-60f6ecb15bf1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204783(v=OCS.15)
ms:contentKeyID: 49290465
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定系統平台

 

_**上次修改主題的時間：** 2013-02-21_

開始部署 常設聊天室伺服器 之前，您必須先在伺服器上為符合系統需求的硬體安裝所需作業系統：

如需執行 Lync Server 2013 之伺服器、資料庫伺服器及檔案伺服器所支援之硬體的詳細資訊，請參閱支援文件中的＜ [Lync Server 2013 的受支援硬體](lync-server-2013-supported-hardware.md)＞。如需支援之作業系統和資料庫軟體的詳細資訊，請參閱支援文件中的＜ [Lync Server 2013 中的伺服器軟體和基礎結構支援](lync-server-2013-server-software-and-infrastructure-support.md)＞。如需 Windows 更新需求的詳細資訊，請參閱支援文件中的＜ [Lync Server 2013 中的其他伺服器支援和需求](lync-server-2013-additional-server-support-and-requirements.md)＞。

常設聊天室伺服器前端伺服器、 **PersistentChatService** 均可部署在 Lync Server 2013Enterprise Edition 集區中的一或多台獨立電腦上。但不可和 Lync ServerEnterprise Edition前端伺服器搭配。如同其他 Lync Server 角色， 常設聊天室伺服器 可以透過啟動載入器加以部署。 **檔案上傳/下載的 常設聊天室 Web 服務**以及 **聊天室管理的 常設聊天室 Web 服務**均為部署在 Lync Server 2013前端伺服器的 Web 元件。

單一 常設聊天室伺服器前端伺服器可支援 20,000 位作用中使用者。您可讓 Persistent Chat Server 集區最多有 4 個支援總共同時 80,000 位使用者的作用中前端。 常設聊天室後端伺服器、 **PersistentChatStore** 會儲存聊天室及類別。雖然相同的 SQL Server 執行個體上支援 Lync Server 2013後端伺服器及 **PersistentChatStore** 組合，但仍建議您將 **PersistentChatStore** 安裝在 Enterprise Edition 集區中專屬的 SQL Server後端伺服器。

若您的組織需要規範支援，您可使用 拓撲產生器來加以安裝。 常設聊天室伺服器 規範服務會與 常設聊天室伺服器前端伺服器安裝在相同的電腦上。規範需使用另一個資料庫。如需 常設聊天室伺服器 規範需求的詳細資訊，請參閱規劃文件中的＜ [在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md)＞。

每個拓撲至少需要一部安裝了 Lync Server 2013 的伺服器，以及一部安裝了 SQL Server 資料庫軟體的伺服器。 拓撲產生器支援多個 Persistent Chat Server 集區。遵循部署文件中的＜ [部署 Lync Server 2013](lync-server-2013-deploying-lync-server.md)＞，您對所有集區使用的部署指示來部署多個 Persistent Chat Server 集區。

您也可以使用 Lync Server 2013Standard Edition 部署 常設聊天室伺服器 。若如此，則會在 Standard Edition 伺服器 上搭配 **PersistentChatService**前端伺服器，然後您可在本機 SQL Server Express 執行個體上部署 **PersistentChatStore**後端伺服器。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不支援高可用性的 常設聊天室伺服器Standard Edition。效能及規模均會受到限制。此外，也僅支援 常設聊天室伺服器  Standard Edition 伺服器 部署的升級。但不支援將 Lync Server 2010群組聊天伺服器升級至 Lync Server 2013常設聊天室伺服器Standard Edition。</td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[Lync Server 2013 中的其他伺服器支援和需求](lync-server-2013-additional-server-support-and-requirements.md)  

#### 其他資源

[Lync Server 2013 的受支援硬體](lync-server-2013-supported-hardware.md)  
[Lync Server 2013 中的伺服器軟體和基礎結構支援](lync-server-2013-server-software-and-infrastructure-support.md)  
[在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md)  
[部署 Lync Server 2013](lync-server-2013-deploying-lync-server.md)

