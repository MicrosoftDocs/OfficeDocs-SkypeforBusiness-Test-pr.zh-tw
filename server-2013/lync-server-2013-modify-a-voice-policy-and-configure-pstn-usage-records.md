---
title: 在 Lync Server 2013 中修改語音原則和設定 PSTN 使用方式記錄
TOCTitle: 在 Lync Server 2013 中修改語音原則和設定 PSTN 使用方式記錄
ms:assetid: 6c53aaf5-218b-4bd4-8cea-31bc9d53f1bd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398511(v=OCS.15)
ms:contentKeyID: 49291239
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中修改語音原則和設定 PSTN 使用方式記錄

 

_**上次修改主題的時間：** 2012-11-01_

如果您想要修改語音原則，請遵循下列步驟。如果您想要建立新的語音原則，請參閱＜[在 Lync Server 2013 中建立語音原則和設定 PSTN 使用方式記錄](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)＞中的程序。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果將使用者指派給沒有相關聯公用交換電話網路 (PSTN) 使用方式記錄的語音原則，則該使用者無法撥出電話。如需 Enterprise Voice 部署中所有可用 PSTN 使用方式記錄的清單，及檢視其屬性，請參閱＜<a href="lync-server-2013-view-pstn-usage-records.md">在 Lync Server 2013 中檢視 PSTN 使用方式記錄</a>＞。</td>
</tr>
</tbody>
</table>


## 若要修改語音原則

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[語音路由\]** 和 **\[語音原則\]**。

4.  在 **\[語音原則\]** 頁面上，按兩下語音原則名稱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>範圍和名稱在語音原則建立時就已設定。您無法加以變更。</td>
    </tr>
    </tbody>
    </table>


5.  (選用) 在 **\[編輯語音原則\]** 中，輸入語音原則的其他描述性資訊。

6.  選取或清除下列核取方塊以啟用或停用每個 **\[撥號功能\]**：
    
      - **\[語音信箱逸出\]** 可在設定為同時響鈴，且手機在關機、電池電力耗盡或在收訊範圍之外時，防止通話立即路由傳送至使用者的行動電話語音信箱系統。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>此功能僅可透過Lync Server 管理命令介面加以設定</td>
        </tr>
        </tbody>
        </table>
    
      - **\[來電轉接\]** 可讓使用者將來電轉接到其他電話和用戶端裝置。Lync Server 2013 針對來電轉接提供各式各樣的設定選項。例如，如果組織不想讓來電向外轉接到 PSTN，系統管理員可套用特殊語音原則以部署此限制。預設為啟用。
    
      - **\[委派\]** 可讓使用者指定其他使用者，來代表他們撥號和接聽電話。在 Lync Server 2013 中，代理人可以設定同時響鈴，以讓撥打至其經理的來電同時讓所有的代理人響鈴目標發出鈴聲。這樣可在回應撥至主管的通話時給予代理人更大的彈性。預設為啟用。
    
      - **\[通話轉接\]** 可讓使用者將通話轉接給其他使用者。預設為啟用。
    
      - **\[通話駐留\]** 可讓使用者將通話駐留成保留狀態，然後由不同電話或用戶端接聽通話。預設為停用。
    
      - **\[同時響鈴\]** 可讓來電在更多電話 (例如，行動電話) 或其他端點裝置上發出鈴聲。Lync Server 2013 針對同時響鈴提供各式各樣的設定選項。預設為啟用。
    
      - **\[小組通話\]** 可讓所定義小組的使用者接聽該小組其他成員的通話。預設為啟用。
    
      - **\[PSTN 重新路由\]** 可在 WAN 擁塞或無法使用時，將被指派此原則的使用者撥打給其他企業使用者的電話，以公用交換電話網路 (PSTN) 重新路由。預設為啟用。
    
      - **\[頻寬原則覆寫\]** 可讓系統管理員覆寫特定使用者的通話許可控制 (CAC) 原則決策。預設為停用。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>系統只會針對撥入給使用者的來電，而不會針對使用者撥出的電話覆寫此原則。工作階段建立之後，便可準確地記錄頻寬使用量。請謹慎使用此設定。</td>
        </tr>
        </tbody>
        </table>
    
      - **\[惡意通話追蹤\]** 可讓使用者使用用戶端 UI 來回報惡意通話 (如炸彈威脅)，此舉會在詳細通話記錄 (CDR) 中以旗標標記通話。預設為停用。

