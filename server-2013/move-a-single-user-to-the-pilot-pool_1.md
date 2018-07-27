---
title: 將單一使用者移到試驗集區
TOCTitle: 將單一使用者移到試驗集區
ms:assetid: 80d5b365-f153-4c61-a148-f9e18ce6e027
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688109(v=OCS.15)
ms:contentKeyID: 49890142
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將單一使用者移到試驗集區

 

_**上次修改主題的時間：** 2012-09-28_

您可以使用 Lync Server 2013 控制台 或 Lync Server 2013 管理命令介面，將使用者從 Office Communications Server 2007 R2 集區移到 Lync Server 2013 試驗集區。在以下範例的 \[登錄器集區\] 欄中， **\<Office Communications Server\>** 是 Office Communications Server 2007 R2 集區，而且所有六個使用者都連線到這個集區。使用下列程式，可使用 Lync Server 2013 控制台 和 Lync Server 管理命令介面 將使用者移到 Lync Server 2013 集區。

![在 Lync Server 控制台中搜尋 OCS 使用者](images/JJ688109.d2008fd6-868b-4f26-84cf-57bb69e073d3(OCS.15).jpg "在 Lync Server 控制台中搜尋 OCS 使用者")

## 使用 Lync Server 2013 控制台移動使用者

1.  使用 RTCUniversalServerAdmins 群組的成員帳戶、CsAdministrator 成員帳戶或 CsUserAdministrator 系統管理角色的成員帳戶登入前端伺服器。

2.  開啟 Lync Server 控制台。

3.  按一下 \[使用者\] 。

4.  從 \[使用者搜尋\] 索引標籤，按一下 \[搜尋\] 按鈕。

5.  接著，按一下 \[新增篩選\] 。

6.  建立篩選，其中的 \[Office Communications Server 使用者\] 等於 \[True\] 。

7.  按一下 \[尋找\] 搜尋舊版 Office Communications Server 2007 R2 使用者。
    
    ![在 Lync Server 控制台中搜尋 OCS 使用者](images/JJ688109.09528349-7915-41e1-91b4-6ab5c12b1b38(OCS.15).jpg "在 Lync Server 控制台中搜尋 OCS 使用者")  

8.  選取您要移至 Lync Server 2013集區的使用者。在此範例中，我們將移動使用者 Sara Davis。

9.  在 \[執行\] 功能表上，選取 \[將選取的使用者移至集區\] 。

10. 從下拉式清單中選取 Lync Server 2013 集區。

11. 按一下 \[動作\] ，然後按一下 \[將選取的使用者移至集區\] 。按一下 \[確定\] 。
    
    ![在 \[移動使用者\] 對話方塊中設定目的地集區](images/JJ205401.8a375003-dc00-4541-b578-4d88f2010601(OCS.15).png "在 [移動使用者] 對話方塊中設定目的地集區")  

12. 檢查使用者的 \[登錄器集區\] 欄位是否包含 Lync Server 2013 集區，如其存在，即表示使用者移動成功。

## 使用 Lync Server 2013 管理命令介面 移動使用者

1.  開啟 Lync Server 管理命令介面。

2.  在命令列輸入下列命令：
    
        Move-CsLegacyUser -Identity "David Pelton" -Target "pool02.contoso.net"

3.  然後在命令列輸入下列命令：
    
        Get-CsUser -Identity "David Pelton"

4.  **RegistrarPool** 身分識別即指向 Lync Server 2013 集區。出現此身分識別代表使用者已成功移動。
    
    ![具有 Identity 篩選器之 Get-CsUser Cmdlet 的輸出](images/JJ205401.bc5d4672-8068-4475-b882-dbd305c801a9(OCS.15).jpg "具有 Identity 篩選器之 Get-CsUser Cmdlet 的輸出")  
    
    > [!NOTE]  
    > 有關 [Get-CsUser] Cmdlet 的詳細資訊，請執行：<strong>Get-Help Get-CsUser –Detailed</strong>
    

