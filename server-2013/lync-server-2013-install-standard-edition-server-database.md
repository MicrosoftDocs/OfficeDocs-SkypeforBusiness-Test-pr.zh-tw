---
title: Lync Server 2013：安裝 Standard Edition Server 資料庫
TOCTitle: 安裝 Standard Edition Server 資料庫
ms:assetid: 0bd3a804-aad6-48cb-981b-54725af032db
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398167(v=OCS.15)
ms:contentKeyID: 49290056
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝 Lync Server 2013 的 Standard Edition Server 資料庫

 

_**上次修改主題的時間：** 2012-10-01_

將 Standard Edition 伺服器 設定為基礎結構中的唯一伺服器，伺服器主控的使用者與其他伺服器的安裝作業不同，在 \[部署精靈\] 中有一個特別為了用於設定初始伺服器的選取項目。

## 若要安裝 Standard Edition Server

1.  以本機系統管理員或網域管理員的身分登入您即將安裝 Standard Edition 伺服器 的伺服器。

2.  如果您尚未準備 Active Directory 網域服務，請先執行下列程序。如需詳細資訊，請參閱＜ [為 Lync Server 2013 準備 Active Directory 網域服務](lync-server-2013-preparing-active-directory-domain-services.md)＞。

3.  在 \[ Lync Server 部署精靈\] 中，按一下 \[準備第一個 Standard Edition Server\] 。

4.  在 **\[準備單一 Standard Edition Server\]** 頁面上，按 **\[下一步\]** 。

5.  在「執行命令」 頁面上，SQL Server 2012 Express 已安裝為 中央管理存放區。已建立所需的防火牆規則。在完成資料庫和必要軟體的安裝時，請按一下 \[完成\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果命令輸出摘要畫面沒有可見的更新，則初始安裝可能需要一些時間。這是由於安裝 SQL Server Express 的緣故。如果您需要監控資料庫的安裝，請使用 [工作管理員] 來監控安裝程式。</td>
    </tr>
    </tbody>
    </table>


6.  如果您先前尚未安裝系統管理工具，請在 Lync Server 部署精靈頁面上按一下 **\[安裝拓撲產生器\]** 。如需詳細資訊，請參閱＜ [安裝 Lync Server 2013 系統管理工具](lync-server-2013-install-lync-server-administrative-tools.md)＞。

7.  確認 \[準備 Active Directory\]、\[準備第一個 Standard Edition Server\] 和 \[安裝拓撲產生器\] 旁邊有綠色勾號。