7.  若要為此語音原則來關聯及設定 PSTN 使用方式記錄，請執行下列任何一項動作：
    
      - 若要從您 Enterprise Voice 部署中所有可用的 PSTN 使用方式記錄清單中選擇一或多個記錄，請按一下 **\[選取\]**。反白顯示您想要與此語音原則關聯的記錄，然後按一下 **\[確定\]**。
    
      - 若要從此語音原則中移除 PSTN 使用方式記錄，請反白顯示記錄，然後按一下 **\[移除\]**。
    
      - 若要定義新的 PSTN 使用方式記錄，並將它與此語音原則關聯，請執行下列動作：
        
        1.  按一下 **\[新增\]**。
        
        2.  在 **\[名稱\]** 欄位中，輸入記錄的唯一描述性名稱。例如，您可能會想要針對 Redmond 的全職員工建立一個名為 **Redmond** 的 PSTN 使用方式記錄，並針對臨時員工建立另一個名為 **RedmondTemps** 的記錄。
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>在 Enterprise Voice 部署內，PSTN 使用方式記錄名稱必須是唯一的。儲存記錄之後，就無法編輯 <strong>[名稱]</strong> 欄位。</td>
            </tr>
            </tbody>
            </table>
        
        3.  使用下列任何一種方法來關聯及設定此 PSTN 使用方式記錄的路由：
            
              - 若要從您 Enterprise Voice 部署中所有可用的路由清單中選擇一或多個路由，請按一下 **\[選取\]**，反白顯示您想要與此 PSTN 使用方式記錄關聯的路由，然後按一下 **\[確定\]**。
            
              - 若要從 PSTN 使用方式記錄中移除路由，請反白顯示路由，然後按一下 **\[移除\]**。
            
              - 若要定義新的路由，並將它與此 PSTN 使用方式記錄關聯，請按一下 **\[新增\]**。如需詳細資訊，請參閱＜[在 Lync Server 2013 中建立語音路由](lync-server-2013-create-a-voice-route.md)＞。
            
              - 若要編輯已與此 PSTN 使用方式記錄關聯的路由，請反白顯示路由，然後按一下 **\[顯示詳細資料\]**。如需詳細資訊，請參閱＜[在 Lync Server 2013 中修改語音路由](lync-server-2013-modify-a-voice-route.md)＞。
        
        4.  按一下 **\[確定\]**。
    
      - 若要編輯已與此語音原則關聯的 PSTN 使用方式記錄，請執行下列動作：
        
        1.  反白顯示您想要編輯的 PSTN 使用方式記錄，然後按一下 **\[顯示詳細資料\]**。
        
        2.  使用下列任何一種方法來關聯及設定此 PSTN 使用方式記錄的路由：
            
              - 若要從您 Enterprise Voice 部署中所有可用的路由清單中選擇一或多個路由，請按一下 **\[選取\]**，反白顯示您想要與此 PSTN 使用方式記錄關聯的路由，然後按一下 **\[確定\]**。
            
              - 若要從此 PSTN 使用記錄移除路由，請反白顯示路由，然後按一下 **\[移除\]**。
            
              - 若要定義新路由，並建立其與此 PSTN 使用方式記錄的關聯，請按一下 **\[新增\]**。如需詳細資訊，請參閱＜[在 Lync Server 2013 中建立語音路由](lync-server-2013-create-a-voice-route.md)＞。
            
              - 若要編輯已與此PSTN 使用方式記錄關聯的路由，請反白顯示路由，然後按一下 **\[顯示詳細資料\]**。如需詳細資訊，請參閱＜[在 Lync Server 2013 中修改語音路由](lync-server-2013-modify-a-voice-route.md)＞。
        
        3.  按一下 **\[確定\]**。

