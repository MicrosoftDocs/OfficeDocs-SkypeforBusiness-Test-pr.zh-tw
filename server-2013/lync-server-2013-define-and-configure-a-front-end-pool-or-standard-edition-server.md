---
title: Lync Server 2013：定義和設定前端集區或 Standard Edition Server
TOCTitle: 定義和設定前端集區或 Standard Edition Server
ms:assetid: 713fc263-23dd-414a-b001-82932e4fe966
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398538(v=OCS.15)
ms:contentKeyID: 49291281
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中定義和設定前端集區或 Standard Edition Server

 

_**上次修改主題的時間：** 2015-03-09_

此程序不需要本機系統管理員或已授權網域群組中的成員資格。您應該以標準使用者身分登入電腦。

如果您要部署的是企業伺服器，集區中 前端伺服器的數目下限必須隨時保持執行狀態。下表摘要說明這些要求。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>集區中的前端伺服器總數</th>
<th>集區正常運作所需的伺服器數</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1-2</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>3-4</p></td>
<td><p>2</p></td>
</tr>
<tr class="odd">
<td><p>5-6</p></td>
<td><p>3</p></td>
</tr>
<tr class="even">
<td><p>7-8</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>9-10</p></td>
<td><p>5</p></td>
</tr>
<tr class="even">
<td><p>11-12</p></td>
<td><p>6</p></td>
</tr>
</tbody>
</table>


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>對 Lync Server 2013 而言，每當您從集區新增或移除前端伺服器，皆必須重新啟動服務。移除和新增伺服器應以個別作業執行。例如，如果您要新增兩部前端伺服器以及移除兩部前端伺服器，請使用下列程序：
<ol>
<li><p>移除兩部前端伺服器。</p></li>
<li><p>發行並重新啟動拓撲。</p></li>
<li><p>重新啟動服務</p></li>
<li><p>新增兩部前端伺服器。</p></li>
<li><p>發行並重新啟動拓撲。</p></li>
<li><p>重新啟動服務。</p></li>
</ol></td>
</tr>
</tbody>
</table>


當您定義好拓撲，請使用下列步驟為您的網站定義 前端集區。如需定義拓撲的詳細資訊，請參閱＜ [針對 Lync Server 2013 在拓撲建置器中定義和設定拓撲](lync-server-2013-define-and-configure-a-topology-in-topology-builder.md)＞。

## 定義 前端集區

1.  在 \[定義新前端集區\] 精靈的 **\[定義新 前端集區\]** 頁面上，按 **\[下一步\]** 。

2.  在 **\[定義 前端集區 FQDN\]** 頁面上，輸入所建立集區的完整網域名稱 (FQDN)，然後依序按一下 **\[Enterprise Edition 前端集區\]** 和 **\[下一步\]** 。

3.  在 \[定義此集區中的電腦\] 頁面上，輸入集區中第一個 前端伺服器 的電腦 FQDN，然後按一下 \[新增\]。請針對任何其他想要新增至集區的電腦 (最多十二部) 重複此步驟，然後按 \[下一步\]。

