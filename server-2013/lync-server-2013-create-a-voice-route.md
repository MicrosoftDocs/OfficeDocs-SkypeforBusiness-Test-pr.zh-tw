---
title: 在 Lync Server 2013 中建立語音路由
TOCTitle: 在 Lync Server 2013 中建立語音路由
ms:assetid: d189057d-cc9d-4622-9d10-f5385d703faf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398898(v=OCS.15)
ms:contentKeyID: 49292391
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立語音路由

 

_**上次修改主題的時間：** 2012-11-01_

下列程序說明如何使用 Lync Server 2013 控制台建立新的語音路由。若要編輯現有的路由，請參閱＜[在 Lync Server 2013 中修改語音路由](lync-server-2013-modify-a-voice-route.md)＞以了解程序。

## 使用 Lync Server 控制台建立語音路由

1.  以 RTCUniversalServerAdmins 群組成員或 **CsVoiceAdministrator**、**CsServerAdministrator** 或 **CsAdministrator** 系統管理角色成員的身分登入電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[語音路由\]**。

4.  按一下 \[路由\] 。

5.  按一下 **\[新增\]**，顯示 **\[新增語音路由\]** 對話方塊。

6.  在 \[名稱\] 欄位中，輸入語音路由的描述性名稱。

7.  (選用) 在 \[描述\] 中，輸入有關語音路由的其他描述性資訊。

8.  若要指定您要此路由採用的模式，可以使用 \[建置要比對的模式\] 工具產生規則運算式，或是手動撰寫規則運算式。
    
      - 若要使用 **\[建置要比對的模式\]** 工具產生規則運算式，請輸入下述的值。您可以指定兩種類型的模式比對：
        
          - **所要允許之號碼的開頭數字：**輸入此路由必須採用的首碼值 (必要時，包括前置 +)。例如，輸入 **+425**，然後按一下 \[新增\]。針對要納入路由中的每一個首碼值重覆此操作。
        
          - **例外狀況：**如果您要針對某個首碼值指定一個或多個例外狀況，則反白顯示首碼，然後按一下 \[例外狀況\]。針對您「不要」此路由採用的比對模式，輸入一個或多個值。例如，若要從路由中排除開頭為 +425237 的數字，則在 \[例外狀況\] 欄位中輸入 **+425237** 這個值，然後按一下 \[確定\]。
    
      - 若要手動定義比對模式，請按一下 \[建置要比對的模式\] 工具中的 \[編輯\]，然後輸入 .NET Framework 規則運算式，指定套用路由之目的地電話號碼的比對模式。如需如何撰寫規則運算式的詳細資訊，請參閱＜.NET Framework 規則運算式＞，網址為：[http://go.microsoft.com/fwlink/?linkid=140927\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=140927%26clcid=0x404)。

9.  如果您不想要對受話者顯示撥出電話的電話 ID，則選取 **\[隱藏本機號碼\]**。如果您選取此選項，則必須指定將在受話者的來電者 ID 畫面上顯示的 **\[其他本機號碼\]**。

10. 若要使一或多個主幹與語音路由產生關聯，則按一下 \[新增\]，然後從清單中選取主幹。
    
    > [!NOTE]  
    > 如果您的部署包含任何 Microsoft Office Communications Server 2007 R2 中繼伺服器，這些伺服器也會出現在清單中。
    


11. 若要使一或多項公用交換電話網路 (PSTN) 的使用方式與語音路由產生關聯，則按一下\[選取\]，然後從針對 Enterprise Voice 部署所定義的 PSTN 使用方式記錄清單中選擇一項記錄。
    
    > [!NOTE]  
    > 若要檢視每一項可用 PSTN 使用方式記錄的屬性，請參閱<a href="lync-server-2013-view-pstn-usage-records.md">在 Lync Server 2013 中檢視 PSTN 使用方式記錄</a>。<br />
    > 若要建立或編輯 PSTN 使用方式記錄，請參閱<a href="lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md">在 Lync Server 2013 中建立語音原則和設定 PSTN 使用方式記錄</a>或<a href="lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md">在 Lync Server 2013 中修改語音原則和設定 PSTN 使用方式記錄</a>。


12. 排列 PSTN 使用方式記錄，以獲得最佳效能。若要變更清單中某筆記錄的位置，請反白顯示記錄名稱，然後按一下向上或向下箭頭。
    
    > [!NOTE]  
    > 在語音原則中，列出 PSTN 使用方式記錄的順序很重要，但是對於語音路由而言，列出 PSTN 使用方式記錄的順序並不重要。不過，我們建議您依照使用頻率來組織清單。例如：RedmondLocal、RedmondLongDist、RedmondInternational 及 RedmondBackup (Lync Server 是從上到下周遊清單)。
    


13. (選用) 在 **\[輸入要測試的轉譯號碼\]** 欄位中輸入一個值，然後按一下 **\[執行\]**。測試結果會在欄位底下顯示。
    
    > [!NOTE]  
    > 您可以儲存尚未通過測試的語音路由，並於之後將它重新設定。如需詳細資訊，請參閱<a href="lync-server-2013-test-voice-routing.md">在 Lync Server 2013 中測試語音路由</a>。
    


14. 按一下 **\[確定\]** 以儲存語音路由。

> [!IMPORTANT]  
> 每當您建立語音路由時，必須執行 [全部認可] 命令來發佈設定變更。如需詳細資訊，請參閱＜<a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中發佈擱置變更至語音路由設定</a>＞。



## 請參閱

#### 工作

[在 Lync Server 2013 中修改語音路由](lync-server-2013-modify-a-voice-route.md)  
[在 Lync Server 2013 中檢視 PSTN 使用方式記錄](lync-server-2013-view-pstn-usage-records.md)  
[在 Lync Server 2013 中建立語音原則和設定 PSTN 使用方式記錄](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)  
[在 Lync Server 2013 中修改語音原則和設定 PSTN 使用方式記錄](lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md)  
[在 Lync Server 2013 中發佈擱置變更至語音路由設定](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### 其他資源

[在 Lync Server 2013 中測試語音路由](lync-server-2013-test-voice-routing.md)

