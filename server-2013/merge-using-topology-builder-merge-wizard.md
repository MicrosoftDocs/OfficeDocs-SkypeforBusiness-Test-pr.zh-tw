---
title: 使用拓撲產生器合併精靈進行合併
TOCTitle: 使用拓撲產生器合併精靈進行合併
ms:assetid: c3f3c425-dab6-4dcd-bf0e-d7fde05f2ebf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205243(v=OCS.15)
ms:contentKeyID: 49292234
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用拓撲產生器合併精靈進行合併

 

_**上次修改主題的時間：** 2012-10-02_

1.  使用拓撲產生器下載現有部署。

2.  在 \[動作\] 功能表中，選取 \[合併 Office Communications Server 2007 R2\] 。

3.  按 **\[下一步\]** 。

4.  在 \[指定 Edge 安裝\] 中，按一下 \[新增\] 。
    
    ![合併拓撲精靈，\[指定 Edge 安裝\] 頁面](images/JJ205243.cdca609d-d4d5-47d9-9ff8-8b1daa4106e1(OCS.15).jpg "合併拓撲精靈，[指定 Edge 安裝] 頁面")  

5.  在 \[指定 Edge 類型\] 中，輸入 Edge Server 設定類型，然後按 \[下一步\] 。此範例使用 \[單一 Edge Server\] 選項。
    
    > [!IMPORTANT]  
    > [擴充的 Edge 部署] 不是支援的設定。[擴充的 Edge Server] 必須先轉換為 [單一 Edge Server] 或 [負載平衡合併的 Edge] Server。
    


6.  在 \[指定內部 Edge 設定\] 中，視需要輸入您 Edge 集區的內部 FQDN 與連接埠相關資訊，然後按 \[下一步\] 。
    
    ![\[指定內部 Edge 設定\] 對話方塊](images/JJ205243.dd664761-839c-4ac8-bd1a-5525589dfbb0(OCS.15).jpg "[指定內部 Edge 設定] 對話方塊")  

7.  在 \[指定外部 Edge\] 中，為您的 Edge Server 輸入 Web 會議 FQDN 資訊。
    
    > [!IMPORTANT]  
    > 在您按 [下一步] 之前，請先執行本程序的下一個步驟。請務必注意不要遺漏此步驟。
    


8.  如果您打算使用舊版 Office Communications Server 2007 R2 Edge Server 進行同盟，請勾選 \[此 Edge 集區是用於同盟和公用 IM 連線\] 核取方塊。如果您已部署多部 Edge Server，當中只有一部會啟用同盟功能。如果您並未勾選此方塊，而是決定稍後再啟用同盟，則您必須再次執行 \[拓撲產生器合併精靈\] 並發行拓撲。
    
    ![Edge Server 對話方塊，\[指定外部 Edge\] 頁面](images/JJ205243.32e97ce5-92f0-477e-8125-5d2ece237b13(OCS.15).jpg "Edge Server 對話方塊，[指定外部 Edge] 頁面")  

9.  在 \[指定下一個躍點\] 中，輸入您環境中下一個躍點位置的完整網域名稱 (FQDN)。按一下 \[完成\] 。
    
    ![Edge Server 對話方塊，\[指定下一個躍點\] 頁面](images/JJ205243.e734ee0d-f91c-4f3f-8ae6-248ecabcf678(OCS.15).jpg "Edge Server 對話方塊，[指定下一個躍點] 頁面")  

10. 在 \[指定 Edge 安裝\] 中，若您所有的 Office Communications Server 2007 R2 Edge Server 都已新增，請按 \[下一步\] 。若您還有其他 Office Communications Server 2007 R2 Edge Server 要新增，請重複此程序的步驟 4 到最後。

11. 在 \[指定內部 SIP 連接埠\] 中，選取預設設定 (亦即，您並未修改預設 SIP 連接埠)。若您不使用預設連接埠 5061，請視需要變更，然後按 \[下一步\] 。

12. 在 \[摘要\] 中按 \[下一步\] ，以開始合併拓撲。

13. 精靈頁面會驗證拓撲的合併是否成功。

14. 在 \[狀態\] 欄中，檢查其值是否為 \[成功\] ，然後按一下 \[完成\] 。

15. 在拓撲產生器的左窗格中，您應該會看見 **BackCompatSite** ，這指出您的 Office Communications Server 2007 R2 環境已與 Lync Server 2013 合併。
    
    ![顯示合併拓撲的拓撲產生器](images/JJ205243.62751c76-f018-4c6d-bb48-c61ef8974d31(OCS.15).jpg "顯示合併拓撲的拓撲產生器")  

16. 從 \[動作\] 功能表中，按一下 \[發行拓撲\] ，然後按 \[下一步\] 。

17. 當 \[發行精靈\] 完成之後，按一下 \[完成\] 。
    
    > [!NOTE]  
    > 請務必完成下一個主題： <a href="import-policies-and-settings.md">匯入原則與設定</a>，以確保舊版原則設定都已匯入至 Lync Server 2013。
    

