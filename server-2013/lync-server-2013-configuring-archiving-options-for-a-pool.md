---
title: 設定集區的封存選項
TOCTitle: 設定集區的封存選項
ms:assetid: b7cb0fd8-3d31-4858-a75c-c66a7742556e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205200(v=OCS.15)
ms:contentKeyID: 49292097
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定集區的封存選項

 

_**上次修改主題的時間：** 2012-10-10_

您可在每個集區的 \[封存\] 設定中建立與設定選項，指定要套用到每個集區的 \[封存\] 選項。集區設定優先於全域設定與網站設定，但僅適用於在集區設定中所指定的集區。

如需關於封存組態如何運作的詳細資訊，包含全域、網站與集區設定的階層，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須先在 [封存] 組態中指定所有適當選項，才能啟用封存功能。如需詳細資訊，請參閱部署文件中<a href="lync-server-2013-configuring-archiving-options.md">設定封存選項</a>。</td>
</tr>
</tbody>
</table>


## 在集區層級設定封存選項

1.  使用指派到 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入 Admin URL 以開啟 Lync Server 2013 控制台。如需關於可用來啟動 Lync Server 2013 控制台不同方法的詳細資訊，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存組態\]。

4.  在 \[封存組態\] 頁面上，按一下 \[新增\]，然後再按一下 \[集區組態\]。

5.  在 \[選取服務\] 中，選取要設定封存的集區。

6.  在 \[建立新的封存設定\] 的 \[封存設定\] 下拉式清單中，選取下列其中一個封存選項：
    
      - \[停用封存\]
    
      - \[封存 IM 工作階段\]
    
      - \[封存 IM 與 Web 會議工作階段\]

7.  也在 \[建立新的封存設定\] 頁面中，執行下列動作：
    
      - 若要在封存無法使用時封鎖活動，請選取 \[封存失敗時封鎖立即訊息 (IM) 和 Web 會議工作階段\] 核取方塊。
    
      - 若要使用 Microsoft Exchange Server 存放封存資料，請按一下 \[Microsoft Exchange 整合\] 核取方塊。
    
      - 若要啟用資料清除，請選取 \[啟用封存資料的清除\] 核取方塊，然後執行下列其中一項：
        
          - 若要指定在特定天數後進行清除，請按一下 \[在最大持續期限 (天) 後清除匯出的封存資料和儲存的封存資料\]，然後指定天數。
        
          - 若要限制只清除已匯出的封存資料，請按一下 \[只清除匯出的封存資料\]。

8.  按一下 \[認可\]。

