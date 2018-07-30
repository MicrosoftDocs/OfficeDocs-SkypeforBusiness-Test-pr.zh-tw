---
title: Lync Server 2013：修改撥號對應表
TOCTitle: 修改撥號對應表
ms:assetid: a91f02df-cf60-40cf-82fe-e0342c118b91
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412797(v=OCS.15)
ms:contentKeyID: 49291939
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中修改撥號對應表

 

_**上次修改主題的時間：** 2012-11-01_

若要修改現有的撥號對應表，請執行下列程序中的步驟，如果要建立新的撥號對應表，請參閱＜ [在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)＞。

## 若要修改撥號對應表

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[語音路由\]** 和 **\[撥號對應表\]** 。

4.  在 **\[撥號對應表\]** 頁面上，按兩下撥號對應表名稱。
    
    > [!NOTE]  
    > 建立撥號對應表時設定撥號對應表範圍和名稱。您無法加以變更。
    


5.  (選用) 在 **\[編輯撥號對應表\]** 中編輯 **\[簡單名稱\]** 欄位，該欄位會預先填入顯示在 **\[名稱\]** 欄位中的相同名稱，以指定反映撥號對應表套用到的網站、服務或使用者的更具描述性名稱。
    
    > [!IMPORTANT]  
    > <strong>[簡單名稱]</strong> 在 Lync Server 2013 部署內的所有撥號對應表之間必須是唯一的。此名稱不得超過 256 個 Unicode 字元，其中每個字元可以是字母或數字字元、連字號 (-)、句點 (.)、加號 (+) 或底線 (_)。<br />
    > <strong>[簡單名稱]</strong> 欄位中不允許使用空格。


6.  (選用) 在 **\[描述\]** 欄位中輸入有關撥號對應表的描述性資訊。

7.  (選用) 如果要使用此撥號對應表作為電話撥入式會議存取號碼的地區，請指定 **\[電話撥入式會議地區\]** 。如果不想將此撥號對應表用於電話撥入式會議存取號碼，請將此欄位保留為空。
    
    > [!NOTE]  
    > 需要使用電話撥入式會議地區，將電話撥入式會議存取號碼與一個或多個撥號對應表關聯。
    


8.  (選用) 在 **\[外部存取首碼\]** 欄位中，只有在使用者需要撥打一個或多個額外前置數來取得外部線路 (例如 9) 時才指定值。您可以輸入最多四個字元 (\#、\* 和 0-9) 的首碼值。
    
    > [!NOTE]  
    > 如果指定了外部存取首碼，則不需要建立新的正規化規則來容納首碼。
    


9.  關聯並設定撥號對應表的正規化規則：
    
      - 若要從 企業語音 部署中可用的所有正規化規則清單中選擇一個或多個規則，請按一下 **\[選取\]** 。在 **\[選取正規化規則\]** 對話方塊中，反白顯示要與撥號對應表關聯的規則，然後按一下 \[確定\] 。
    
      - 若要定義新的正規化規則並將其與撥號對應表關聯，請按一下 **\[新增\]** 。如需定義新規則的詳細資訊，請參閱 [在 Lync Server 2013 中定義正規化規則](lync-server-2013-defining-normalization-rules.md)。
    
      - 若要編輯已與撥號對應表關聯的正規化規則，請反白顯示該規則名稱並按一下 **\[顯示詳細資訊\]** 。如需編輯規則的詳細資訊，請參閱 [在 Lync Server 2013 中定義正規化規則](lync-server-2013-defining-normalization-rules.md)。
    
      - 若要複製現有正規化規則以用作定義新規則的起點，請反白顯示該規則名稱，然後依序按一下 **\[複製\]** 和 **\[貼上\]** 。如需編輯副本的詳細資訊，請參閱 [在 Lync Server 2013 中定義正規化規則](lync-server-2013-defining-normalization-rules.md)。
    
      - 若要從撥號對應表移除正規化規則，請反白顯示該規則名稱並按一下 **\[移除\]** 。
    
    > [!NOTE]  
    > 每個撥號對應表至少必須具有一個關聯的正規化規則。如需如何決定撥號對應表需要的所有正規化規則的詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-dial-plans-and-normalization-rules.md">Lync Server 2013 中的撥號對應表和正規化規則</a>＞。
    


10. 確認撥號對應表的正規化規則按照正確的順序排列。若要變更規則在清單中的位置，請反白規則名稱，然後按向上或向下箭頭。
    
    > [!IMPORTANT]  
    > Lync Server 會由上而下周遊正規化規則清單，並使用符合撥打號碼的第一個規則。如果設定撥號對應表，以便撥打的號碼可以符合多個正規化規則，請確定較嚴格的規則排在較不嚴格的規則上面。<br />
    > 預設的 <strong>Keep All</strong> 正規化規則 <strong>^(\d{11})$</strong> 符合任何 11 位數號碼。例如，如果新增符合以 1425 開頭的 11 位數號碼的正規化規則，請確定 <strong>Keep All</strong> 排在限制較高規則 <strong>^(1425\d{7})$</strong> 下面。


11. (選用) 輸入一個測試撥號對應表的號碼，然後按一下 **\[前往\]** 。測試結果將顯示在 **\[輸入測試號碼\]** 下。
    
    > [!NOTE]  
    > 您可以儲存尚未通過測試的撥號對應表，並於日後重新設定。如需詳細資訊，請參閱 <a href="lync-server-2013-test-voice-routing.md">在 Lync Server 2013 中測試語音路由</a>。
    


12. 按一下 \[確定\] 。

13. 在 \[撥號對應表\] 頁面上，依序按一下 \[認可\] 和 \[全部認可\] 。
    
    > [!NOTE]  
    > 建立或修改撥號對應表時，必須執行 [全部認可] 命令才能發佈設定變更。如需詳細資訊，請參閱作業文件中的＜ <a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中發佈擱置變更至語音路由設定</a>＞。
    


## 請參閱

#### 工作

[在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)  
[在 Lync Server 2013 中發佈擱置變更至語音路由設定](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### 其他資源

[在 Lync Server 2013 中定義正規化規則](lync-server-2013-defining-normalization-rules.md)

