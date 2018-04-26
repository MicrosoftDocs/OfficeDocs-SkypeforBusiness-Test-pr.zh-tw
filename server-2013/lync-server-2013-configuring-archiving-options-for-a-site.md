---
title: 設定網站的封存選項
TOCTitle: 設定網站的封存選項
ms:assetid: 59b48fd9-d5fc-40b4-abae-e9cf89ee5573
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204930(v=OCS.15)
ms:contentKeyID: 49291009
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定網站的封存選項

 

_**上次修改主題的時間：** 2012-10-09_

您可以針對這其中的每一個網站，藉由在封存設定中建立和設定選項，以指定要套用至特定網站的封存選項。網站設定優先於全域設定，但僅適用於網站設定中指定的網站。集區設定優先於網站設定

如需有關封存設定如何運作 (包含全域、網站及集區設定的階層) 的詳細資訊，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您應該先在封存設定中指定所有適當的選項，才能啟用封存。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要啟用封存，必須指定封存原則，控制全域層級及網站與使用者層級 (如其適用) 之內部及外部通訊的封存。如有設定使用者層級原則，還必須將使用者原則指派給特定使用者。如需建立及設定封存原則的詳細資料，請參閱作業文件中的<a href="lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md">在 Lync Server 2013 中管理內部與外部通訊的封存</a>。</td>
</tr>
</tbody>
</table>


## 在網站層級設定封存選項

1.  透過指派至 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任一部電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 2013 控制台。如需各種 Lync Server 2013 控制台啟動方法的詳細資訊，請參閱＜[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)＞。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存組態\]。

4.  在 **\[封存組態\]** 頁面上，按一下 **\[新增\]**，然後按一下 **\[站台組態\]**。

5.  在 **\[選取站台\]** 中，選取要設定封存的網站。

6.  在 **\[建立新的封存設定\]** 的 **\[封存設定\]** 下拉式清單方塊中，執行下列其中一項作業：
    
      - 若只要啟用立即訊息 (IM) 工作階段的封存，請按一下 **\[封存 IM 工作階段\]**。
    
      - 若要同時啟用 IM 工作階段和會議的封存，請按一下 **\[封存 IM 和 Web 會議工作階段\]**。
    
      - 若要停用原則的封存，請按一下 **\[停用封存\]**。

7.  此外，在 **\[建立新的封存設定\]** 中，執行下列動作：
    
      - 若要在封存無法使用時封鎖活動，請選取 **\[封存失敗時封鎖立即訊息 (IM) 和 Web 會議工作階段\]** 核取方塊。
    
      - 若要使用 Microsoft Exchange Server 來儲存封存資料，請按一下 **\[Microsoft Exchange 整合\]** 核取方塊。
    
      - 若要啟用資料清除，請選取 **\[啟用封存資料的清除\]** 核取方塊，然後執行下列其中一項作業：
        
          - 若要指定在特定天數後進行清除，請按一下 **\[在最大持續期限 (天) 後清除匯出的封存資料和儲存的封存資料\]**，然後指定天數。
        
          - 若要限制只清除已匯出的封存資料，請按一下 **\[只清除匯出的封存資料\]**。

8.  按一下 **\[認可\]**。