8.  排列 PSTN 使用方式記錄，以獲得最佳效能。若要變更清單中某筆記錄的位置，請反白顯示記錄名稱，然後按一下向上或向下箭頭。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>PSTN 使用方式記錄列在語音原則中的順序十分重要。Lync Server 會從上到下周遊清單。建議您依使用頻率來組織清單，例如：RedmondLocal、RedmondLongDist、RedmondInternational 和 RedmondBackup。</td>
    </tr>
    </tbody>
    </table>


9.  若要針對此語音原則中的來電轉接和同時鈴響建立關聯並設定 PSTN 使用方式記錄，請執行下列其中一項作業：
    
      - 若要依據此語音原則針對來電轉接和同時響鈴使用相同的 PSTN 使用方式記錄，請從下拉式功能表中選取 **\[使用通話 PSTN 使用方式的路由\]** 選項。
    
      - 若要讓來電轉接和同時響鈴僅供內部 Lync 使用者使用，從下拉式功能表選取 **\[僅路由傳送至內部 Lync 使用者\]**。通話不會轉接至外部 PSTN 號碼。
    
      - 若要針對用於此語音原則之外的來電轉接和同時響鈴指定其他 PSTN 使用方式記錄，請從下拉式功能表中選取 **\[使用自訂 PSTN 使用方式的路由\]** 選項。此選項會特別針對來電轉接和同時響鈴顯示控制項，用來選取現有 PSTN 使用方式記錄或建立新的 PSTN 使用方式記錄。
        
          - 若要針對來電轉接和同時響鈴從所有可用的 PSTN 使用方式記錄清單中選擇一筆或多筆記錄，請按一下 **\[選取\]**。反白顯示想要與此來電轉接和同時鈴響原則關聯的記錄，然後按一下 **\[確定\]**。
        
          - 若要從此來電轉接和同時鈴響原則移除 PSTN 使用方式記錄，請反白顯示記錄，然後按一下 **\[移除\]**。
        
          - 若要定義新的 PSTN 使用方式記錄，並建立其與此來電轉接和同時鈴響的關聯，請執行下列動作：
            
            1.  按一下 **\[新增\]**。
            
            2.  在 **\[名稱\]** 欄位中，輸入記錄的唯一描述性名稱。
                
                <table>
                <thead>
                <tr class="header">
                <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
                </tr>
                </thead>
                <tbody>
                <tr class="odd">
                <td>PSTN 使用方式記錄名稱必須是 Enterprise Voice 部署內的唯一名稱。儲存記錄之後，就無法編輯 <strong>[名稱]</strong> 欄位。</td>
                </tr>
                </tbody>
                </table>
            
            3.  使用下列任一方法針對此 PSTN 使用方式記錄建立關聯及設定路由：
                
                  - 若要從 Enterprise Voice 部署中所有可用路由的清單中選擇一個或多個路由，請按一下 **\[選取\]**，並反白顯示想要與此 PSTN 使用方式記錄建立關聯的路由，然後按一下 **\[確定\]**。
                
                  - 若要從 PSTN 使用方式記錄中移除路由，請反白顯示路由，然後按一下 **\[移除\]**。
                
                  - 若要定義新路由，並建立其與此 PSTN 使用方式記錄的關聯，按一下 **\[新增\]**。如需詳細資訊，請參閱＜[在 Lync Server 2013 中建立語音路由](lync-server-2013-create-a-voice-route.md)＞。
                
                  - 若要編輯已經與此 PSTN 使用方式記錄建立關聯的路由，請反白顯示路由，然後按一下 **\[顯示詳細資料\]**。如需詳細資訊，請參閱＜[在 Lync Server 2013 中修改語音路由](lync-server-2013-modify-a-voice-route.md)＞。
            
            4.  按一下 **\[確定\]**。
        
          - 若要編輯已經與此語音原則建立關聯的 PSTN 使用方式記錄，請執行下列動作：
            
            1.  反白顯示希望編輯的 PSTN 使用方式記錄，然後按一下 **\[顯示詳細資料\]**。
            
            2.  使用下列任一方法，針對此 PSTN 使用方式記錄來建立關聯及設定路由：
                
                  - 若要從 Enterprise Voice 部署中所有可用路由的清單中選擇一個或多個路由，請按一下 **\[選取\]**，並反白顯示想要與此 PSTN 使用方式記錄關聯的路由，然後按一下 **\[確定\]**。
                
                  - 若要從此 PSTN 使用方式記錄中移除路由，請反白顯示路由，然後按一下 **\[移除\]**。
                
                  - 若要定義新的路由，並將它與此 PSTN 使用方式記錄關聯，請按一下 **\[新增\]**。如需詳細資訊，請參閱＜[在 Lync Server 2013 中建立語音路由](lync-server-2013-create-a-voice-route.md)＞。
                
                  - 若要編輯已與此 PSTN 使用方式記錄關聯的路由，請反白顯示路由，然後按一下 **\[顯示詳細資料\]**。如需詳細資訊，請參閱＜[在 Lync Server 2013 中修改語音路由](lync-server-2013-modify-a-voice-route.md)＞。
            
            3.  按一下 **\[確定\]**。

