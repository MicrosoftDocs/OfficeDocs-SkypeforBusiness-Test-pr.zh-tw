---
title: 疑難排解 Lync Server 2013 中的 Lync VDI 外掛程式
TOCTitle: 疑難排解 Lync Server 2013 中的 Lync VDI 外掛程式
ms:assetid: 183c9449-b907-409c-b5ed-b02af3bd93ee
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204713(v=OCS.15)
ms:contentKeyID: 49290222
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 疑難排解 Lync Server 2013 中的 Lync VDI 外掛程式

 

_**上次修改主題的時間：** 2012-10-10_

## 疑難排解在精簡型用戶端上安裝 Lync VDI 外掛程式的問題

如果在精簡型用戶端上安裝 VDI 外掛程式時發生問題，請檢查下列各項：

  - 確定您在 TEMP 和 TMP 系統變數中指定的資料夾中有足夠的空間。

  - 確定已關閉防寫保護。請參閱裝置製造商的文件，以取得指示。

## 疑難排解配對問題

當 VDI 外掛程式配對失敗時，右下的配對圖示會顯示成紅色的 “X”，如下所示：

![顯示成功配對的 Lync VDI 圖示](images/JJ204713.303d618c-4bc8-41c4-8553-2475de0d395e(OCS.15).png "顯示成功配對的 Lync VDI 圖示")

以下是失敗的可能原因，以及您可以採取的更正動作。

  - **使用者在登入時輸入不正確的憑證。**
    
    使用者應登出 Lync，並以正確的憑證重新登入。配對對話方塊會重新出現，並顯示配對是否成功。

  - **有另一個遠端桌面用戶端執行個體正在執行中。**
    
    如果其於 Windows 中使用遠端桌面連線，則使用者應執行下列動作：
    
    1.  啟動工作管理員：按 **Alt+Ctrl+Delete** 鍵，然後按一下 \[啟動工作管理員\]。
    
    2.  按一下 \[程序\] 索引標籤，在清單中尋找名為 **mstsc.exe** 的所有程序。
    
    3.  將每個 **mstsc.exe** 程序醒目提示，然後按一下 \[結束處理程序\]。
    
    4.  啟動新的遠端桌面工作階段，並重試連線。

  - **必要檔案安裝不正確。**
    
    外掛程式安裝在本機電腦之後，下列檔案應存在於 C:\\Program Files\\Microsoft Office\\Office15 (或適當的磁碟機代號) 底下：
    
      - LyncVdiPlugin.dll
    
      - UcVdi.dll
    
    如果 VDI 配對有任何問題，請檢查並確定這些檔案存在於本機電腦上。

  - **Lync 用戶端正在本機電腦上執行。**
    
    若要使用 Lync VDI 外掛程式，Lync 用戶端絕不能在本機電腦上執行，否則配對將會失敗。最佳作法是，使用者不應將 Lync 用戶端安裝在本機電腦上。

