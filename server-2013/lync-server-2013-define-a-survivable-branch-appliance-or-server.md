---
title: Lync Server 2013：定義 Survivable Branch Appliance 或 Survivable Branch Server
TOCTitle: 定義 Survivable Branch Appliance 或 Survivable Branch Server
ms:assetid: 1f49cfbe-30b3-4600-af15-47cb2f58d18a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398280(v=OCS.15)
ms:contentKeyID: 49290302
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中定義 Survivable Branch Appliance 或 Survivable Branch Server

 

_**上次修改主題的時間：** 2012-10-07_

如果您將 Survivable Branch Appliance 或 Server 加入拓撲時尚未予以定義，請在中央網站執行下列程序。

## 若要定義 Survivable Branch Appliance 或 Survivable Branch 伺服器

1.  依序按一下 \[開始\] 、\[程式集\] 、\[ Microsoft Lync Server 2013\] ，然後按一下 \[ Lync Server拓撲產生器\] 。

2.  在主控台樹狀目錄中，依序展開中央網站、\[分支網站\] ，以及您想要部署 Survivable Branch Appliance 或 Survivable Branch 伺服器的分支網站名稱。

3.  以滑鼠右鍵按一下 \[ Survivable Branch Appliance\] ，然後按一下 \[新增 Survivable Branch Appliance\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>[ Survivable Branch Appliance] 就是用來定義 Survivable Branch 伺服器和 Survivable Branch Appliance 的位置。</td>
    </tr>
    </tbody>
    </table>


4.  在 \[定義 Survivable Branch Appliance\] 對話方塊中，按一下 \[FQDN\] ，輸入要部署在分支網站的 Survivable Branch Appliance 或 Survivable Branch 伺服器的完整網域名稱 (FQDN)，然後按 \[下一步\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您定義的是 Survivable Branch Appliance，則在 <strong>[FQDN]</strong> 輸入的名稱必須與 <strong>servicePrincipalName</strong> 屬性中指派的 Survivable Branch Appliance FQDN 相同。如需詳細資訊，請參閱＜ <a href="lync-server-2013-add-a-survivable-branch-appliance-to-active-directory.md">在 Lync Server 2013 中將 Survivable Branch Appliance 新增到 Active Directory</a>＞。</td>
    </tr>
    </tbody>
    </table>


5.  依序按一下 **\[前端集區\]** 、 Survivable Branch Appliance 或 Survivable Branch 伺服器 要連接的中央網站上的前端伺服器 (使用者服務集區)，以及 **\[下一步\]** 。

6.  依序按一下 \[Edge Server\] 和 Survivable Branch Appliance 或 Survivable Branch 伺服器要連接的 Edge 集區以便提供 PSTN 連線給分支網站的遠端使用者，然後按 \[下一步\] 。

7.  按一下 **\[閘道 FQDN 或 IP 位址\]** ，然後輸入 Survivable Branch Appliance 或 Survivable Branch 伺服器 相關聯之閘道對等端的 FQDN 或 IP 位址，以便用於路由傳送撥入或撥出的 PSTN 電話。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您定義的是 Survivable Branch Appliance，此為 Survivable Branch Appliance 內的中繼伺服器所要連接的閘道，以提供 PSTN 連線。</td>
    </tr>
    </tbody>
    </table>


8.  按一下 **\[IP/PSTN 閘道的聆聽連接埠\]** ，接受預設連接埠。

9.  在 **\[SIP 傳輸通訊協定\]** 中，按一下 Survivable Branch Appliance 或 Survivable Branch 伺服器 要使用的傳輸通訊協定，然後按一下 **\[完成\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>基於安全考量，強烈建議您使用傳輸層安全性 (TLS)。如果您定義的是 Survivable Branch Appliance，請參閱 Survivable Branch Appliance 廠商文件，確認您的 Survivable Branch Appliance 有支援 TLS 通訊協定。</td>
    </tr>
    </tbody>
    </table>


10. 在主控台樹狀目錄中，以滑鼠右鍵按一下新的 Survivable Branch Appliance 或 Server、按一下 **\[拓撲\]** ，然後按一下 **\[發行\]** 。

**下一步** ： [使用 Lync Server 2013 部署 Survivable Branch Appliance 或 Server - 分支網站工作](lync-server-2013-deploy-a-survivable-branch-appliance-or-server-branch-site-task.md)

