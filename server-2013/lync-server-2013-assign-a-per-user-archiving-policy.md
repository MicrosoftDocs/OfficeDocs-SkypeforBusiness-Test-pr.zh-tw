---
title: 指派每位使用者的封存原則
TOCTitle: 指派每位使用者的封存原則
ms:assetid: a12ca483-b235-460f-b3fe-130fb3087264
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182560(v=OCS.15)
ms:contentKeyID: 49291866
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指派每位使用者的封存原則

 

_**上次修改主題的時間：** 2013-02-22_

封存原則是您可以在 Lync Server 2013 控制台中設定之使用者帳戶的其中一個個別設定。

您可以選擇部署一個或多個個別使用者封存原則。您也可以只部署全域層級封存原則或網站層級封存原則。如果您選擇部署個別使用者原則，則必須明確指派原則給使用者、群組或連絡人物件。未指派任何特定網站層級或個別使用者原則時，封存需求會自動預設為全域層級會議原則中所定義的需求。

在建立至少一個個別使用者封存原則之後，請使用本主題中的程序來指派原則，該原則應適當地指定特定使用者的內部通訊、外部通訊或兩者是否將由伺服器封存。

如需建立個別使用者封存原則的詳細資訊，請參閱＜[建立封存原則以針對特定網站或使用者啟用或停用封存內部或外部通訊](lync-server-2013-creating-an-archiving-policy-to-enable-or-disable-archiving-of-internal-or-external-communications-for-specific-sites-or-users.md)＞。

## 若要指派個別使用者封存原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[使用者\]。

4.  使用下列其中一種方法，找到使用者：
    
      - 在 **\[搜尋使用者\]** 方塊中，輸入該使用者帳戶的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或線路統一資源識別項 (URI) 的全部或頭幾個字，然後按一下 **\[尋找\]**。
    
      - 如果有儲存的查詢，請按一下 **\[開啟查詢\]** 圖示、使用 **\[開啟\]** 對話方塊擷取查詢 (.usf 檔)，然後按一下 **\[尋找\]**。

5.  (選用) 指定其他搜尋條件，縮減結果：
    
    1.  按一下 **\[新增篩選\]**。
    
    2.  輸入使用者內容，您可以自行輸入或按一下下拉式清單的箭頭以選取內容。
    
    3.  在 **\[等於\]** 下拉式清單中，按一下運算子 (例如**等於**或**不等於**)。
    
    4.  依據您選取的使用者內容，輸入您要用來篩選搜尋結果的條件，您可以自行輸入或按一下下拉式清單的箭頭。
        
        > [!TIP]  
        > 若要將更多搜尋子句加入至查詢，請按一下 <strong>[新增篩選]</strong>。
    
    5.  按一下 **\[尋找\]**。

6.  依序按一下搜尋結果中的某個使用者、**\[動作\]** 和 **\[指派原則\]**。
    
    > [!TIP]
    > 如果您要將相同的個別使用者封存原則套用至多位使用者，請在搜尋結果中選取多位使用者，然後按一下 <strong>[執行]</strong>，再按一下 <strong>[指派原則]</strong>。


7.  在 **\[指派原則\]** 中的 **\[封存原則\]** 下，執行下列其中一項：
    
    > [!NOTE]  
    > 由於 <strong>[指派原則]</strong> 對話方塊可以設定多個原則，因此對話方塊中的每個原則預設都是選取 <strong>[&lt;維持不變&gt;]</strong>。不變更此設定，即可繼續沿用先前指派給使用者的原則。
    
    
      - 允許 Lync Server 2013 自動選擇全域層級原則，或是網站層級原則 (如果已定義)。
    
      - 按一下您之前在 **\[封存原則\]** 頁面上定義之個別使用者封存原則的名稱。
        
        > [!TIP]  
        > 為了協助您判斷應指派哪個原則，在按下原則名稱後，按一下 <strong>[檢視]</strong> 可以檢視該原則所定義的使用者權限。


8.  完成時，請按一下 \[確定\] 。

## 使用 Windows PowerShell Cmdlet 指派個別使用者封存原則

使用 Windows PowerShell 和 **Grant-CsArchivingPolicy** Cmdlet 也可以指派個別使用者封存原則。您可以從 Lync Server 2013 管理命令介面 或從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 將個別使用者封存原則指派給單一使用者

  - 下列命令會將個別使用者封存原則 RedmondArchivingPolicy 指派給使用者 Ken Myer。
    
        Grant-CsArchivingPolicy -Identity "Ken Myer" -PolicyName "RedmondArchivingPolicy"

## 將個別使用者封存原則指派給多個使用者

  - 此命令會將個別使用者封存原則 RedmondArchivingPolicy 指派給在登錄器集區 atl-cs-001.litwareinc.com 上具有帳戶的所有使用者。如需此命令中使用的 Filter 參數的詳細資訊，請參閱 [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser) Cmdlet 的文件。
    
        Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Grant-CsArchivingPolicy -PolicyName "RedmondArchivingPolicy"

## 指派取消個別使用者封存原則

  - 下列命令會取消指派先前指派給 Ken Myer 的所有個別使用者封存原則。取消指派個別使用者語音原則之後，系統會自動使用全域原則來管理 Ken Myer，或者如果有本機網站原則，則會使用本機網站原則來管理。網站原則的優先順序高於全域原則。
    
        Grant-CsarchivingPolicy -Identity "Ken Myer" -PolicyName $Null

如需詳細資訊，請參閱 [Grant-CsArchivingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsArchivingPolicy) Cmdlet 的說明主題。

## 請參閱

#### 工作

[建立封存原則以針對特定網站或使用者啟用或停用封存內部或外部通訊](lync-server-2013-creating-an-archiving-policy-to-enable-or-disable-archiving-of-internal-or-external-communications-for-specific-sites-or-users.md)  

#### 其他資源

[指派每位使用者的原則](lync-server-2013-assigning-per-user-policies.md)

