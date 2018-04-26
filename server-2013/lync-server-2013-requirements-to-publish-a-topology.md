---
title: Lync Server 2013：發行拓撲的需求
TOCTitle: 發行拓撲的需求
ms:assetid: 841cdf5d-d884-414d-ab50-3bb681b622ed
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg195733(v=OCS.15)
ms:contentKeyID: 49291520
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中發行拓撲的需求

 

_**上次修改主題的時間：** 2013-02-21_

本主題說明無論是使用 拓撲產生器 或 Lync Server 2013 管理命令介面 命令列介面，在發行拓撲時需要的特定基礎結構和軟體需求。這些需求除了適用一般作業系統、軟體和權限需求，也適用於所有的 Lync Server 2013 系統管理工具。發行拓撲之前，請確定您符合所有的系統管理工具需求。

  - 您必須在已加入相同網域或正在建立之 Lync Server 2013 部署樹系的電腦上執行 拓撲產生器，才能完成 Active Directory 網域服務 準備步驟，讓您在該電腦上使用系統管理工具，成功發行您的拓撲。

  - 除了 Edge Server 之外，定義在拓撲中的電腦必須加入網域和 AD DS。不過，當您發行拓撲時，電腦不需要在線上。

  - 必須建立集區共用的檔案，而且可供遠端使用者使用。

  - 為了發行 Enterprise Edition 前端集區，SQL Server 的後端伺服器必須在線上加入您部署伺服器的網域中，而且設定適當的防火牆規則，讓遠端使用者可以使用。如需指定防火牆例外的詳細資訊，請參閱＜ [瞭解與 Lync Server 2013 搭配使用時之 SQL Server 的防火牆需求](lync-server-2013-understanding-firewall-requirements-for-sql-server.md)＞。如需其他有關設定 SQL Server 的詳細資訊，請參閱＜ [為 Lync Server 2013 設定 SQL Server](lync-server-2013-configure-sql-server-for-lync-server.md)＞。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Standard Edition 伺服器 有一個組合的資料庫，會接受發行的組態。您必須先在 Lync Server 部署精靈 中執行 [準備第一個 Standard Edition Server] 設定工作。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 工作

[在 Lync Server 2013 中發行拓撲](lync-server-2013-publish-the-topology.md)  
[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)  

#### 概念

[Lync Server 2013 中的系統管理工具軟體需求](lync-server-2013-administrative-tools-software-requirements.md)  
[Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)  

#### 其他資源

[設定和管理 Lync Server 2013 所需的系統管理員權限](lync-server-2013-administrator-rights-and-permissions-required-for-setup-and-administration.md)

