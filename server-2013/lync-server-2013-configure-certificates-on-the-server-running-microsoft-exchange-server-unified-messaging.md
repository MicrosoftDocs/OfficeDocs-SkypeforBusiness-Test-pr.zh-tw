---
title: 在執行 Microsoft Exchange Server Unified Messaging 的伺服器上設定憑證
TOCTitle: 在執行 Microsoft Exchange Server Unified Messaging 的伺服器上設定憑證
ms:assetid: 74c883b4-cef6-41a9-b2eb-7212be32fea4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398564(v=OCS.15)
ms:contentKeyID: 49291322
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在執行 Microsoft Exchange Server Unified Messaging 的伺服器上設定憑證

 

_**上次修改主題的時間：** 2012-09-26_

如果您已依照規劃文件中[在 Lync Server 2013 中規劃 Exchange Unified Messaging 整合](lync-server-2013-planning-for-exchange-unified-messaging-integration.md) 所述的程序部署了 Exchange 整合通訊 (UM)，而您想要為組織中的 Enterprise Voice 使用者提供 Exchange UM 功能，可使用下列程序，在執行 Exchange UM 的伺服器上設定憑證。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>針對內部憑證，執行 Lync Server 2013 的伺服器以及執行 Microsoft Exchange 的伺服器，都必須要有互相信任的信任根授權單位憑證。憑證授權單位 (CA) 可以是相同或不同的憑證授權單位，只要伺服器將憑證授權單位的根憑證登錄在其信任的根授權單位憑證存放區即可。</td>
</tr>
</tbody>
</table>


您必須使用伺服器憑證設定 Exchange Server，以便連線至 Lync Server 2013：

1.  下載 Exchange Server 的 CA 憑證。

2.  安裝 Exchange Server 的 CA 憑證。

3.  確認 CA 在 Exchange Server 的受信任的根 CA 清單中。

4.  建立 Exchange Server 的憑證要求並安裝憑證。

5.  指派 Exchange Server 的憑證。

## 若要下載 CA 憑證

1.  在執行 Exchange UM 的伺服器上，依序按一下 **\[開始\]** 和 **\[執行\]**，輸入 **http://\<您的發行 CA 伺服器名稱\>/certsrv**，然後按一下 **\[確定\]**。

2.  在 **\[選取工作\]** 下方，按一下 **\[下載 CA 憑證、憑證鏈結或 CRL\]**。

