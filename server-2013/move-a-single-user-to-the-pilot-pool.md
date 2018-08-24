---
title: 將單一使用者移到試驗集區
TOCTitle: 將單一使用者移到試驗集區
ms:assetid: e9de81a8-40dd-4446-81e7-a2b810eaea50
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205401(v=OCS.15)
ms:contentKeyID: 49292681
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將單一使用者移到試驗集區

 

_**上次修改主題的時間：** 2012-09-26_

您可使用 Lync Server 2013 控制台或 Lync Server 2013 管理命令介面，將使用者從 Lync Server 2010 集區移至 Lync Server 2013 試驗集區。在下列範例的登錄器集區欄位中， **pool01.contoso.net** 是 Lync Server 2010 集區，六名使用者將全數連線至此集區。請依照下列程式將使用者移至 Lync Server 2013 集區 (使用 Lync Server 2013 控制台與 Lync Server 管理命令介面)。

## 使用 Lync Server 2013 控制台移動使用者

**Lync Server 2013 Control Panel 的使用者清單**

![Lync Server 控制台，\[移動使用者\] 對話方塊](images/JJ205401.a2bce284-0392-4db3-9bb2-9f12699738e7(OCS.15).jpg "Lync Server 控制台，[移動使用者] 對話方塊")

1.  使用屬於 RTCUniversalServerAdmins 群組成員、CsAdministrator 成員或 CsUserAdministrator 系統管理角色的帳戶登入前端伺服器。

2.  開啟 \[Lync Server 控制台\]。

3.  依序按一下 \[使用者\]、\[搜尋\] 及 \[尋找\]。

4.  選取您要移至 Lync Server 2013 集區的使用者。在此範例中，我們將移動使用者 Sara Davis。

5.  在 \[動作\] 功能表上，選取 \[將選取的使用者移至集區\]。

6.  從下拉式清單中選取 Lync Server 2013 集區。

7.  按一下 \[動作\]，再按一下 \[將選取的使用者移至集區\]，然後按一下 \[確定\]。
    
    ![移動使用者，\[目的地登錄器集區\] 對話方塊](images/JJ205401.8a375003-dc00-4541-b578-4d88f2010601(OCS.15).png "移動使用者，[目的地登錄器集區] 對話方塊")  

8.  確認使用者的 \[登錄器集區\] 欄位現在是否含有 Lync Server 2013 集區，如果有的話，即表示該使用者已移動成功。

## 使用 Lync Server 2013 管理命令介面移動使用者

1.  開啟 Lync Server 管理命令介面。

2.  在命令列輸入下列命令：
    
        Move-CsUser -Identity "David Pelton" -Target "pool02.contoso.net"

3.  然後在命令列輸入下列命令：
    
        Get-CsUser -Identity "David Pelton"

4.  **RegistrarPool** 身分識別即指向 Lync Server 2013 集區。出現此身分識別代表使用者已成功移動。
    
    ![具有 Identity 篩選器之 Get-CsUser Cmdlet 的輸出](images/JJ205401.bc5d4672-8068-4475-b882-dbd305c801a9(OCS.15).jpg "具有 Identity 篩選器之 Get-CsUser Cmdlet 的輸出")  
    
    > [!NOTE]  
    > 如需 <strong>Get-CsUser</strong> Cmdlet 的相關詳細資訊，請執行：<strong>Get-Help Get-CsUser –Detailed</strong>
    

