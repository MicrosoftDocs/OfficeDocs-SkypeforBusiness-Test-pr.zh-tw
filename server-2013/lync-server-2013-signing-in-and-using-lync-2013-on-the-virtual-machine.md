---
title: Lync Server 2013：在虛擬機器上登入和使用 Lync 2013
TOCTitle: 在虛擬機器上登入和使用 Lync 2013
ms:assetid: 6140fc19-5bef-4b58-9b0f-19112b5ecd00
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204948(v=OCS.15)
ms:contentKeyID: 49291086
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在虛擬機器上登入和使用 Lync 2013

 

_**上次修改主題的時間：** 2012-10-03_

啟用 VDI 外掛程式後，在使用者登入 Lync 2013 時將會發生下列步驟。

1.  使用者在虛擬機器上執行的 Lync 2013 用戶端中輸入認證。

2.  在 Lync 偵測到 VDI 外掛程式的可用性後， Lync 會提示使用者重新輸入認證。建議使用者在此對話方塊中選取 **\[儲存我的密碼\]** 核取方塊，這樣在後續的登入中就不需要輸入認證。

3.  Lync 開始與 VDI 外掛程式配對。在配對完成前，用戶端會在 Lync 狀態列中顯示兩個圖示。左下方的圖示表示沒有音訊裝置可用，右下方閃爍的圖示表示 VDI 配對在進行中，如下圖所示：
    
    ![顯示成功配對的 Lync VDI 圖示](images/JJ204713.303d618c-4bc8-41c4-8553-2475de0d395e(OCS.15).png "顯示成功配對的 Lync VDI 圖示")  

4.  VDI 配對成功後，圖示會變更為表示音訊裝置將用於通話，以及 VDI 配對成功：
    
    ![顯示成功的 Lync VDI 配對圖示](images/JJ204948.57be3387-a3e5-4949-831e-f5ff9fcc5598(OCS.15).png "顯示成功的 Lync VDI 配對圖示")  

5.  在 Lync 與 VDI 外掛程式配對後，使用者可以在連線到本機電腦的 Lync 相容裝置上看到自己的目前狀態。現在使用者就可以正常撥打及接聽通話。