3.  在 **\[下載 CA 憑證、憑證鏈結或 CRL\]** 下，選取 **\[編碼方法為 Base 64\]**，然後按一下 **\[下載 CA 憑證\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您也可以在此步驟指定識別名編碼規則 (DER) 編碼。如果您選取 DER 編碼，此程序下一個步驟中以及<strong>「若要安裝 CA 憑證」</strong>步驟 10 中的檔案類型會是 .p7b，而非 .cer。</td>
    </tr>
    </tbody>
    </table>


4.  在 **\[檔案下載\]** 對話方塊中，按一下 **\[儲存\]**，然後將檔案儲存到伺服器的硬碟上 (視您在上一個步驟中選取的編碼而定，檔案的副檔名會是 .cer 或 .p7b)。

## 若要安裝 CA 憑證

1.  在執行 Exchange UM 的伺服器上，依序按一下 **\[開始\]** 和 **\[執行\]**，在 **\[開啟\]** 方塊中輸入 **mmc**，然後按一下 **\[確定\]**，以開啟 Microsoft Management Console (MMC)。

2.  在 **\[檔案\]** 功能表中，按一下 **\[新增/移除嵌入式管理單元\]**，然後按一下 **\[新增\]**。

3.  在 **\[新增獨立嵌入式管理單元\]** 方塊中，按一下 **\[憑證\]**，然後按一下 **\[新增\]**。

4.  在 **\[憑證嵌入式管理單元\]** 對話方塊中，按一下 **\[電腦帳戶\]**，然後按 **\[下一步\]**。

5.  在 **\[選擇電腦\]** 對話方塊中，確定 **\[本機電腦: (執行這個主控台的電腦)\]** 核取方塊已經選取，然後按一下 **\[完成\]**。

6.  按一下 **\[關閉\]**，然後按一下 **\[確定\]**。

7.  在主控台樹狀目錄中，依序展開 **\[憑證 (本機電腦)\]** 和 **\[信任的根憑證授權\]**，然後按一下 **\[憑證\]**。

8.  以滑鼠右鍵按一下 **\[憑證\]**，按一下 **\[所有工作\]**，再按一下 **\[匯入\]**。

9.  按 **\[下一步\]**。

10. 按一下 **\[瀏覽\]**，找出檔案，然後按 **\[下一步\]** (視您在**「若要下載 CA 憑證」**步驟 3 中選取的編碼而定，檔案的副檔名會是 .cer 或 .p7b)。

11. 按一下 **\[將所有憑證放入以下的存放區\]**。

12. 按一下 **\[瀏覽\]**，然後選取 **\[受信任的根憑證授權單位\]**。

13. 按 **\[下一步\]** 以驗證設定，然後按一下 **\[完成\]**。

## 若要確認 CA 是否在受信任的根 CA 清單中

1.  在執行 Exchange UM 的伺服器上，於 MMC 中依序展開 **\[憑證 (本機電腦)\]** 和 **\[受信任的根憑證授權單位\]**，然後按一下 **\[憑證\]**。

2.  在詳細資料窗格中，確認您的 CA 位於受信任的 CA 清單上。

## 使用 Lync Server 設定 Exchange Server 2013 UM

1.  如需詳細資訊，請參閱 [http://go.microsoft.com/fwlink/?linkid=265372\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=265372%26clcid=0x404)＜Exchange Server＞文件中的＜使用 Lync Server 整合 Exchange Server 2013 UM＞。

## 若要在 Exchange Server 2007 (SP1) 上建立憑證要求及安裝憑證

1.  在執行 Exchange UM 的伺服器上，依序按一下 **\[開始\]** 和 **\[執行\]**，輸入 **http://\<***您的發行 CA 伺服器名稱***\>/certsrv**，然後按一下 **\[確定\]**。

2.  在 **\[選取工作\]** 下，按一下 **\[要求憑證\]**。

3.  在 **\[要求憑證\]** 下，按一下 **\[進階憑證要求\]**。

4.  在 **\[進階憑證要求\]** 下，按一下 **\[建立並送出要求至此 CA\]**。

5.  在 **\[進階憑證要求\]** 下，選取 **\[Web 伺服器\]** 或針對伺服器驗證設定的另一個伺服器憑證範本。

6.  在 **\[離線範本識別資訊\]** 下的 **\[名稱\]** 方塊中，輸入 Exchange Server 的完整網域名稱 (FQDN)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您必須輸入 Exchange Server 的 FQDN，才能夠進行通訊。</td>
    </tr>
    </tbody>
    </table>


7.  在 **\[金鑰選項\]** 下，按一下 **\[將憑證存放在本機電腦憑證存放區\]** 核取方塊。

8.  按一下網頁下方的 **\[送出\]** 按鈕。

9.  在開啟並要求確認的對話方塊中，按一下 **\[是\]**。

10. 在 \[已發出憑證\] 頁面的 **\[已發出憑證\]** 下，按一下 **\[安裝這個憑證\]**。

11. 在開啟並要求確認的對話方塊中，按一下 **\[是\]**。

12. 確認顯示「您的新憑證已經安裝成功」訊息。

## 若要在 Exchange Server 2010 上建立憑證

1.  以適當的使用者權限登入執行 Exchange UM 的伺服器。如需詳細資訊，請參閱＜用戶端存取權限＞，網址為 [http://go.microsoft.com/fwlink/?linkid=195499\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=195499%26clcid=0x404)。

2.  參閱下列程序以建立憑證：
    
    1.  ＜建立新的 Exchange 憑證＞，網址為 [http://go.microsoft.com/fwlink/?linkid=195494\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=195494%26clcid=0x404)
    
    2.  ＜匯入 Exchange 憑證＞，網址為 [http://go.microsoft.com/fwlink/?linkid=195496\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=195496%26clcid=0x404)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>對於憑證的 <strong>[主體名稱]</strong>，您必須輸入 Exchange Server 的 FQDN，才能夠進行通訊。</td>
    </tr>
    </tbody>
    </table>


## 若要在 Exchange Server 2007 (SP1) 上指派憑證

1.  在執行 Exchange UM 的伺服器上開啟 MMC。

2.  在主控台樹狀目錄中，展開 **\[個人\]**，然後按一下 **\[憑證\]**。

3.  在詳細資料窗格中，確認有顯示個人憑證。

4.  按兩下憑證以閱讀憑證的詳細資料，並且確認憑證有效。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>可能需要幾分鐘，才會顯示憑證是有效的。</td>
    </tr>
    </tbody>
    </table>


5.  重新啟動 Microsoft Exchange Unified Messaging 服務。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>執行 Exchange Server 2007 SP1 Unified Messaging 的伺服器會自動擷取正確的憑證。</td>
    </tr>
    </tbody>
    </table>


6.  開啟 \[事件檢視器\] 並尋找事件識別碼 1112，此事件識別碼會指定執行 Exchange Server 2007 SP1 Unified Messaging 之伺服器所擷取的憑證。

## 若要在 Exchange Server 2010 上指派憑證

1.  以適當的使用者權限登入執行 Exchange UM 的伺服器。如需詳細資訊，請參閱＜用戶端存取權限＞，網址為 [http://go.microsoft.com/fwlink/?linkid=195499\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=195499%26clcid=0x404)。

2.  如需指派憑證的程序，請參閱＜將服務指派給憑證＞，網址為 [http://go.microsoft.com/fwlink/?linkid=195497\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=195497%26clcid=0x404)。