4.  
    
    在 \[選取功能\] 頁面上，選取您希望此前端集區擁有的功能之對應核取方塊。例如，如果您只部署立即訊息 (IM) 和目前狀態功能，則可以選取 \[會議\] 核取方塊以允許多方 IM，但是不要選取 \[電話撥入式 (PSTN) 會議\]、\[企業語音\] 或 \[通話許可控制\] 核取方塊，因為它們代表語音、視訊和共同作業會議功能。
    
      - **會議**   此選項可啟用豐富的功能組合，包括
        
          - 可讓多方人員 (兩方以上) 同時參與單一 IM 工作階段的 IM 功能
        
          - 會議功能內含文件共同作業、應用程式共用與桌面共用。
        
          - A/V 會議功能可方便使用者啟動即時音訊/視訊 (A/V) 會議，而且不需要藉助諸如 Live Meeting 服務或協力廠商音訊橋接之類的外部服務即可完成。
    
      - **電話撥入式 (PSTN) 會議**   允許使用者透過公共交換電話網路 (PSTN)，而不需要透過音訊會議提供者，即可加入 Lync Server 2013 的音訊部分。
    
      - **Enterprise Voice**   Enterprise Voice 是 Lync Server 2013 中可讓使用者撥打及接聽電話的 VoIP 解決方案。如果您打算使用 Lync Server 2013 執行語音通話、語音信箱或其他需要用到硬體裝置或軟體用戶端的功能，請部署這項功能。
    
      - **通話許可控制服務 (CAC)**   CAC 是一種根據可用頻寬限制，判斷是否允許建立即時通訊工作階段 (例如語音或視訊通話) 的方式。如果您只有部署 IM 與顯示狀態功能，那就不需要部署 CAC，因為兩者都不會用到 CAC 功能。
    
      - **封存**   封存提供一種方法，讓您可封存透過 Lync Server 2013 傳送的 IM 內容、會議內容或兼具二者。
    
      - **監控**   監控伺服器可讓您收集網路和端點上描述媒體品質的數值資料，還有與 VoIP 通話、IM 訊息、A/V 交談、會議、應用程式共用和檔案傳輸相關的使用資訊，以及通話錯誤及通話失敗之疑難排解資訊。
    
    > [!NOTE]  
    > 如果您想在部署中啟用 CAC，每個中央網站中只能針對一個集區啟用 CAC。如果您是部署語音功能或 A/V 會議，則建議使用 CAC。
    
    
    下表說明可用的功能 (上方) 以及提供給使用者使用的功能 (左側)。表中的選項代表您應該為組織選取並啟用的功能。
    
    
    <table>
    <colgroup>
    <col style="width: 20%" />
    <col style="width: 20%" />
    <col style="width: 20%" />
    <col style="width: 20%" />
    <col style="width: 20%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th></th>
    <th>會議</th>
    <th>電話撥入式會議</th>
    <th>企業語音</th>
    <th>通話許可控制</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>立即訊息和目前狀態</p></td>
    <td><p>X</p></td>
    <td><p></p></td>
    <td><p></p></td>
    <td><p></p></td>
    </tr>
    <tr class="even">
    <td><p>會議</p></td>
    <td><p>X</p></td>
    <td><p>X</p></td>
    <td><p></p></td>
    <td><p></p></td>
    </tr>
    <tr class="odd">
    <td><p>A/V 會議</p></td>
    <td><p>X</p></td>
    <td><p>X</p></td>
    <td><p></p></td>
    <td><p>X</p></td>
    </tr>
    <tr class="even">
    <td><p>企業語音</p></td>
    <td><p></p></td>
    <td><p></p></td>
    <td><p>X</p></td>
    <td><p>X</p></td>
    </tr>
    </tbody>
    </table>


5.  在 **\[選取組合的伺服器角色\]** 頁面上，您可以選擇將 中繼伺服器組合在 前端伺服器上，或是將其部署為獨立伺服器。
    
    您可以將 中繼伺服器組合在 前端集區上。
    
      - 如果您想要將 中繼伺服器組合在 Enterprise Edition 前端集區上，請確定已選取核取方塊。這些伺服器角色就會部署至集區伺服器上。
    
      - 如果您想要將 中繼伺服器部署為獨立伺服器，請清除適當的核取方塊。在完整部署 前端伺服器之後，您將使用不同的部署步驟來部署 中繼伺服器。
    
    > [!NOTE]  
    > 建議您盡可能組合中繼伺服器。如需組合的或獨立中繼伺服器支援的詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-components-and-topologies-for-mediation-server.md">Lync Server 2013 中之中繼伺服器的元件和拓撲</a>＞。
    


