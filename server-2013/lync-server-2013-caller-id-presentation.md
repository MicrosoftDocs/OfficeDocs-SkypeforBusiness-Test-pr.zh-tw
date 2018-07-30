---
title: Lync Server 2013：來電顯示呈現方式
TOCTitle: 來電顯示呈現方式
ms:assetid: 6a643961-a0a1-41d1-96ba-6c428a89d82e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204980(v=OCS.15)
ms:contentKeyID: 49291209
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的來電顯示呈現方式

 

_**上次修改主題的時間：** 2013-02-22_

使用 Lync Server 2010，受話方的電話號碼 (也就是所撥打的電話號碼) 可以從 E.164 格式轉譯為*trunk peer* (也就是相關聯的閘道、專用交換機 (PBX) 或 SIP 主幹) 所需的當地撥號格式。若要執行此操作，您必須定義一或多個轉譯規則，先轉譯要求 URI 後，再路由至主幹對等。

Lync Server 2013 採用此選項，可將來電者的電話號碼 (即來電者撥打電話時發話的電話號碼) 從 E.164 格式轉譯為主幹對等所需的本地撥號格式。例如，您可撰寫轉譯規則，來將撥號字串開頭的 +44 移除，並以 0144 來取代。

**使用 Lync Server 控制台設定來電者 ID**

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[語音路由\] ，再按一下 \[主幹組態\] 。

4.  在 **\[主幹組態\]** 頁面上，按兩下現有的主幹 (例如 **\[通用\]** 主幹)，顯示 **\[編輯主幹組態\]** 對話方塊。

5.  若要設定來電者 ID 呈現方式：
    
      - 若要從 企業語音 部署中可用的所有轉譯規則清單中選擇一或多個規則，請按一下 **\[選取\]** 。在 **\[來電號碼轉譯規則\]** 中，按一下您想要與主幹建立關聯的規則，然後按一下 **\[確定\]** 。
    
      - 若要定義新的轉譯規則並與主幹建立關聯，請按一下 \[新增\] 。如需關於定義新規則的詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中定義轉譯規則](lync-server-2013-defining-translation-rules.md)。
    
      - 若要編輯已與主幹相關聯的轉譯規則，請按一下規則名稱，然後再按一下 \[顯示詳細資料\] 。如需詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中定義轉譯規則](lync-server-2013-defining-translation-rules.md)。
    
      - 若要複製現有轉譯規則以便用來定義新規則，請按一下規則名稱，再依序按一下 \[複製\] 和 \[貼上\] 。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中定義轉譯規則](lync-server-2013-defining-translation-rules.md)＞。
    
      - 若要移除主幹中的轉譯規則，請反白選取規則名稱，然後再按一下 \[移除\] 。
    
    > [!WARNING]
    > 如果您已在關聯的主幹對等端上設定轉譯規則，請勿再將轉譯規則與主幹建立關聯，因為這兩個規則可能會產生衝突。

