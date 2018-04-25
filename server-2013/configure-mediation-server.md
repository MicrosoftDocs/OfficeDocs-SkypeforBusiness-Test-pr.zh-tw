---
title: 設定中繼伺服器
TOCTitle: 設定中繼伺服器
ms:assetid: 583236fd-33cd-4045-81df-baa58ed07779
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204913(v=OCS.15)
ms:contentKeyID: 49290988
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定中繼伺服器

 

_**上次修改主題的時間：** 2012-09-28_

本程序詳細說明設定 Lync Server 2013 集區以使用 Lync Server 2013 中繼伺服器 (而不是舊版 Office Communications Server 2007 R2 中繼伺服器) 所需的步驟。

若要在新增或移除伺服器角色時順利發行、啟用或停用拓撲，您應該以 RTCUniversalServerAdmins 和 Domain Admins 群組成員的使用者身分登入。您也可以委派適當的系統管理員權限與授權來新增伺服器角色。如需詳細資訊，請參閱 Standard Edition Server 或 Enterprise Edition Server 之部署文件中的委派設定權限。若要變更其他設定，只需具備 RTCUniversalServerAdmins 群組的成員資格即可。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需尋找能和 Lync Server 2013 搭配使用之完整 PSTN 閘道、IP-PBX 以及 SIP 主幹連線服務的詳細資訊，請參閱＜Microsoft Unified Communications 開啟互通性程式＞，網址為： <a href="http://go.microsoft.com/fwlink/?linkid=206015%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=206015&amp;clcid=0x404</a>。</td>
</tr>
</tbody>
</table>


## 使用拓撲產生器設定中繼伺服器

1.  從拓撲產生器開啟現有的拓撲。

2.  在左窗格中，瀏覽至 **\[PSTN 閘道\]** 。

3.  以滑鼠右鍵按一下 **\[PSTN 閘道\]** ，然後按一下 **\[新增 IP/PSTN 閘道\]** 。

4.  在 **\[定義新的 IP/PSTN 閘道\]** 頁面中填入下列資訊：
    
      - 輸入閘道 FQDN 或 IP 位址。如果閘道使用 TLS 通訊協定，就需要閘道的 FQDN。
    
      - 接受 **\[IP/PSTN 閘道的聆聽連接埠\]** 的預設值；其如有修改，請輸入新的聆聽連接埠。
    
      - 設定 **\[SIP 傳輸通訊協定\]** 。

5.  在左窗格中，瀏覽至 **\[Enterprise Edition 前端集區\]** 或 **\[Standard Edition Server\]** 。

6.  以滑鼠右鍵按一下集區，然後按一下 \[編輯屬性\] 。

7.  在 **\[中繼伺服器\]** 底下，設定 **\[聆聽連接埠\]** 。

8.  接著，選取新建的 PSTN 閘道並按一下 **\[新增\]** ，建立關聯。

9.  在 **\[拓撲產生器\]** 中選取最頂端的節點 **\[Lync Server\]** 。

10. 在 **\[執行\]** 功能表中，選取 **\[發行拓撲\]** ，然後按 **\[下一步\]** 。

11. 當 \[發行精靈\] 完成之後，按一下 \[完成\] ，以關閉精靈。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>請務必完成下一個主題＜ <a href="change-voice-routes-to-use-the-new-lync-server-2013-mediation-server.md">變更語音路由以使用新的 Lync Server 2013 中繼伺服器</a>＞，以確認語音路由指向正確的中繼伺服器。</td>
</tr>
</tbody>
</table>

