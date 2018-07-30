---
title: 指派每個使用者的用戶端版本原則
TOCTitle: 指派每個使用者的用戶端版本原則
ms:assetid: f7e8ba2f-62dc-4e7d-8b63-682986f10240
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182607(v=OCS.15)
ms:contentKeyID: 49292855
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指派每個使用者的用戶端版本原則

 

_**上次修改主題的時間：** 2013-02-22_

用戶端版本原則是您可以在 Lync Server 控制台 中設定之使用者帳戶的其中一個個別設定。

您可以選擇部署一個或多個個別使用者用戶端版本原則。您也可以只部署全域層級用戶端版本原則，或是網站層級或集區層級用戶端版本原則。如果您選擇部署個別使用者原則，則必須明確指派原則給使用者、群組或連絡人物件。如果未指派特定網站層級、集區層級或個別使用者原則，可在 Lync Server 2013 中註冊的預設用戶端，是在全域層級用戶端版本原則中定義的用戶端。

至少建立一個個別使用者用戶端版本原則之後，請利用本主題中的程序指派一個原則，用於指定允許在 Lync Server 中註冊的用戶端版本。

如需建立個別使用者用戶端版本原則的詳細資訊，請參閱[指定可用來登入 Lync Server 2013 的用戶端應用程式](lync-server-2013-specifying-the-client-applications-that-can-be-used-to-log-on-to-lync-server-2013.md)。

## 若要指派個別使用者用戶端版本原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[使用者\]。

4.  使用下列其中一種方法，找到使用者：
    
      - 在 \[搜尋使用者\] 方塊中，輸入該使用者帳戶的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或線路統一資源識別項 (URI) 的全部或頭幾個字，然後按一下 \[尋找\]。
    
      - 如果有儲存的查詢，請按一下 \[開啟查詢\] 圖示、使用 \[開啟\] 對話方塊擷取查詢 (.usf 檔)，然後按一下 \[尋找\]。

5.  (選用) 指定其他搜尋條件，縮減結果：
    
    1.  按一下 \[新增篩選\]。
    
    2.  輸入使用者內容，您可以自行輸入或按一下下拉式清單的箭頭以選取內容。
    
    3.  在 \[等於\] 下拉式清單中，按一下運算子 (例如\[等於\]或 \[不等於\])。
    
    4.  依據您選取的使用者內容，輸入您要用來篩選搜尋結果的條件，您可以自行輸入或按一下下拉式清單的箭頭。
        
        > [!TIP]  
        > 若要將更多搜尋子句加入至查詢，請按一下 [新增篩選]。
    
    5.  按一下 \[尋找\]。

6.  依序按一下搜尋結果中的某個使用者、\[動作\] 和 \[指派原則\]。
    
    > [!TIP]
    > 如果您要將相同的個別使用者用戶端版本原則套用至多位使用者，請在搜尋結果中選取多位使用者，然後按一下 [執行]，再按一下 <strong>[指派原則]</strong>。


7.  在 \[指派原則\] 中的 \[用戶端版本原則\] 下，執行下列其中一項：
    
    > [!NOTE]  
    > 由於 [指派原則] 對話方塊可以設定多個原則，因此對話方塊中的每個原則預設都是選取 [&lt;維持不變&gt;]。不變更此設定，即可繼續沿用先前指派給使用者的原則。
    
    
      - 允許 Lync Server 自動選擇全域層級原則，或是 (如果有定義) 網站層級原則或集區層級原則。
    
      - 按一下您之前在 \[用戶端版本原則\] 頁面上定義之個別使用者用戶端版本原則的名稱。
        
        > [!TIP]  
        > 為了協助您判斷應指派哪個原則，在按下原則名稱後，按一下 [檢視] 可以檢視該原則所定義的使用者權限。


8.  完成時，請按一下 \[確定\]。

## 使用 Lync Server 管理命令介面 Cmdlet 指派個別使用者用戶端版本原則。

您可使用 Grant-CsClientVersionPolicy Cmdlet 指派每個使用者用戶端版本原則。您可從 Lync Server 2013 管理命令介面 或 Windows PowerShell 的 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。 的遠端工作階段執行此 Cmdlet。

## 指派每個使用者用戶端版本原則給單一使用者

  - 下列命令會將每個使用者用戶端版本原則 RedmondClientVersionPolicy 指派給使用者 Ken Myer。
    
        Grant-CsClientVersionPolicy -Identity "Ken Myer" -PolicyName "RedmondClientVersionPolicy"

## 指派每個使用者用戶端版本原則給多位使用者

  - 此命令會將每個使用者用戶端版本原則 RedmondClientVersionPolicy 指派給目前指派語音原則 RedmondVoicePolicy 的所有使用者。如需此命令中所用 Filter 參數的詳細資訊，請參閱 [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser) Cmdlet 的文件。
    
        Get-CsUser -Filter {VoicePolicy -eq "RedmondVoicePolicy"} | Grant-CsClientVersionPolicy -PolicyName "RedmondClientVersionPolicy"

## 取消指派每個使用者用戶端版本原則

  - 以下命令會取消指派任何先前指派給 Ken Myer 的每個使用者用戶端版本原則。取消指派 Ken Myer 的每個使用者原則後，會自動使用全域原則、Ken Myer 的本機網站原則 (如果有的話)，或指派至他登錄器的服務範圍原則來管理他。服務範圍原則會優於全域原則。
    
        Grant-CsClientVersionPolicy -Identity "Ken Myer" -PolicyName $Null

如需詳細資訊，請參閱 [Grant-CsClientVersionPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsClientVersionPolicy) Cmdlet 的說明主題。

## 請參閱

#### 其他資源

[指派每位使用者的原則](lync-server-2013-assigning-per-user-policies.md)  
[在 Lync Server 2013 中管理裝置、電話及用戶端應用程式](lync-server-2013-managing-devices-phones-and-client-applications.md)

