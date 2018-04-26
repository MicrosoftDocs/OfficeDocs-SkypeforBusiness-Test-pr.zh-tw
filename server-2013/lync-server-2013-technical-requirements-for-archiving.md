---
title: Lync Server 2013：封存的技術需求
TOCTitle: 封存的技術需求
ms:assetid: 896d60e2-be4b-462d-8357-4cd307ab7304
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205059(v=OCS.15)
ms:contentKeyID: 49291582
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中封存的技術需求

 

_**上次修改主題的時間：** 2012-10-09_

Lync Server 2013 技術需求如下：

  - 基礎結構需求。

  - 必須針對封存安裝必備軟體。

  - 封存的資料儲存需求。

  - 封存部署的延展性需求與考量。

  - 封存資料庫的效能需求與考量。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這個 Lync Server 2013 版本不提供延展性與效能資訊。</td>
</tr>
</tbody>
</table>


## 基礎結構需求

Lync Server 2013 封存基礎結構需求與 Lync Server 2013 部署的需求相同。如需詳細資訊，請參閱規劃文件中的 [判斷 Lync Server 2013 的基礎結構需求](lync-server-2013-determining-your-infrastructure-requirements.md)。

## 封存先決條件

Lync Server 2013 簡化封存的先決條件，原因如下：

  - Archiving Server 不再是伺服器角色。整合資料收集代理程式在集區中的前端伺服器和 Standard Edition Server 上執行，以擷取封存所用的資料，因此您不需要設定個別的系統平台進行封存。

  - 封存使用 Lync Server 2013 檔案儲存來暫時儲存會議內容檔案，因此您不需要設定個別的檔案儲存進行封存。

  - 在 Lync Server 2013 中，不需要訊息佇列。

## 封存的資料儲存需求

此外，您需要設定封存儲存的基礎結構。這包括下列其中一或兩項作業：

  - **Microsoft Exchange 儲存**。會議內容檔案 (例如 PowerPoint 簡報) 封存成為附件。如果您要使用 Microsoft Exchange 整合，以便 Lync 封存資料一併與 Exchange 規範資料儲存，您必須將 Exchange 2013 用於 Exchange 部署，並確保儲存大小上限支援會議內容檔案的儲存。如果使用 Microsoft Exchange 整合選項部署封存， Lync 封存資料只會對於隸屬於 Exchange 2013 伺服器的使用者一併與 Exchange 2013 規範資料儲存。您必須先部署 Exchange 2013，然後使用 Microsoft Exchange 整合選項部署並啟用封存。如果您選擇使用 Exchange 2013 儲存，除非您有並非隸屬於 Exchange 2013 伺服器的 Lync 使用者，否則不需要部署個別 SQL Server 資料庫用於封存。

  - **封存的 SQL Server 資料庫儲存**。若要支援不隸屬於 Exchange 2013 伺服器的使用者，或者您不要使用 Microsoft Exchange 整合選項，您必須使用 SQL Server 資料庫部署封存儲存。 Lync Server 2013 支援下列 64 位元版本的 SQL Server：
    
      - Microsoft SQL Server 2008 R2 Enterprise
    
      - Microsoft SQL Server 2008 R2 Standard
    
      - Microsoft SQL Server 2012 Enterprise
    
      - Microsoft SQL Server 2012 Standard
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>不支援 Microsoft SQL Server 2008 R2 Express 及 Microsoft SQL Server 2012 Express 進行封存。不支援 32 位元版本的 SQL Server。如需其他的 SQL Server 需求及限制，請參閱規劃文件或支援文件中的＜ <a href="lync-server-2013-database-software-support.md">Lync Server 2013 中的資料庫軟體支援</a>＞。</td>
    </tr>
    </tbody>
    </table>
    
    您必須先設定 SQL Server 平台才能部署和啟用封存功能。如果用來發佈拓撲的帳戶擁有適當的系統管理員權限，您可以在發佈拓撲時建立封存資料庫 (LcsLog)。您也可以稍後建立資料庫，這是安裝程序的一部分。如需 SQL Server 的詳細資訊，請參閱 SQL Server TechCenter，網址為： [http://go.microsoft.com/fwlink/?linkid=129045\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=129045%26clcid=0x404)。

