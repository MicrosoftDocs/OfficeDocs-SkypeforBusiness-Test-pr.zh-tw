---
title: Lync Server 2013：設定外部 Edge 介面的憑證
TOCTitle: 設定外部 Edge 介面的憑證
ms:assetid: 5d78182c-88d8-4483-95ad-74b17f2d5fac
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398409(v=OCS.15)
ms:contentKeyID: 49291054
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 設定外部 Edge 介面的憑證

 

_**上次修改主題的時間：** 2012-09-08_

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您執行 [憑證精靈] 時，請確定您用來登入的帳戶，是具有您要使用之憑證範本類型適當權限的群組成員。根據預設， Lync Server 憑證要求會使用 Web 伺服器憑證範本。如果您要以 RTCUniversalServerAdmins 群組成員的帳戶使用此範本來要求憑證，請確定群組具有使用該範本所需的註冊權限。</td>
</tr>
</tbody>
</table>


每一台 Edge Server 都需要在周邊網路與網際網路之間的介面上放置一個公用憑證，而該憑證的主體替代名稱必須包含 Access Edge Service 的外部名稱與 Web Conferencing Edge Service 完整網域名稱 (FQDN)。

如需有關此憑證與其他憑證需求的詳細資訊，請參閱＜ [Lync Server 2013 中的外部使用者存取的憑證需求](lync-server-2013-certificate-requirements-for-external-user-access.md)＞。

如需負責提供符合整合通訊憑證之特定需求，且與 Microsoft 合作以確保可搭配 \[ Lync Server 2013 憑證精靈\] 一起使用的公用憑證授權單位 (CA) 清單，請參閱 Microsoft 知識庫文件 929395＜Exchange Server 和 Communications Server 的整合通訊憑證合作夥伴＞，網址為 <http://go.microsoft.com/fwlink/?linkid=202834>。

## 設定外部介面的憑證

若要在網站上設定外部 Edge 介面的憑證，請使用本節所述步驟執行下列事項：

  - 為 Edge Server 的外部介面建立憑證要求。

  - 將要求送出給公用 CA。

  - 匯入每一部 Edge Server 外部介面的憑證。

  - 指派每一部 Edge Server 外部介面的憑證。

  - 如果您的部署範圍包括好幾部 Edge Server，請將憑證連同其私密金鑰一起匯出，然後將其複製到其他 Edge Server 上。接著，將其匯入到每一台 Edge Server 並如先前所述加以指定。在每一部 Edge Server 上重複這個程序。

您可以從公用憑證授權單位 (CA) 直接要求公用憑證，例如從公用 CA 網站。本節所述步驟使用的憑證精靈適用於大多數憑證工作。如果您選擇從公用 CA 直接要求憑證，則您需要適當修改每個步驟以要求、傳輸與匯入憑證，同時匯入憑證鏈結。

當您從外部 CA 要求憑證時，附上的認證必須具備從該 CA 要求憑證的權限。每一家 CA 的安全性原則都會定義可以用來要求、發行、管理或讀取憑證的認證 (亦即，特定使用者與群組名稱)。

如果您決定透過 Certificates Microsoft Management Console (MMC) 匯入憑證鏈結與憑證，則您必須將其匯入電腦的憑證存放庫。如果您將其匯入使用者或服務憑證存放區，您將無法在 Lync Server 2013 憑證精靈中使用該憑證進行指派。

## 若要為 Edge Server 的外部介面建立憑證要求

