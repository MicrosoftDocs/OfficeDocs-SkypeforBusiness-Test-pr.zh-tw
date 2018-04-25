---
title: 指派每個使用者的 PIN 原則
TOCTitle: 指派每個使用者的 PIN 原則
ms:assetid: d8211c64-0b63-4193-a074-673da7d14287
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182594(v=OCS.15)
ms:contentKeyID: 49292469
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指派每個使用者的 PIN 原則

 

_**上次修改主題的時間：** 2013-02-22_

電話撥入式會議個人識別碼 (PIN) 原則是使用者帳戶的其中一項個別設定，您可以在 Lync Server 2013 控制台中加以設定。

您可以選擇部署一個或多個個別使用者 PIN 原則。您也可以只部署全域層級 PIN 原則或網站層級 PIN 原則。如果您選擇部署個別使用者原則，則必須明確指派原則給使用者、群組或連絡人物件。未指派特定網站層級或個別使用者原則時，有關將 PIN 用於電話撥入式會議的使用者權利及使用權限，會自動預設為全域層級 PIN 原則中所定義的使用者權利和使用權限。

在建立至少一個個別使用者 PIN 原則後，請使用本主題中的程序來指派原則，該原則會指定您希望伺服器施加在特定使用者所建立及使用之 PIN 上的限制。

如需建立個別使用者電話撥入式會議 PIN 原則的詳細資訊，請參閱[在 Lync Server 2013 中建立或修改使用者站台或群組的電話撥入式會議 PIN 設定](lync-server-2013-create-or-modify-dial-in-conferencing-pin-settings-for-a-site-or-group-of-users.md)。

## 若要指派個別使用者 PIN 原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[使用者\]**。

4.  使用下列其中一種方法，找到使用者：
    
      - 在 **\[搜尋使用者\]** 方塊中，輸入該使用者帳戶的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或線路統一資源識別項 (URI) 的全部或頭幾個字，然後按一下 **\[尋找\]**。
    
      - 如果有儲存的查詢，請按一下 **\[開啟查詢\]** 圖示、使用 **\[開啟\]** 對話方塊擷取查詢 (.usf 檔)，然後按一下 **\[尋找\]**。

5.  (選用) 指定其他搜尋條件，縮減結果：
    
    1.  按一下 **\[新增篩選\]**。
    
    2.  輸入使用者內容，您可以自行輸入或按一下下拉式清單的箭頭以選取內容。
    
    3.  在 **\[等於\]** 下拉式清單中，按一下運算子 (例如**等於**或**不等於**)。
    
    4.  依據您選取的使用者內容，輸入您要用來篩選搜尋結果的條件，您可以自行輸入或按一下下拉式清單的箭頭。
        
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

6.  依序按一下搜尋結果中的某個使用者、**\[動作\]** 和 **\[指派原則\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您要將相同的個別使用者 PIN 原則套用至多位使用者，請在搜尋結果中選取多位使用者，然後按一下 <strong>[執行]</strong>，再按一下 <strong>[指派原則]</strong>。</td>
    </tr>
    </tbody>
    </table>


7.  在 **\[指派原則\]** 中的 **\[PIN 原則\]** 下，執行下列其中一項：
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>由於 <strong>[指派原則]</strong> 對話方塊可以設定多個原則，因此對話方塊中的每個原則預設都是選取 <strong>[&lt;維持不變&gt;]</strong>。不變更此設定，即可繼續沿用先前指派給使用者的原則。</td>
    </tr>
    </tbody>
    </table>
    
      - 允許 Lync Server 2013 自動選擇全域層級原則，或是網站層級原則 (如果已定義)。
    
      - 按一下您之前在 **\[PIN 原則\]** 頁面上定義之個別使用者 PIN 原則的名稱。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>為了協助您判斷應指派哪個原則，在按下原則名稱後，按一下 <strong>[檢視]</strong> 可以檢視該原則所定義的使用者權限。</td>
        </tr>
        </tbody>
        </table>


8.  完成時，請按一下 **\[確定\]**。

## 使用 Lync Server 管理命令介面 Cmdlet 指派每一使用者的 PIN 原則

您可以使用 Lync Server 管理命令介面與 **Grant-CsPinPolicy** Cmdlet，來指派每一使用者 PIN 原則。您可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段來執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 將每一使用者 PIN 原則指派給單一使用者

  - 下列命令會將每一使用者 PIN 原則 RedmondPinPolicy 指派給使用者：Ken Myer。
    
        Grant-CsPinPolicy -Identity "Ken Myer" -PolicyName "RedmondPinPolicy"

## 將每一使用者 PIN 原則指派給多位使用者

  - 下列命令會將每一使用者 PIN 原則 RedmondUsersPinPolicy 指派給在 Redmond 城市工作的所有使用者。如需此命令中使用之 LdapFilter 參數的詳細資訊，請參閱＜[Get-CsUser](get-csuser.md)＞。
    
        Get-CsUser -LdapFilter "l=Redmond" | Grant-CsPinPolicy -PolicyName "RedmondUsersPinPolicy"

## 取消指派個別使用者 PIN 原則

  - 下列命令可取消指派先前指派給 Ken Myer 的任何每一使用者 PIN 原則。取消指派每一使用者原則之後，將會使用全域原則或其本機網站原則 (如果存在的話) 自動管理 Ken Myer。網站原則的優先順序高於全域原則。
    
        Grant-CsPinPolicy -Identity "Ken Myer" -PolicyName $Null

如需詳細資訊，請參閱＜[Grant-CsPinPolicy](grant-cspinpolicy.md)＞。

## 請參閱

#### 工作

[建立新 PIN 原則](lync-server-2013-create-a-new-pin-policy.md)  

#### 其他資源

[指派每位使用者的原則](lync-server-2013-assigning-per-user-policies.md)

