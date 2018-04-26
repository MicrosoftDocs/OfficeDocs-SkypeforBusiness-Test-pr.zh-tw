---
title: 部署 Lync Server 2013 試驗集區
TOCTitle: 部署 Lync Server 2013 試驗集區
ms:assetid: a81aba1e-e636-434b-8c56-4150435bb55d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205144(v=OCS.15)
ms:contentKeyID: 49291931
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 部署 Lync Server 2013 試驗集區

 

_**上次修改主題的時間：** 2013-11-22_

移轉至 Lync Server 2013 的其中一個必要步驟就是部署試驗集區。試驗集區是您用來測試 Lync Server 2013 是否能與 Lync Server 2010 部署共存之處。共存只是在您將所有使用者與集區移至 Lync Server 2013 之前的暫時狀態。

當您部署試驗集區時，會用到 \[定義新前端集區精靈\]。您應該在 Lync Server 2013 試驗集區中部署與 Lync Server 2010 集區中相同的功能與工作負載群。如果您部署了 封存伺服器、 監控伺服器和 System Center Operations Manager 以封裝或監控您的 Lync Server 2010 環境，而且想要在整個移轉過程中持續進行封裝或監控，您也會需要在您的試驗環境中部署這些功能。您為了封存或監控 Lync Server 2010 環境所部署的版本不會在 Lync Server 2013 環境中擷取資料。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>下列程序討論在整個試驗集區部署程序中，您應考量的功能和設定。本節只著重在部署試驗集區時應該考量的要點。如需詳細步驟，請參閱《 <a href="lync-server-2013-deploying-lync-server.md">部署 Lync Server 2013</a>部署指南》。</td>
</tr>
</tbody>
</table>


**部署 Lync Server 2013 試驗集區**

1.  以 Domain Admins 群組與 RTCUniversalServerAdmins 群組成員的身分，登入安裝了拓撲產生器的電腦。

2.  展開樹狀結構，直到到達 **Lync Server 2013** 的 \[Enterprise Edition 前端集區\] 為止。

3.  用滑鼠右鍵按一下 \[Enterprise Edition 前端集區\] ，然後選取 \[新增前端集區\] 。
    
    ![拓撲產生器伺服器集區選取子功能表](images/JJ205144.c2feed27-3418-42a6-a254-76e83607db9c(OCS.15).jpg "拓撲產生器伺服器集區選取子功能表")

4.  輸入集區 FQDN。當您定義試驗集區時，可以選擇部署 Enterprise Edition 前端集區或 Standard Edition 伺服器。 Lync Server 2013 不需要試驗集區功能與舊版集區中的部署相同。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您為試驗集區所定義的集區或伺服器完整網域名稱 (FQDN) 不得重複。它不能與目前部署的 Lync Server 2010 集區同名，或是與其他目前部署的伺服器同名。</td>
    </tr>
    </tbody>
    </table>
    
    ![\[定義新前端集區精靈 FQDN\] 頁面](images/JJ205144.c5fd138c-e75a-413a-827f-b1461c996d40(OCS.15).jpg "[定義新前端集區精靈 FQDN] 頁面")

5.  在 \[選取功能\] 頁面上，選取您希望此前端集區擁有的功能之對應核取方塊。例如，如果您只部署立即訊息 (IM) 和目前狀態功能，則可以選取 \[會議\] 核取方塊以允許多方 IM，但是不要選取 \[電話撥入式 (PSTN) 會議\]、\[企業語音\] 或 \[通話許可控制\] 核取方塊，因為它們代表語音、視訊和共同作業會議功能。如需選取功能的其他資料，請參閱部署文件中的＜ [在 Lync Server 2013 中定義和設定前端集區或 Standard Edition Server](lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md)＞。
    
    ![前端集區的 \[選取功能\] 頁面](images/JJ205144.5c3f3ff9-6e17-4d66-9b13-3bd55b38246b(OCS.15).jpg "前端集區的 [選取功能] 頁面")

6.  在 \[選取組合的伺服器角色\] 頁面上，建議您組合 Lync Server 2013 中的 中繼伺服器。當您使用 Lync Server 2013 合併舊的拓撲時，要先組合 Lync Server 2010中繼伺服器。合併拓撲並設定 Lync Server 2013  中繼伺服器之後，即可決定是否要保留組合後的 中繼伺服器，或是要在稍後於部署程序中將 中繼伺服器 角色移至 Lync Server 2013 時，將其變更為獨立伺服器。
    
    ![前端集區的 \[選取組合的伺服器角色\] 頁面](images/JJ205144.e00b7eba-010b-44ed-b0a6-6ab3e534fb8c(OCS.15).jpg "前端集區的 [選取組合的伺服器角色] 頁面")

7.  在試驗集區部署過程中，請勿在 \[建立伺服器角色與此前端集區的關聯\] 頁面上選擇 \[啟用要供此前端集區之媒體元件使用的 Edge 集區\] 選項。此為您會在移轉較後期階段時才啟用及上線的功能。目前請將此設定留空。
    
    ![\[建立伺服器角色與前端集區的關聯\] 頁面](images/JJ205144.2d95a798-ad76-4dad-9392-ce41f4d938d1(OCS.15).jpg "[建立伺服器角色與前端集區的關聯] 頁面")

8.  在 \[選取 Office Web Apps Server\] 頁面上，按一下 \[新增\] ，然後指定應用程式伺服器的 FQDN。
    
    ![定義新 Office Online Server FQDN 內容](images/JJ205144.25c6b455-f1b8-4326-a569-6e338153d398(OCS.15).jpg "定義新 Office Online Server FQDN 內容")

9.  在 \[定義封存 SQL Server 儲存區\] 頁面上，定義 Lync Server Archiving 和 Monitoring 的 SQL Server 儲存區，選取先前為 Lync Server 2013 建立的 SQL Server 執行個體。
    
    ![\[定義封存 SQL Server 存放區\] 頁面](images/JJ205144.0f76f1dc-d0d7-42a0-aea3-400b8e1f35cd(OCS.15).jpg "[定義封存 SQL Server 存放區] 頁面")

10. 若要發行拓撲，請用滑鼠右鍵按一下 **Lync Server** 節點，然後按一下 \[發行拓撲\] 。
    
    ![顯示設定拓撲的拓撲產生器](images/JJ205144.c3eafa20-159e-4355-a23d-9f72aeb26037(OCS.15).jpg "顯示設定拓撲的拓撲產生器")

11. 發行程序完成時，請按一下 \[完成\] 。

若要安裝本機版的設定儲存區及啟動所需的服務，請參閱部署文件中的＜ [針對 Lync Server 2013 設定前端伺服器和前端集區](lync-server-2013-setting-up-front-end-servers-and-front-end-pools.md)＞。