10. (選用) 輸入號碼以測試語音原則，然後按一下 **\[執行\]**。測試結果會顯示在 **\[要測試的轉譯號碼\]** 下方。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以儲存尚未通過測試的語音原則，稍後再加以重新設定。如需詳細資訊，請參閱＜<a href="lync-server-2013-test-voice-routing.md">在 Lync Server 2013 中測試語音路由</a>＞。</td>
    </tr>
    </tbody>
    </table>


11. 按一下 **\[確定\]**。

12. 在 **\[語音原則\]** 頁面上，依序按一下 **\[認可\]** 和 **\[全部認可\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>只要建立或修改語音原則，就必須執行 <strong>[全部認可]</strong> 命令來發行設定變更。如需詳細資訊，請參閱作業文件中的<a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中發佈擱置變更至語音路由設定</a>。</td>
    </tr>
    </tbody>
    </table>


13. (選用) \[語音信箱\] 逸出會偵測使用者的行動電話語音信箱是否立即接聽來電，並中斷與行動電話語音信箱的連線。這樣可讓來電繼續在使用者的其他端點上響鈴，讓使用者有機會接聽來電。如需語音信箱原則設定方式的詳細資訊，請參閱＜[在 Lync Server 2013 中設定語音信箱逸出功能](lync-server-2013-configuring-voice-mail-escape.md)＞。

## 請參閱

#### 工作

[在 Lync Server 2013 中建立語音原則和設定 PSTN 使用方式記錄](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)  
[在 Lync Server 2013 中檢視 PSTN 使用方式記錄](lync-server-2013-view-pstn-usage-records.md)  
[在 Lync Server 2013 中建立語音路由](lync-server-2013-create-a-voice-route.md)  
[在 Lync Server 2013 中修改語音路由](lync-server-2013-modify-a-voice-route.md)  
[在 Lync Server 2013 中發佈擱置變更至語音路由設定](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  
[在 Lync Server 2013 中設定語音信箱逸出功能](lync-server-2013-configuring-voice-mail-escape.md)  

#### 其他資源

[在 Lync Server 2013 中測試語音路由](lync-server-2013-test-voice-routing.md)