6.  \[建立伺服器角色與此前端集區的關聯\] 頁面可讓您定義伺服器角色，並建立伺服器角色與 前端集區 的關聯。以下是可用的角色：
    
    **啟用 Edge 集區**    可定義及關聯單一 Edge Server 或 Edge Server 集區。 Edge Server 可協助組織內部使用者及組織外部人員 (包括同盟使用者) 順利進行通訊及共同作業。
    
    您可透過以下兩種案例，部署及關聯伺服器角色：
    
    在案例一當中，您可以為全新安裝定義新的拓撲。您可透過下列兩種方式之一進行安裝後續動作：
    
      - 清除核取方塊，並開始定義拓撲。發行、設定及測試前端和後端伺服器角色之後，您可以再次執行 拓撲產生器，以將角色伺服器新增至拓撲。此策略可讓您測試 前端集區 和執行 SQL Server 的伺服器，而不受其他角色的干擾。完成初始測試之後，您可以再次執行 拓撲產生器 以選取需要部署的角色。
    
      - 選取您需要安裝的角色，然後設定硬體以配合選取的角色。
    
    在案例二中，您已有現成的部署項目及可部署新角色的基礎結構，或者您需要將現有的角色與新的 前端伺服器關聯：
    
      - 在此案例中，您將選取想要部署的角色，或是將之與新的 前端伺服器關聯。不管是哪一種情況，您都需要先定義角色並設定需要的硬體後，才開始安裝。

7.  在 **\[定義 SQL 存放區\]** 頁面上，執行下列其中一項：
    
      - 若要使用拓撲中已定義的現有 SQL Server 存放區，請從 **\[SQL 存放區\]** 選取一個執行個體。
    
      - 若要定義新的 SQL Server 執行個體來儲存集區資訊，請按一下 **\[新增\]** ，然後在 **\[定義新 SQL 存放區\]** 對話方塊中指定 **\[SQL Server FQDN\]** 。
    
      - 若要指定 SQL Server 執行個體的名稱，請選取 **\[具名執行個體\]** ，然後指定執行個體的名稱。
    
      - 若要使用預設執行個體，請按一下 **\[預設執行個體\]** 。
    
      - 若要使用 SQL 鏡像，請選取 **\[啟用 SQL 鏡像\]** ，並選取現有執行個體或建立新的執行個體。

8.  在 **\[定義檔案共用\]** 頁面上，執行下列其中一項：
    
      - 若要使用拓撲中已經定義的檔案共用，選取 **\[使用先前定義的檔案共用\]** 。
    
      - 若要定義新的檔案共用，請選取 **\[定義新的檔案共用\]** ，並在 **\[檔案伺服器 FQDN\]** 方塊中輸入要在其上設置檔案共用的現有檔案伺服器的 FQDN，然後在 **\[檔案共用\]** 方塊中輸入檔案共用名稱。
    
    > [!IMPORTANT]  
    > Lync Server 2013 的檔案共用不能位在 前端伺服器上。請注意，在此範例中，檔案共用已位在 SQL Server 型後端伺服器上。這個位置可能不符合貴組織的最佳需求，使用檔案伺服器可能會更適合。您不需要先建立檔案共用，就能定義檔案共用。在您發行拓撲之前，必須先在定義檔案共用的位置上加以建立。
    


