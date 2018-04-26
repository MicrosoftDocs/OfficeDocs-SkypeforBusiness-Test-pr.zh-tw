---
title: Lync Server 2013：將 Survivable Branch Appliance 新增到 Active Directory
TOCTitle: 將 Survivable Branch Appliance 新增到 Active Directory
ms:assetid: 3e63507c-d60b-40ec-8bbe-586b1d707c3e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425906(v=OCS.15)
ms:contentKeyID: 49290687
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將 Survivable Branch Appliance 新增到 Active Directory

 

_**上次修改主題的時間：** 2012-09-23_

如果您打算部署 Survivable Branch Appliance，則必須將 Survivable Branch Appliance 新增至 Active Directory 網域服務。請在中央網站執行這項程序。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這項程序僅適用於部署 Survivable Branch Appliance。如果您部署的是 Survivable Branch 伺服器，請勿執行此程序。</td>
</tr>
</tbody>
</table>


## 若要將 Survivable Branch Appliance 新增至 Active Directory 網域服務

1.  以 Enterprise Admins 群組成員的身分，登入成員伺服器。

2.  依序按一下 **\[開始\]** 、 **\[系統管理工具\]** 和 **\[Active Directory 使用者和電腦\]** 。

3.  在 **\[執行\]** 功能表上，依序按一下 **\[新增\]** 和 **\[電腦\]** 。

4.  在 **\[新增物件 - 電腦\]** 對話方塊中，輸入 Survivable Branch Appliance 電腦物件的名稱 (例如 BranchOffice1)，然後按一下 **\[變更\]** 。

5.  在 **\[選取使用者或群組\]** 對話方塊中，新增 RTCUniversalSBATechnicians 群組，然後按一下 **\[確定\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>稍後會由分支網站的 RTCUniversalSBATechnicians 群組成員將此裝置新增至網域。</td>
    </tr>
    </tbody>
    </table>


6.  按一下 **\[確定\]** 儲存 Survivable Branch Appliance 電腦物件。

7.  依序按一下 **\[開始\]** 、 **\[系統管理工具\]** 和 **\[ADSI 編輯器\]** 。

8.  在 **\[ADSI 編輯器\]** 中，用滑鼠右鍵按一下您於先前步驟建立的電腦物件，然後按一下 **\[內容\]** 。

9.  在屬性清單中，依序按一下 **\[servicePrincipalName\]** 和 **\[編輯\]** 。

10. 在 **\[要新增的值\]** 欄位中輸入 HOST/\<SBA FQDN\>，其中 \<SBA FQDN\> 是 Survivable Branch Appliance 的完整網域名稱 (FQDN)。例如，輸入 **HOST/BranchOffice1.contoso.com** 。

11. 按一下 **\[確定\]** 儲存 **servicePrincipalName** 屬性設定，然後按一下 **\[確定\]** 儲存電腦物件內容。

12. 在 **\[Active Directory 使用者和電腦\]** 中，用滑鼠右鍵按一下 **\[使用者\]** 、按一下 **\[新增\]** ，然後按一下 **\[使用者\]** 。

13. 在精靈中輸入資訊，以建立 Survivable Branch Appliance 技術人員的網域使用者帳戶。

14. 在 **\[Active Directory 使用者和電腦\]** 中，按一下 **\[使用者\]** 、用滑鼠右鍵按一下使用者物件，然後按一下 **\[加入群組中\]** 。

15. 在 **\[輸入物件名稱來選取\]** 中，輸入 **RTCUniversalSBATechnicians** ，然後按一下 **\[確定\]** 。

16. 針對每個分支網站技術人員，重複步驟 12-15。

**下一步**：[在 Lync Server 2013 中新增分支網站至拓撲](lync-server-2013-add-branch-sites-to-your-topology.md)

