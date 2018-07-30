---
title: Lync Server 2013：針對災害復原部署配對前端集區
TOCTitle: 針對災害復原部署配對前端集區
ms:assetid: 2f12467c-8b90-43e6-831b-a0b096427f17
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204773(v=OCS.15)
ms:contentKeyID: 49290474
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中針對災害復原部署配對前端集區

 

_**上次修改主題的時間：** 2013-02-21_

您可以使用 拓撲產生器，輕易地部署成對的 前端集區災害復原拓撲。

## 部署一對前端集區

1.  若為尚未定義的新集區，請使用 拓撲產生器建立集區。

2.  在 拓撲產生器中，以滑鼠右鍵按一下兩個集區中的其中一個，然後按一下 \[編輯內容\] 。

3.  按一下左窗格中的 \[恢復\] ，然後選取右窗格中的 \[關聯的備份集區\] 。

4.  在下方 \[關聯的備份集區\] 中，選取您要與此集區配對的集區。您僅能選取尚未與其他集區配對的現有集區。
    
    ![恢復對話方塊](images/JJ204773.36080581-db76-497d-bf9e-f02b39574d0e(OCS.15).png "恢復對話方塊")  

5.  選取 \[語音自動容錯移轉和容錯回復\] ，然後按一下 \[確定\] 。
    
    當您檢視關於此集區的詳細資訊時，相關聯的集區會立即顯示在 \[恢復\] 之下的右側窗格中。

6.  使用 拓撲產生器發佈拓撲。

7.  若尚未部署這兩個集區，請立即部署，以完成組態。您可在此程序中略過最後這兩個步驟。
    
    然而，若在您定義成對關聯之前，就已部署了集區，您就必須完成下列兩個最後步驟。

8.  在兩個集區中的每部前端伺服器上，執行下列項目：
    
        <system drive>\Program Files\Microsoft Lync Server 2013\Deployment\Bootstrapper.exe 
    
    這會設定使備份配對順利運作所需的其他服務。

9.  從 Lync Server 管理命令介面命令提示字元，執行下列命令：
    
        Start-CsWindowsService -Name LYNCBACKUP

10. 使用下列 Cmdlet，強制兩個集區的使用者及會議資料互相進行同步處理：
    
      ```
      Invoke-CsBackupServiceSync -PoolFqdn <Pool1 FQDN>
      ```    
      ```
      Invoke-CsBackupServiceSync -PoolFqdn <Pool2 FQDN>
      ```
    
    同步處理資料可能需要花費一些時間。您可以使用下列 Cmdlet 檢查狀態。確保雙向中的狀態處於穩定狀態。
    
      ```
      Get-CsBackupServiceStatus -PoolFqdn <Pool1 FQDN>
      ```    
      ```
      Get-CsBackupServiceStatus -PoolFqdn <Pool2 FQDN>
      ```

> [!NOTE]  
> [語音自動容錯移轉和容錯回復] 選項以及 拓撲產生器中的相關時間間隔僅會套用至 Lync Server 2010 中引入的語音恢復功能。選取此選項不表示會自動使用本文件中討論的集區容錯移轉。集區容錯移轉和容錯回復一律需要管理員以手動方式分別呼叫容錯移轉和容錯回復 Cmdlet。


