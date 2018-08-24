---
title: 在 Lync Server 2013 中執行非正式語音路由測試
TOCTitle: 在 Lync Server 2013 中執行非正式語音路由測試
ms:assetid: ea0e6059-bf04-4b03-b6d3-8f5534b731e2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399049(v=OCS.15)
ms:contentKeyID: 49292684
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中執行非正式語音路由測試

 

_**上次修改主題的時間：** 2012-08-07_

您可以使用 **\[建立語音路由測試案例資訊\]** 對話方塊先執行非正式的測試，再建立實際測試案例。如果您對於測試結果感到滿意，可以選擇將結果儲存為正式測試案例。

## 執行非正式語音路由測試

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 \[語音路由\] 和 \[測試語音路由\]。

4.  在 **\[測試語音路由\]** 頁面上，按一下 **\[建立語音路由測試案例資訊\]**。

5.  在 **\[撥號號碼\]** 欄位中，輸入要用於這項測試的電話號碼。這個號碼將會正規化，並且顯示於 **\[結果\]** 窗格的 **\[正規化的號碼\]** 欄位中。

6.  在 **\[撥號對應表\]** 清單中，選取要用於測試撥號號碼的撥號對應表。預設是 \[全域\] 撥號對應表。
    
    當您執行測試時，這個撥號對應表中第一項符合撥號號碼的正規化規則將會顯示於 **\[結果\]** 窗格的 **\[正規化規則\]** 欄位中。

7.  在 **\[語音原則\]** 清單中，選取要用於測試撥號號碼的語音原則。預設是全域語音原則。
    
    當您執行測試時，此語音原則中第一項相符的 PSTN 使用方式記錄將會顯示於 **\[結果\]** 窗格的 **\[第一個 PSTN 使用方式\]** 欄位中。另外，與此 PSTN 使用方式記錄相關聯的第一個相符的語音路由將會顯示於 **\[第一個路由\]** 欄位中。

8.  (選用) 如果您想要對照指派給特定使用者的語音原則測試撥號號碼，請選取 **\[從使用者填入\]** 核取方塊。
    
    1.  按一下 **\[瀏覽\]**，顯示 **\[選取企業語音使用者\]** 對話方塊。
    
    2.  按一下 **\[尋找\]**，顯示已啟用 Enterprise Voice 的使用者清單。
    
    3.  按兩下要使用其指派的語音原則進行這項測試的使用者名稱。現在 **\[原則\]** 欄位會填入指派給所選取使用者的語音原則。
    
    當您執行測試時，此語音原則中第一項相符的 公用交換電話網路 (PSTN) 使用方式記錄將會顯示於 \[結果\] 窗格的 \[第一個 PSTN 使用方式\] 欄位中。另外，與此 PSTN 使用方式記錄相關聯的第一個相符的語音路由將會顯示於 \[第一個路由\] 欄位中。

9.  按一下 **\[執行\]**，執行測試案例。結果會在對話方塊的右側面板中顯示。

10. (選用) 如果您想要將此測試組態儲存為正式測試案例，請按一下 **\[另存新檔\]**。
    
    1.  在 **\[儲存語音路由測試案例資訊\]** 對話方塊的 **\[名稱\]** 欄位中，輸入測試案例的唯一名稱。
        
        在 Enterprise Voice 部署中，此名稱在所有語音路由測試案例之間必須是唯一的。此名稱最多可以有 32 個字元，並可包含任何英數字元以及反斜線 (\\)、句點 (.) 或底線 (\_)。
    
    2.  請注意，\[儲存語音路由測試案例資訊\] 對話方塊上的其餘欄位都是唯讀的，其內容會從非正式測試組態*和*結果預先填入。請確認這是您要儲存的測試案例組態。
        
        > [!Note]  
		> 測試結果的值會用來預先填入 <strong>[儲存語音路由測試案例資訊]</strong> 對話方塊上的欄位，如下所述：
        > <ul>
        > <li><p><strong>[預期的轉譯]</strong> 會以 <strong>[正規化的號碼]</strong> 欄位中的值預先填入。</p></li>
        > <li><p><strong>[預期的路由]</strong> 會以 <strong>[第一個路由]</strong> 欄位中的值預先填入。</p></li>
        > <li><p><strong>[預期的 PSTN 使用方式記錄]</strong> 會以 <strong>[第一個 PSTN 使用方式]</strong> 欄位中的值預先填入。</p></li>
        > </ul>
        > 如果在測試回合期間找不到任何與這些值相符的項目，則 <strong>[儲存語音路由測試案例資訊]</strong> 對話方塊上對應的欄位會是空白的。
    
    3.  按一下 \[確定\] 儲存測試案例，或按一下 \[取消\] 返回 \[檢視語音路由測試案例資訊\] 對話方塊，進一步擴展測試後再將它儲存。

11. 依序按一下 **\[認可\]** 和 **\[全部認可\]**。
    
    > [!NOTE]  
    > 只要您建立語音路由測試案例，就必須執行 [全部認可] 命令發佈測試案例。如需詳細資訊，請參閱操作文件中的＜<a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中發佈擱置變更至語音路由設定</a>＞。
    


## 請參閱

#### 工作

[在 Lync Server 2013 中建立語音路由測試案例](lync-server-2013-create-a-voice-routing-test-case.md)  
[在 Lync Server 2013 中執行語音路由測試案例](lync-server-2013-run-voice-routing-test-cases.md)  
[在 Lync Server 2013 中匯出語音路由測試案例](lync-server-2013-export-voice-routing-test-cases.md)  
[在 Lync Server 2013 中改善語音路由測試案例](lync-server-2013-import-voice-routing-test-cases.md)  

#### 其他資源

[在 Lync Server 2013 中設定撥號對應表](lync-server-2013-configuring-dial-plans.md)  
[在 Lync Server 2013 中設定語音原則、PSTN 使用方式記錄和語音路由](lync-server-2013-configuring-voice-policies-pstn-usage-records-and-voice-routes.md)

