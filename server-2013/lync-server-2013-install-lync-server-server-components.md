---
title: Lync Server 2013：安裝 Lync Server 伺服器元件
TOCTitle: 安裝 Lync Server 伺服器元件
ms:assetid: 186aed6e-7adf-4a92-9f2e-f9a4de5ff202
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398239(v=OCS.15)
ms:contentKeyID: 49290225
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝 Lync Server 2013 的伺服器元件

 

_**上次修改主題的時間：** 2014-05-05_

執行下列步驟前，請確定先使用網域使用者帳戶登入伺服器，該帳戶必須兼具本機系統管理員身分，及 Active Directory 中 RTCUniversalReadOnlyAdmins 群組成員身分。

Lync Server 部署精靈 可用來安裝每個 Lync 伺服器角色以及啟動伺服器所需的元件。本文會帶領您完成在 Lync 基礎結構中部署 Standard Edition 伺服器 或 前端伺服器 的步驟。

## 安裝 Lync Server 元件

1.  如果目前未執行 Lync Server 部署精靈，請在要安裝 Lync 的伺服器上啟動它。

2.  按一下 \[安裝或更新 Lync Server 系統\] 。

3.  在 \[部署精靈\] 中，確認 \[步驟 1：安裝本機設定存放區\] 有出現綠色核取方塊，這代表此伺服器已完成安裝存放區的本機複本。如果未核取，您需要在伺服器上安裝本機設定存放區。請依照＜[在 Lync Server 2013 中安裝本機設定存放區](lync-server-2013-install-the-local-configuration-store.md)＞中的步驟執行，然後返回此處。

4.  準備好在伺服器上安裝 Lync Server 2013 元件時，請按一下 \[步驟 2：安裝或移除 Lync Server 元件\] 旁邊的 \[執行\]。

5.  在 \[安裝 Lync Server 元件\] 頁面上，按 \[下一步\] 以安裝如已發行拓撲中所定義的元件。

6.  \[執行命令\] 頁面會在執行安裝時顯示命令摘要以及安裝資訊。完成後，您可透過此清單選取欲檢視的記錄檔，然後按一下 \[檢視記錄檔\]。

7.  完成 Lync Server 2013 元件安裝，並已視需要檢閱記錄後，按一下 \[完成\] 來完成此安裝步驟。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果系統提示您重新啟動伺服器 (如果需要安裝 Windows Desktop Experience，可能會發生此狀況)，請照做。電腦重新啟動並運行後，您需要從上述的步驟 3 開始重複這些程序 (基本上在 [部署精靈] 中再次執行步驟 2)。</td>
    </tr>
    </tbody>
    </table>

