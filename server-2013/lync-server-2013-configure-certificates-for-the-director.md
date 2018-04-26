---
title: Lync Server 2013：為 Director 設定憑證
TOCTitle: 為 Director 設定憑證
ms:assetid: 22988186-15ae-43b1-92f4-0adb3b75a7fd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398296(v=OCS.15)
ms:contentKeyID: 49290334
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 Director 的憑證

 

_**上次修改主題的時間：** 2012-09-08_

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您執行 [憑證精靈] 時，請確定您用來登入的帳戶，是具有您要使用之憑證範本類型適當權限的群組成員。根據預設， Lync Server 2013 憑證要求會使用 Web 伺服器憑證範本。如果您要以 RTCUniversalServerAdmins 群組成員的帳戶使用此範本來要求憑證，請確定群組具有使用該範本所需的註冊權限。</td>
</tr>
</tbody>
</table>


每個 Director 都需要預設憑證、Web 內部憑證以及 Web 外部憑證。如需 Director 憑證需求的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中內部伺服器的憑證需求](lync-server-2013-certificate-requirements-for-internal-servers.md)＞。

請使用下列程序設定 Director 憑證。為每個 Director 重複這個程序。此程序步驟說明如何從組織部署之內部企業根憑證授權單位 (CA) 設定憑證，以及使用離線要求程序設定憑證。如需從外部 CA 取得憑證的詳細資訊，請洽詢您的支援小組。

## 為 Director 或 Director 集區設定憑證

1.  在 Lync Server 部署精靈的 **\[步驟 3：要求、安裝或指派憑證\]** 旁邊，按一下 **\[執行\]** 。

2.  在 **\[憑證精靈\]** 頁面中，按一下 **\[要求\]** 。

3.  在「憑證要求」 頁面上，按 \[下一步\] 。

4.  在「延遲或立即要求」 頁面上，接受預設的 \[立即將此要求傳送到線上憑證授權單位\] 選項，然後按 \[下一步\] 。

5.  在 **\[選擇憑證授權單位 (CA)\]** 頁面上，按一下您要使用的內部 Windows 憑證授權單位，然後按 **\[下一步\]** 。

6.  在 **\[憑證授權單位帳戶\]** 頁面上，指定若您據以登入的帳戶不具備要求憑證的充分授權時，要使用的其他憑證，然後按 **\[下一步\]** 。

7.  在 **\[指定其他憑證範本\]** 頁面上，按 **\[下一步\]** 。

8.  在 **\[名稱和安全性設定\]** 頁面上，您可指定 **\[易記名稱\]** 、接受 2048 位元金鑰長度，然後按 **\[下一步\]** 。

9.  在 **\[組織資訊\]** 頁面上，您可選擇性指定組織資訊，然後按 **\[下一步\]** 。

10. 在 **\[地理資訊\]** 頁面上，您可選擇性指定地理資訊，然後按 **\[下一步\]** 。

11. 在 **\[主體名稱 / 主體替代名稱\]** 頁面上，按 **\[下一步\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>主體替代名稱清單應該包含您安裝 Director 的電腦名稱 (若是單一 Director) 或 Director 集區名稱，以及為組織設定的簡單 URL 名稱。</td>
    </tr>
    </tbody>
    </table>


12. 在「主體別名 (SAN) 上的 SIP 網域設定」 頁面上，為您要 Director 處理的所有網域選取 \[設定的 SIP 網域\] ，然後按 **\[下一步\]** 。

13. 在 **\[設定其他主體替代名稱\]** 頁面上，增加其他必要的主體替代名稱，然後按 **\[下一步\]** 。

14. 在 **\[憑證要求摘要\]** 頁面上，按 **\[下一步\]** 。

15. 在 **\[執行命令\]** 頁面上，等命令完成執行後，按 **\[下一步\]** 。

16. 在 **\[線上憑證要求狀態\]** 頁面上，按一下 **\[完成\]** 。

17. 在 **\[憑證指派\]** 頁面上，按 **\[下一步\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您要檢視憑證，請按兩下清單中的憑證。</td>
    </tr>
    </tbody>
    </table>


18. 在 **\[憑證指派摘要\]** 頁面上，按 **\[下一步\]** 。

19. 在 **\[執行命令\]** 頁面上，等命令完成執行後，按一下 **\[完成\]** 。

20. 在 **\[憑證精靈\]** 頁面中，按一下 **\[關閉\]** 。

