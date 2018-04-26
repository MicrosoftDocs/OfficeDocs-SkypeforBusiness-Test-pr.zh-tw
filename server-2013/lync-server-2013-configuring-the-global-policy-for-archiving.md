---
title: 設定封存的全域原則
TOCTitle: 設定封存的全域原則
ms:assetid: 58341d6b-c3ff-4dd9-b1c7-0048f33861ca
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204906(v=OCS.15)
ms:contentKeyID: 49290975
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定封存的全域原則

 

_**上次修改主題的時間：** 2012-10-09_

當您部署前端伺服器時，Lync Server 會建立封存的全域原則。預設會在全域原則中停用封存。除非您設定網站或使用者原則 (其優先於全域原則)，或者您針對部分或所有使用者使用 Microsoft Exchange 整合，否則全域原則會控制是否要針對整個部署的內部與外部通訊啟用封存。如果您使用 Microsoft Exchange 整合，全域原則便不會套用至任何位於 Exchange 2013 且其信箱狀態為 \[就地保留\] 的使用者。

如需有關封存原則如何運作 (包含全域、網站及使用者原則的階層)，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您針對部署啟用 Microsoft Exchange 整合，Exchange 就地保留原則便會控制是否要針對位於 Exchange 2013 且其信箱狀態為 [就地保留] 的使用者啟用封存。如需詳細資訊，請參閱部署文件中的<a href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">設定使用 Exchange Server 整合時的封存原則</a>。<br />
啟用封存之前，您應該先在封存設定中指定所有適當的選項。如需詳細資訊，請參閱部署文件中的<a href="lync-server-2013-configuring-archiving-options.md">設定封存選項</a>。</td>
</tr>
</tbody>
</table>


## 使用 Lync Server 封存資料庫時設定封存的全域原則

1.  使用指派到 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 2013 控制台。如需各種 Lync Server 2013 控制台啟動方法的詳細資訊，請參閱＜[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)＞。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存原則\]。

4.  在 **\[封存原則\]** 頁面上，依序按一下 **\[通用\]** 和 **\[編輯\]**，然後按一下 **\[顯示詳細資料\]**。

5.  在 \[編輯封存原則 - 通用\] 中，執行下列動作：
    
      - 如果您不想要使用此預設全域名稱，請在 **\[名稱\]** 中指定全域原則的新名稱。
    
      - 在 **\[描述\]** 中，提供有關使用者原則的資訊 (例如，*divisionName* 的全域原則)。
    
      - 若要控制未特別透過網站原則或使用者原則控制之所有網站及使用者的內部通訊封存，請選取或清除 **\[封存內部通訊\]** 核取方塊。
    
      - 若要控制未特別透過網站原則或使用者原則控制之所有網站及使用者的外部通訊封存，請選取或清除 \[封存外部通訊\] 核取方塊。

6.  按一下 **\[認可\]**。

