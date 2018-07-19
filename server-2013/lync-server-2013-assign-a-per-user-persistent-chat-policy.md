---
title: 指派每個使用者的常設聊天室原則
TOCTitle: 指派每個使用者的常設聊天室原則
ms:assetid: e22168f2-fde1-4f0a-b194-1fc881436822
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721908(v=OCS.15)
ms:contentKeyID: 49890349
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指派每個使用者的常設聊天室原則

 

_**上次修改主題的時間：** 2013-02-22_

您可在 Lync Server 2013 控制台 或 Lync Server 2013 管理命令介面指派個別使用者常設聊天原則。有關 常設聊天室伺服器 的建立使用者原則詳細資訊，請參閱＜[在 Lync Server 2013 中建立常設聊天室的使用者原則](lync-server-2013-create-a-user-policy-for-persistent-chat.md)＞。

## 在 Lync Server 控制台 指派個別使用者常設聊天原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[使用者\]。

4.  使用下列其中一種方法，找到使用者：
    
      - 在 \[搜尋使用者\] 方塊中，輸入該使用者帳戶的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或線路統一資源識別項 (URI) 的全部或頭幾個字，然後按一下 \[尋找\]。
    
      - 如果有儲存的查詢，請按一下 \[開啟查詢\] 圖示，使用 \[開啟\] 對話方塊擷取查詢 (.usf 檔)，然後按一下 \[尋找\]。

5.  (選用) 指定其他搜尋條件，縮減結果：
    
    1.  按一下 \[新增篩選\]。
    
    2.  輸入使用者內容，您可以自行輸入或按一下下拉式清單的箭頭以選取內容。
    
    3.  在 \[等於\] 下拉式清單中，按一下運算子 (例如 \[等於\]或 \[不等於\])。
    
    4.  依據您選取的使用者內容，輸入您要用來篩選搜尋結果的條件，您可以自行輸入或按一下下拉式清單的箭頭。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>若要將更多搜尋子句加入至查詢，請按一下 [新增篩選]。</td>
        </tr>
        </tbody>
        </table>
    
    5.  按一下 \[尋找\]。

6.  依序按一下搜尋結果中的某個使用者、\[動作\] 和 \[指派原則\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果想將同一個個別使用者常設聊天原則套用至多位使用者，請在搜尋結果中選取多位使用者，然後按一下 [執行]，再按一下 [指派原則]。</td>
    </tr>
    </tbody>
    </table>


7.  在 \[指派原則\] 的 \[常設聊天原則\] 下，執行下列其中一項作業：
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>由於 [指派原則] 對話方塊可以設定多個原則，因此對話方塊中的每個原則預設都是選取 [&lt;維持不變&gt;]。不變更此設定，即可繼續沿用先前指派給使用者的原則。</td>
    </tr>
    </tbody>
    </table>
    
      - 選取 \[\<自動\>\] 可讓 Lync Server 2013 自動選擇全域層級原則或網站層級原則 (如果有定義的話)。
    
      - 按一下您之前在 \[常設聊天原則\] 頁面所定義個別使用者封存原則的名稱。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>為了協助您判斷應指派哪個原則，在按下原則名稱後，按一下 [檢視] 可以檢視該原則所定義的使用者權限。</td>
        </tr>
        </tbody>
        </table>


8.  完成時，請按一下 \[確定\]。

## 使用 Lync Server PowerShell Cmdlet 指派個別使用者常設聊天原則

個別使用者常設聊天原則也可透過 Lync Server PowerShell 與 Grant-CsPersistentChatPolicy Cmdlet 指派。此 Cmdlet 可從 Lync Server 2013 管理命令介面或是 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 將個別使用者常設聊天原則指派到單一使用者

  - 下列命令可將個別使用者常設聊天原則 RedmondPersistentChatPolicy 指派到使用者 Ken Myer。
    
        Grant-CsPersistentChatPolicy -Identity "Ken Myer" -PolicyName "RedmondPersistentChatPolicy"

## 將個別使用者常設聊天原則指派到多位使用者

  - 此命令可將個別使用者常設聊天原則 RedmondUsersPersistentChatPolicy 指派到 IT 部門的所有員工。如需詳細了解本命令所用的 LdapFilter 參數，請參閱＜[Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser)＞Cmdlet 的文件。
    
        Get-CsUser -LdapFilter "Department=IT" | Grant-CsPersistentChatPolicy -PolicyName "RedmondUsersPersistentChatPolicy"

## 解除指派個別使用者常設聊天原則

  - 下列命令可解除先前指派到 Ken Myer 的個別使用者常設聊天原則。解除指派個別使用者原則後，系統會使用全域原則或本機網站原則 (若有的話) 自動管理 Ken Myer。網站原則優於全域原則。
    
        Grant-CsPersistentChatPolicy -Identity "Ken Myer" -PolicyName $Null

如需詳細資訊，請參閱＜[Grant-CsPersistentChatPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsPersistentChatPolicy)＞Cmdlet 的說明主題。

## 請參閱

#### 概念

[在 Lync Server 2013 中建立常設聊天室的使用者原則](lync-server-2013-create-a-user-policy-for-persistent-chat.md)