1.  在 Edge Server 的 \[部署精靈\] 中，按一下 \[步驟 3: 要求、安裝或指派憑證\] 旁邊的 \[再執行一次\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您的組織想要支援與 AOL 的公用立即訊息 (IM) 連線能力，則您無法使用 Lync Server 部署精靈要求憑證。這時請執行本主題稍後「若要為 Edge Server 的外部介面建立憑證要求以支援對 AOL 的公用 IM 連線能力」中的步驟。<br />
    如果您在集區中的單一位置有多部 Edge Server，則可以在任何一部 Edge Server 上執行「 Lync Server 2013 憑證精靈」。</td>
    </tr>
    </tbody>
    </table>


2.  在 \[可用憑證工作\] 頁面上，按一下 \[建立新憑證要求\] 。

3.  在 \[憑證要求\] 頁面上，按一下 \[外部邊緣憑證\] 。

4.  在 \[延遲或立即要求\] 頁面上，選取 \[立即準備此要求，但稍後再傳送\] 核取方塊。

5.  在 \[憑證要求檔案\] 頁面上，輸入用來儲存此要求的檔案完整路徑和名稱 (例如，c:\\cert\_exernal\_edge.cer)。

6.  若要使用預設 WebServer 範本之外的其他範本，在 \[指定其他憑證範本\] 頁面上，選取 \[針對選取的憑證授權單位使用其他憑證範本\] 核取方塊。

7.  在 \[名稱和安全性設定\] 頁面上，執行下列動作：
    
      - 在 \[易記名稱\] 中，輸入憑證的顯示名稱。
    
      - 在 **\[位元長度\]** 中，指定位元長度 (預設值通常是 **2048** )。
    
      - 確認已選取 \[將憑證私密金鑰標示為可匯出\] 核取方塊。

8.  在 \[組織資訊\] 頁面上，輸入組織的名稱和組織單位 (例如部門)。

9.  在 \[地理資訊\] 頁面上，指定位置資訊。

10. 在 \[主體名稱/主體別名\] 頁面上，會顯示精靈將自動填入的資訊。如果您還需要其他主體別名，請在後續兩個步驟中指定。

11. 在 \[主體替代名稱 (SAN) 上的 SIP 網域設定\] 頁面上，選取網域核取方塊，將 sip.*\<sipdomain\>* 項目新增至主體替代名稱清單中。

12. 在 \[設定其他主體別名\] 頁面上，指定任何需要的其他主體別名。

13. 在 \[要求摘要\] 頁面上，檢閱要用來產生要求的憑證資訊。

14. 當命令執行完畢之後，執行下列步驟：
    
      - 若要檢視憑證要求記錄檔，按一下 **\[檢視記錄檔\]** 。
    
      - 若要完成憑證要求，按 **\[下一步\]** 。

15. 在 **\[憑證要求檔案\]** 頁面上，執行下列步驟：
    
      - 若要檢視產生的憑證簽署要求 (CSR) 檔案，按一下 **\[檢視\]** 。
    
      - 按一下 **\[完成\]** ，關閉精靈。

16. 將輸出檔案複製到某個位置，您可以從這個位置將它送出到公用 CA。

## 若要為 Edge Server 的外部介面建立憑證要求以支援對 AOL 的公用 IM 連線能力

1.  若有必要的範本可提供給 CA，請在 Edge Server 中使用下列 Windows PowerShell Cmdlet 以要求憑證：
    
        Request-CsCertificate -New -Type AccessEdgeExternal  -Output C:\ <certfilename.txt or certfilename.csr>  -ClientEku $true -Template <template name>
    
    Lync Server 2013 中所提供的預設範本憑證名稱為 Web Server。如果您需要使用不同於預設範本的其他範本，請僅指定 *\<template name\>*。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您的組織想要對 AOL 支援公用 IM 連線能力，您必須使用 Windows PowerShell (而非憑證精靈) 以要求要指定給 Access Edge Service 之外部邊緣的憑證。這是因為憑證精靈用來要求憑證的 Lync Server 2013 Web 伺服器範本不支援用戶端 EKU 組態。在您使用 Windows PowerShell 建立憑證之前，CA 管理員必須建立並部署支援用戶端 EKU 的新範本。</td>
    </tr>
    </tbody>
    </table>


## 若要將要求送出到公用憑證授權單位

1.  開啟輸出檔案。

2.  複製並貼上憑證簽署要求 (CSR) 的內容。

3.  如果出現提示，請指定下列選項：
    
      - 伺服器平台為 **\[Microsoft\]** 。
    
      - 版本為 **\[IIS\]** 。
    
      - 使用類型為 **\[Web 伺服器\]** 。
    
      - 回應格式為 **PKCS7** 。

4.  在公用 CA 驗證您的資訊之後，您會收到一封電子郵件，其中包含憑證所需的文字。

5.  複製此電子郵件的文字，並將內容儲存到本機電腦的文字檔 (.txt) 中。

## 若要匯入 Edge Server 外部介面的憑證

1.  以 Administrators 群組成員身分登入方才用來建立憑證要求的同一部 Edge Server。

2.  在 \[部署精靈\] 的 **\[部署 Edge Server\]** 頁面上，按一下 **\[步驟 3：要求、安裝或指派憑證\]** 旁邊的 **\[再執行一次\]** 。

3.  在 **\[可用憑證工作\]** 頁面上，按一下 **\[從 .p7b、pfx 或 .cer 檔案匯入憑證\]** 。

4.  在 \[匯入憑證\] 頁面上，按一下 \[瀏覽\] 來尋找並選取您為 Edge Server 外部介面要求的憑證 (或者，您可以輸入完整路徑和檔案名稱)。如果憑證包含私密金鑰，請選取 \[憑證檔案包含憑證的私密金鑰\] ，然後輸入私密金鑰的密碼。按 \[下一步\] 。

5.  在 \[匯入憑證摘要\] 頁面中，檢閱摘要，然後按 \[下一步\] 。

6.  在 \[執行命令\] 中，檢閱匯入結果，視需要按一下 \[檢視記錄檔\] 以取得更多資訊，然後按一下 \[完成\] ，完成憑證的匯入。

7.  如果您正在設定 Edge Server 集區，請按照本主題後面的「為集區中的 Edge Server 匯出包含私密金鑰的憑證」程序，匯出憑證及其私密金鑰。請將匯出的憑證檔案複製到其他 Edge Server，然後將之匯出至每一部 Edge Server 上的電腦存放區。

## 為集區中的 Edge Server 匯出包含私密金鑰的憑證

1.  以 Administrators 群組成員身分登入剛才用來匯入憑證的同一部 Edge Server。

2.  依序按一下 \[開始\] 、\[執行\] ，然後輸入 **MMC** 。

3.  在 Microsoft Management Console (MMC) 主控台，按一下 \[檔案\] ，然後按一下 \[新增/移除嵌入式管理單元\] 。

4.  在 \[新增或移除嵌入式管理單元\] 中，按一下 \[憑證\] ，然後按一下 \[新增\] 。

5.  在 \[憑證\] 對話方塊中，選取 \[電腦帳戶\] ，按 \[下一步\] ，在 \[選取電腦\] 中選取 \[本機電腦: (執行這個主控台的電腦)\] ，按一下 \[完成\] ，然後按一下 \[確定\] ，完成 MMC 主控台的設定。

6.  按兩下 \[憑證 (本機電腦)\] ，展開憑證存放區，按兩下 \[個人\] ，然後按兩下 \[憑證\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果本機電腦的憑證個人存放區中沒有憑證，則匯入的憑證就沒有關聯的私密金鑰。請檢閱要求和匯入步驟。如果問題仍持續存在，請與您的憑證授權單位管理員或提供者連絡。</td>
    </tr>
    </tbody>
    </table>


7.  在 \[本機電腦的憑證個人存放區\] 中，在您匯出的憑證上按一下滑鼠右鍵，按一下 \[所有工作\] ，然後按一下 \[匯出\] 。

8.  在憑證匯出精靈中，按 \[下一步\] ，選取 \[是，匯出私密金鑰\] ，然後按 \[下一步\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果 [是，匯出私密金鑰] 選項無法使用，則與該憑證關聯的私密金鑰就不會標示為可匯出。您需要重新申請憑證，確定憑證標示為允許匯出私密金鑰，才能繼續匯出。請與您的憑證授權單位管理員或提供者連絡。</td>
    </tr>
    </tbody>
    </table>


9.  在 \[匯出檔案格式\] 對話方塊中，選取 \[個人資訊交換 – PKCS\#12 (.PFX)\] ，然後選取下列項目：
    
      - 盡可能在憑證路徑中包含所有憑證
    
      - 匯出所有延伸內容
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>從 Edge Server 匯出憑證時，不要選取 [如果匯出成功即刪除私密金鑰] 。選取這個選項時，必須將憑證和私密金鑰匯入這個 Edge Server。</td>
        </tr>
        </tbody>
        </table>


10. 按 **\[下一步\]** 。

11. 輸入私密金鑰的密碼，再輸入一次密碼以進行確認，然後按 \[下一步\] 。

12. 輸入匯出憑證的路徑和檔案名稱，使用 .pfx 副檔名。路徑必須可供集區中的所有其他 Edge Server 存取，或是可透過卸除式媒體進行傳輸，例如 USB 快閃磁碟機。按 \[下一步\] 。

13. 檢閱 \[完成憑證匯出精靈\] 中的摘要，然後按一下 \[完成\] 。

14. 在 \[成功匯出\] 對話方塊中，按一下 \[確定\] 。

15. 按照本主題中的「若要匯入 Edge Server 外部介面的憑證」程序步驟，將匯出的憑證檔匯入其他 Edge Server。

## 若要指派 Edge Server 外部介面的憑證

1.  在每部 Edge Server 上，於 \[部署精靈\] 中的 **\[步驟 3：要求、安裝或指派憑證\]** 旁邊的 **\[再執行一次\]** 。

2.  在 **\[可用憑證工作\]** 頁面上，按一下 **\[指派現有的憑證\]** 。

3.  在 **\[憑證指派\]** 頁面上，按一下 **\[外部邊緣憑證\]** 並選取 **\[進階憑證用途\]** 核取方塊。

4.  在 **\[進階憑證用途\]** 頁面上，選取所有核取方塊以將憑證指派給所有用途。

5.  在 **\[憑證存放區\]** 頁面上，選取您為 Edge Server 外部介面要求與匯入的公用憑證。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您所要求與匯入的憑證不在清單中，可用的疑難排解方法之一就是確認憑證的主體名稱與主體別名符合憑證的所有需求，同時，如果您是手動匯入憑證與憑證鏈結 (而非使用先前的步驟進行)，表示該憑證位於正確的憑證存放區 (電腦憑證存放區，而非使用者或服務憑證存放區)。</td>
    </tr>
    </tbody>
    </table>


6.  在 **\[憑證指派摘要\]** 頁面上，檢閱您的設定，然後按 **\[下一步\]** 指派憑證。

7.  在精靈完成頁面中，按一下 \[完成\] 。

8.  在使用以上步驟指派邊緣憑證之後，開啟每部伺服器上的「憑證」嵌入式管理單元，並依序展開 **\[憑證 (本機電腦)\]** 和 **\[個人\]** ，接著按一下 **\[憑證\]** ，然後確認在詳細資料窗格中有列出該憑證。

9.  如果您的部署範圍包括多部 Edge Server，請為每部 Edge Server 重複這個程序。

