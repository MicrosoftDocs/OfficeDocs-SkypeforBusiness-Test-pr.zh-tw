---
title: 鎖定或解除鎖定使用者 PIN
TOCTitle: 鎖定或解除鎖定使用者 PIN
ms:assetid: 3d293a8a-e182-4547-8b06-2603c3c77329
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688028(v=OCS.15)
ms:contentKeyID: 49890031
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 鎖定或解除鎖定使用者 PIN

 

_**上次修改主題的時間：** 2013-02-23_

您可以從 Lync Server 2013 控制台的 **\[使用者\]** 區段中鎖定或解除鎖定使用者的 PIN。

## 在 Lync Server 控制台中鎖定使用者的 PIN

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[使用者\]**。

4.  使用下列其中一種方法，找到使用者：
    
      - 在 **\[搜尋使用者\]** 方塊中，輸入該使用者帳戶的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或線路統一資源識別項 (URI) 的全部或頭幾個字，然後按一下 **\[尋找\]**。
    
      - 如果有儲存的查詢，請按一下 **\[開啟查詢\]** 圖示、使用 **\[開啟\]** 對話方塊擷取查詢 (.usf 檔)，然後按一下 **\[尋找\]**。

5.  (選用) 指定其他搜尋條件，縮減結果：
    
    1.  按一下 **\[新增篩選\]**。
    
    2.  輸入使用者內容，您可以自行輸入或按一下下拉式清單的箭頭以選取內容。
    
    3.  在 **\[等於\]** 下拉式清單中，按一下運算子 (例如 **\[等於\]** 或 **\[不等於\]**)。
    
    4.  視您選取的使用者內容而定，透過直接輸入文字或按一下下拉式清單中的箭頭，輸入您要用來篩選搜尋結果的準則。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>若要將更多搜尋子句加入至查詢，請按一下 <strong>[新增篩選]</strong>。</td>
        </tr>
        </tbody>
        </table>
    
    5.  按一下 **\[尋找\]**。
    
    6.  按一下使用者、**\[動作\]**，然後按一下 **\[鎖定 PIN\]**。

## 在 Lync Server 控制台中解除鎖定使用者的 PIN

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \]**\[使用者**。

4.  使用下列其中一種方法，找到使用者：
    
      - 在 **\[搜尋使用者\]** 方塊中，輸入該使用者帳戶的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或線路統一資源識別項 (URI) 的全部或頭幾個字，然後按一下 **\[尋找\]**。
    
      - 如果有儲存的查詢，請按一下 **\[開啟查詢\]** 圖示、使用 **\[開啟\]** 對話方塊擷取查詢 (.usf 檔)，然後按一下 **\[尋找\]**。

5.  (選用) 指定其他搜尋條件，縮減結果：
    
    1.  按一下 **\[新增篩選\]**。
    
    2.  輸入使用者內容，您可以自行輸入或按一下下拉式清單的箭頭以選取內容。
    
    3.  在 **\[等於\]** 下拉式清單中，按一下運算子 (例如 **\[等於\]** 或 **\[不等於\]**)。
    
    4.  視您選取的使用者內容而定，透過直接輸入文字或按一下下拉式清單中的箭頭，輸入您要用來篩選搜尋結果的準則。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>若要將更多搜尋子句加入至查詢，請按一下 <strong>[新增篩選]</strong>。</td>
        </tr>
        </tbody>
        </table>
    
    5.  按一下 **\[尋找\]**。
    
    6.  按一下使用者、**\[動作\]**，然後按一下 **\[解除鎖定 PIN\]**。

## 使用 Lync Server 管理命令介面 Cmdlet 鎖定及解除鎖定使用者 PIN

您也可以使用 Windows PowerShell 以及 Lock-CsClientPin 和 Unlock-CsClientPin Cmdlet 來鎖定及解除鎖定使用者 PIN。可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段來執行這些 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 鎖定使用者 PIN

  - 如要鎖定使用者的 PIN，請使用 Lock-CsClientPin Cmdlet。例如：
    
        Lock-CsClientPin -Identity "Ken Myer"

## 解除鎖定使用者 PIN

  - 如要解除鎖定使用者的 PIN，請使用 Unlock-CsClientPin Cmdlet。例如：
    
        Unlock-CsClientPin -Identity "Ken Myer"

如需詳細資訊，請參閱 [Lock-CsClientPin](lock-csclientpin.md) 及 [Unlock-CsClientPin](unlock-csclientpin.md) Cmdlet 的說明主題。

