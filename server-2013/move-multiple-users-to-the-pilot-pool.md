---
title: 將多個使用者移到試驗集區
TOCTitle: 將多個使用者移到試驗集區
ms:assetid: 90d0590c-922c-4933-b778-9dd850b59310
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205096(v=OCS.15)
ms:contentKeyID: 49291660
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將多個使用者移到試驗集區

 

_**上次修改主題的時間：** 2012-10-02_

您可以使用 Lync Server 2013 控制台或 Lync Server 2013 管理命令介面，將多位使用者從 Lync Server 2010 集區移至 Lync Server 2013 試驗集區。

## 使用 Lync Server 2013 控制台移動多位使用者

1.  開啟 Lync Server 的 \[控制台\] 。

2.  依序按一下 \[使用者\] 、\[搜尋\] 及 \[尋找\] 。

3.  選取兩位您要移至 Lync Server 2013 集區的使用者。在此範例中，我們將移動 Chen Yang 和 Claus Hansen 這兩位使用者。
    
    ![將使用者移至特定登錄器集區](images/JJ205096.70d510e1-8e6b-40a5-a80b-27cbc63fc337(OCS.15).jpg "將使用者移至特定登錄器集區")  

4.  從 \[動作\] 功能表，選取 \[將選取的使用者移至集區\] 。

5.  從下拉式清單中選取 Lync Server 2013 集區。

6.  按一下 \[動作\] ，然後按一下 \[將選取的使用者移至集區\] 。按一下 \[確定\]。
    
    ![移動使用者，\[目的地登錄器集區\] 對話方塊](images/JJ205401.8a375003-dc00-4541-b578-4d88f2010601(OCS.15).png "移動使用者，[目的地登錄器集區] 對話方塊")  

7.  檢查使用者的 \[登錄器集區\] 欄是否包含了 Lync Server 2013 集區，如果存在，即表示使用者移動成功。

## 使用 Lync Server 2013 管理命令介面 移動多個使用者

1.  開啟 Lync Server 2013 管理命令介面。

2.  在命令列中輸入下列命令，並將 **User1** 和 **User2** 取代為您要移動的特定使用者名稱，並將 **pool\_FQDN** 取代為目的地集區的名稱。在此範例中，我們將移動 Hao Chen 和 Katie Jordan 這兩位使用者。
    
        Get-CsUser -Filter {DisplayName -eq "User1" -or DisplayName - eq "User2"} | Move-CsUser -Target "pool_FQDN"
    
    ![PowerShell Get-CsUser Cmdlet 的範例](images/JJ205096.767ff9fc-755d-4a80-a710-5b1367aecbe0(OCS.15).jpg "PowerShell Get-CsUser Cmdlet 的範例")  

3.  在命令列中輸入下列命令
    
        Get-CsUser -Identity "User1"

4.  **登錄器集區** 身分識別目前應指向您在前一步驟指定為 **pool\_FQDN** 的集區。這個身分識別的存在可確認使用者已成功移動。重複執行步驟以確認已移除 **User2**。
    
    ![PowerShell Get-UsUser -Identity Cmdlet 的輸出](images/JJ205096.8ff04c67-37a0-4156-bfbc-28f9f7b137c8(OCS.15).jpg "PowerShell Get-UsUser -Identity Cmdlet 的輸出")  

## 使用 Lync Server 2013 管理命令介面同時移動所有使用者

在此範例中，已將所有使用者傳回 Lync Server 2010 集區 (pool01.contoso.net)。使用 Lync Server 2013 管理命令介面，我們會同時將所有使用者移至 Lync Server 2013 集區 (pool02.contoso.net)。

1.  開啟 **Lync Server 2013 管理命令介面**。

2.  在命令列輸入下列命令：
    
        Get-CsUser -OnLyncServer | Move-CsUser -Target "pool_FQDN"
    
    ![管理命令介面中的 PowerShell Cmdlet 與結果](images/JJ205096.1e57ccb1-9378-4dc7-82b7-dcaa63a285c6(OCS.15).png "管理命令介面中的 PowerShell Cmdlet 與結果")  

3.  接著，針對某一位試驗使用者執行 **Get-CsUser**。
    
        Get-CsUser -Identity "Hao Chen"

4.  每位使用者的「登錄器集區」身分識別現在會指向您在前一步驟中指定為「pool\_FQDN」的集區。這個身分識別的存在可確認使用者已成功移動。

5.  此外，我們可以在 Lync Server 2013 控制台中檢視使用者清單，並確認登錄器集區值現在指向 Lync Server 2013 集區。
    
    ![Lync Server 2013 控制台使用者清單](images/JJ205096.3f2e87a7-ec59-43c5-82cb-e770108bfb04(OCS.15).jpg "Lync Server 2013 控制台使用者清單")