9.  在 **\[指定 Web 服務 URL\]** 頁面上，執行下列其中一項或兩項：
    
    > [!IMPORTANT]  
    > 基礎 URL 是 URL 的 Web 服務識別 (去除 https://)。例如，如果集區的 Web 服務的完整 URL 為 https://pool01.contoso.net，則基底 URL 是 pool01.contoso.net。
    
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您有一個以上 前端集區或 前端伺服器，則外部 Web 服務 FQDN 必須為唯一名稱。例如，如果您將 前端伺服器外部 Web 服務 FQDN 定義為 <strong>pool01.contoso.com</strong>，您便無法將 <strong>pool01.contoso.com</strong> 始用於其他 前端集區或 前端伺服器。</td>
    </tr>
    </tbody>
    </table>
    
    1.  如果您是設定 DNS 負載平衡，請選取 \[覆寫內部 Web 服務集區 FQDN\] 核取方塊，並在 \[內部基底 URL\] 中輸入內部基底 URL (必須與集區 FQDN 不同，例如，可以是 internal-\<基底 URL\>)。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果決定使用自行定義的 FQDN 來覆寫內部 Web 服務，每個 FQDN 都必須是唯一的，用於區分其他的 前端集區、Director 或 Director 集區。<strong>定義 URL 或完整網域名稱時，僅限使用標準字元</strong> (包括 A–Z、a–z、0–9 以及連字號)。請勿使用 Unicode 字元或底線 (_)。URL 或 FQDN 中的非標準字元通常不受外部 DNS 與公用 CA 支援 (也就是 URL 或 FQDN 必須指派給憑證中的主體名稱或主體別名時)。</td>
        </tr>
        </tbody>
        </table>
    
    2.  (選用) 在 **\[外部基底 URL\]** 中輸入外部基底 URL。輸入外部基底 URL 的目的，是為了與內部網域命名區分。例如，您的內部網域為 contoso.net，而外部網域名稱為 contoso.com。這時您可以使用 contoso.com 網域名稱來定義 URL。在反向 Proxy 的情況中，這種作法也很重要。外部基底 URL 網域名稱會與反向 Proxy 的 FQDN 的網域名稱相同。要啟用立即訊息和顯示狀態功能，必須要能透過 HTTP 存取 前端集區。
    
    > [!NOTE]  
    > 若要使用 DNS 負載平衡，您必須建立適當的 DNS 記錄。如需詳細資訊，請參閱＜ <a href="lync-server-2013-configure-dns-for-load-balancing.md">在 Lync Server 2013 中設定 DNS 負載平衡</a>＞。
    


10. 如果您已在 **\[選取功能\]** 頁面上選取 **\[會議\]** ，請在 **\[選取 Office Web Apps Server\]** 頁面中選取 **\[建立集區與 Office Web Apps Server 的關聯\]** ，然後按一下 **\[新增\]** (或從下拉式清單中選取現有 Office Web Apps Server)。

11. 在 **\[定義新 Office Web Apps Server\]** 對話方塊的 **\[Office Web Apps Server FQDN\]** 方塊中，請鍵入 Office Web Apps Server 電腦的完整網域名稱 (FQDN)；在執行此動作之時，您的 Office Web Apps Server 探索 URL 應會自動輸入至 **\[Office Web Apps Server 探索 URL\]** 方塊。
    
    如果 Office Web Apps Server 安裝了內部部署，並與 Lync Server 2013 位於相同的網路地區，則不應選取 **\[Office Web Apps Server 部署於外部網路 (即周邊/網際網路)\]** 選項。
    
    如果 Office Web Apps Server 部署於內部防火牆外，請選取 **\[Office Web Apps Server 部署於外部網路 (即周邊/網際網路)\]** 選項。
    
    > [!NOTE]  
    > 如需詳細資訊，請參閱＜<a href="lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md">設定 Office Web Apps Server 與 Lync Server 2013 的整合</a>＞。
    


12. 請在 **\[定義封存 SQL 存放區\]** 頁面選取現有執行個體或 SQL Server，或定義新的執行個體以儲存與封存資料相關聯的資料。

13. 請在 **\[定義監控 SQL 存放區\]** 頁面選取現有執行個體或 SQL Server，或定義新的執行個體以儲存與監控資料相關聯的資料。

14. 按 \[下一步\]。如果您已在 \[建立伺服器角色與此前端集區的關聯\] 頁面上定義了其他角色伺服器，則系統會開啟個別的角色組態精靈頁面，方便您設定這些伺服器角色。如需詳細資訊，請參閱以下內容：
    
    [在 Lync Server 2013 中部署外部使用者存取](lync-server-2013-deploying-external-user-access.md)

15. 如果您沒有選取要設定及部署的其他伺服器角色，或是當您已完成其他角色伺服器的組態時，按一下 **\[完成\]** 。

