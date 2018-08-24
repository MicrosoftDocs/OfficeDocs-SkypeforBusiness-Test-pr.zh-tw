---
title: 指派每個使用者的行動性原則
TOCTitle: 指派每個使用者的行動性原則
ms:assetid: d8bf997f-4bc7-48d3-973b-323505f55e9d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721902(v=OCS.15)
ms:contentKeyID: 49890338
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指派每個使用者的行動性原則

 

_**上次修改主題的時間：** 2013-02-22_

行動性原則是使用者帳戶的其中一項個別設定，您可以在 Lync Server 控制台或 Lync Server 管理命令介面中加以設定。

## 在 Lync Server 控制台中指派每位使用者的行動性原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[使用者\]。

4.  使用下列其中一種方法，找到使用者：
    
      - 在 \[搜尋使用者\] 方塊中，輸入該使用者帳戶的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或線路統一資源識別項 (URI) 的全部或頭幾個字，然後按一下 \[尋找\]。
    
      - 如果有儲存的查詢，請按一下 \[開啟查詢\] 圖示、使用 \[開啟\] 對話方塊擷取查詢 (.usf 檔)，然後按一下 \[尋找\]。

5.  (選用) 指定其他搜尋條件，縮減結果：
    
    1.  按一下 \[新增篩選\]。
    
    2.  輸入使用者內容，您可以自行輸入或按一下下拉式清單的箭頭以選取內容。
    
    3.  在 \[等於\] 下拉式清單中，按一下運算子 (例如 \[等於\] 或 \[不等於\])。
    
    4.  依據您選取的使用者內容，輸入您要用來篩選搜尋結果的條件，您可以自行輸入或按一下下拉式清單的箭頭。
        
        > [!TIP]  
        > 若要將更多搜尋子句加入查詢，請按一下 [新增篩選]。
    
    5.  按一下 \[尋找\]。

6.  依序按一下搜尋結果中的某個使用者、\[動作\] 和 \[指派原則\]。
    
    > [!TIP]
    > 如果您想將同一個的每一使用者行動性原則套用至多位使用者，請在搜尋結果中選取多位使用者，然後依序按一下[動作] 和 [指派原則]。


7.  在 \[指派原則\] 中的 \[行動性原則\] 下，執行下列其中一個動作：
    
    > [!NOTE]  
    > 由於 [指派原則] 可以設定多個原則，因此對話方塊中的每個原則預設都是選取 [&lt;維持不變&gt;]。不變更此設定，即可繼續沿用先前指派給使用者的原則。
    
    
      - 選取 \[\<自動\>\] 可讓 Lync Server 2013 自動選擇全域層級原則或網站層級原則 (如果有定義的話)。
    
      - 按一下您之前在 \[行動性原則\] 頁面上所定義每一使用者行動性原則的名稱。
        
        > [!TIP]  
        > 為了協助您判斷應指派哪個原則，在按下原則名稱後，按一下 [檢視] 可以檢視該原則所定義的使用者權限。


8.  完成時，請按一下 \[確定\]。

## 使用 Lync Server 管理命令介面 Cmdlet 指派每一使用者的行動性原則

您可以使用 Lync Server 管理命令介面與 **Grant-CsMobilityPolicy** Cmdlet，來指派每一使用者行動性原則。您可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段來執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 將每一使用者行動性原則指派給單一使用者

  - 下列命令會將每一使用者行動性原則 RedmondMobilityPolicy 指派給使用者：Ken Myer。
    
        Grant-CsMobilityPolicy -Identity "Ken Myer" -PolicyName "RedmondMobilityPolicy"

## 將每一使用者行動性原則指派給多位使用者

  - 下列命令會將每一使用者行動性原則 RedmondMobilityPolicy 指派給目前獲指派 NorthAmericaMobilityPolicy 原則的所有使用者。如需此命令中使用之 Filter 參數的詳細資訊，請參閱＜[Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser)＞。
    
        Get-CsUser -Filter {MobilityPolicy -eq "NorthAmericaMobilityPolicy"} | Grant-CsMobilityPolicy -PolicyName "RedmondMobilityPolicy"

## 取消指派每一使用者行動性原則

  - 下列命令可取消指派先前指派給 Ken Myer 的任何每一使用者行動性原則。取消指派每一使用者原則之後，將會使用全域原則或其本機網站原則 (如果存在的話) 自動管理 Ken Myer。網站原則的優先順序高於全域原則。
    
        Grant-CsMobilityPolicy -Identity "Ken Myer" -PolicyName $Null

如需詳細資訊，請參閱＜[Grant-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsMobilityPolicy)＞。

## 請參閱

#### 工作

[在 Lync Server 2013 中設定行動原則](lync-server-2013-configuring-mobility-policy.md)

