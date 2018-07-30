---
title: 將 Lync Server 封存原則套用至使用者
TOCTitle: 將 Lync Server 封存原則套用至使用者
ms:assetid: a23e4876-aa8d-4f49-a3bd-3696616e8290
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205143(v=OCS.15)
ms:contentKeyID: 49291852
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將 Lync Server 封存原則套用至使用者

 

_**上次修改主題的時間：** 2012-10-10_

建立 Lync Server 使用者原則後，您必須先將原則套用至 Lync Server 2013 所屬的特定使用者或使用者群組，此原則才會生效。如需針對特定使用者建立使用者原則的詳細資訊，請參閱部署文件中的＜[在 Lync Server 中建立和設定封存的使用者原則](lync-server-2013-creating-and-configuring-user-policies-for-archiving-in-lync-server.md)＞。

如需封存原則運作方式的詳細資訊 (包含全域、網站和使用者原則的階層)，請參閱規劃文件、部署文件或作業文件中的＜[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要設定及使用封存，必須先部署封存。如需詳細資料，請參閱部署文件中的<a href="lync-server-2013-deploying-archiving.md">在 Lync Server 2013 中部署封存</a>。<br />
如果您的部署已啟用 Microsoft Exchange 整合，則 Exchange 就地保留原則會控制 Exchange 2013 所屬使用者是否啟用封存並就地保留其信箱。如需詳細資訊，請參閱部署文件中的＜<a href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">設定使用 Exchange Server 整合時的封存原則</a>＞。<br />
您必須先在 [封存] 組態中指定所有適當選項，才能啟用封存功能。如需詳細資訊，請參閱部署文件中的＜<a href="lync-server-2013-configuring-archiving-options.md">設定封存選項</a>＞。</td>
</tr>
</tbody>
</table>


## 將 Lync Server 封存原則套用至使用者

1.  使用指派到 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入 Admin URL 以開啟 Lync Server 2013 控制台。如需各種 Lync Server 2013 控制台啟動方法的詳細資訊，請參閱＜[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)＞。

3.  在左導覽列中，按一下 \[使用者\]，然後搜尋想要設定的使用者帳戶。

4.  在列出搜尋結果的表格中，依序按一下使用者帳戶、\[編輯\] 及 \[顯示詳細資料\]。

5.  在 \[封存原則\] 下的 \[編輯 Lync Server 使用者\] 中，選取想要套用的封存使用者原則。
    
    > [!NOTE]  
    > [&lt;自動&gt;] 設定會套用預設伺服器安裝設定。伺服器會自動套用這些設定。
    


6.  按一下 \[認可\]。

