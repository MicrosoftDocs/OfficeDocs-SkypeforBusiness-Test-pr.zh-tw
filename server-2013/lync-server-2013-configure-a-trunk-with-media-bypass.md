---
title: Lync Server 2013：設定含媒體旁路的主幹
TOCTitle: 設定含媒體旁路的主幹
ms:assetid: 99d729ea-5a4c-4ff2-a4a3-93a24368da6d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398792(v=OCS.15)
ms:contentKeyID: 49291781
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定含媒體旁路的主幹

 

_**上次修改主題的時間：** 2014-02-07_

遵循這些步驟以設定已啟用媒體旁路的主幹。若要設定停用媒體旁路的主幹，請參閱 [在 Lync Server 2013 中設定無媒體旁路的主幹](lync-server-2013-configure-a-trunk-without-media-bypass.md)。當您想要將部署的中繼伺服器數目降到最低時，媒體旁路會很實用。中繼伺服器集區通常會部署在中央網站，而且它會控制分支網站的閘道。啟用媒體旁路時，可讓來自分支網站用戶端的公用交換電話網路 (PSTN) 通話媒體直接流經這些網站的閘道。Lync Server 2013 撥出電話路由和 Enterprise Voice 原則必須正確設定，以便來自分支網站用戶端的 PSTN 通話可以路由傳送至適當的閘道。

強烈建議您啟用媒體旁路。但是，在啟用 SIP 主幹上的媒體旁路前，請確認您的合格 SIP 主幹提供者可支援媒體旁路且能成功達到此案例所要求的需求。更明確地說，提供者必須具有貴組織內部網路中之伺服器的 IP 位址。如果提供者無法支援此案例，媒體旁路將無法成功運作。如需詳細資訊，請參閱規劃文件中的 [在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>媒體旁路不會與每個公用交換電話網路 (PSTN) 閘道、IP-PBX 以及工作階段邊界控制器 (SBC) 相互溝通。Microsoft 已經與認證的合作夥伴測試了一組 PSTN 閘道和 SBC，並用 Cisco IP-PBX 完成部分測試。只有列在 Unified Communications Open Interoperability Program – Lync Server 中的產品和版本支援媒體旁路，網址為：<a href="http://go.microsoft.com/fwlink/?linkid=214406%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=214406&amp;clcid=0x404</a>。</td>
</tr>
</tbody>
</table>


下述的主幹組態群組了一組參數，這些參數會套用於被指派此主幹組態的主幹。特定的主幹組態可以全域套用 (套用於所有不具更明確之網站或集區組態的主幹)，或套用於網站或集區。集區層級的主幹組態用於將特定主幹組態套用於單一主幹。

## 若要設定具有媒體旁路的主幹

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[語音路由\] ，再按一下 \[主幹組態\] 。

4.  在 **\[主幹組態\]** 頁面上，使用下列其中一個方法設定主幹：
    
      - 按兩下現有主幹 (例如 **\[通用\]** 主幹)，顯示 **\[編輯主幹組態\]** 對話方塊。
    
      - 按一下 \[新增\] ，然後選取新主幹組態範圍：
        
          - **網站主幹 ：**從 \[選取網站\] 中選擇此主幹組態的網站，然後按一下 \[確定\] 。請注意，如果已為某個網站建立主幹組態，則該網站不會出現在 \[選取網站\] 。此主幹組態將套用於該網站中的所有主幹。
        
          - **集區主幹 ：**選擇此主幹組態要套用於的主幹名稱。此主幹可以是 拓撲產生器中定義之根主幹或任何其他主幹。從 \[選取服務\] 按一下 \[確定\] 。請注意，如果已為特定主幹建立主幹組態，則該主幹不會出現在 \[選取服務\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>一旦選取主幹組態的範圍後，就無法變更。<br />
    [名稱] 欄位會預先填入主幹組態所關聯之網站或服務的名稱，此名稱無法變更。</td>
    </tr>
    </tbody>
    </table>


5.  在 \[支援的最大早期對話\] 中指定值。這個值表示公用交換電話網路 (PSTN) 閘道、IP-PBX 或 ITSP 工作階段界限控制器 (SBC) 能針對傳送給中繼伺服器之 INVITE 所接收的分支回應數上限。預設值為 20。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在變更這個值之前，請洽詢服務提供者或設備製造商，以取得系統功能的詳細資料。</td>
    </tr>
    </tbody>
    </table>


6.  選取下列其中一個 **\[加密支援等級\]** 選項：
    
      - **必要 ：**必須使用安全即時傳輸通訊協定 (SRTP) 加密來保護中繼伺服器和閘道或專用交換機 (PBX) 之間的流量。
    
      - **選用 ：**如果服務提供者或設備製造商支援 SRTP，則使用 SRTP 加密。
    
      - **不支援 ：**服務提供者或設備製造商不支援 SRTP 加密，因此不使用 SRTP 加密。

7.  如果您想要讓媒體略過中繼伺服器以便讓主幹對等處理，請選取 **\[啟用媒體旁路\]** 核取方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要使媒體旁路順利運作，PSTN 閘道、IP-PBX 或 ITSP 工作階段界限控制器必須支援某些功能。如需詳細資訊，請參閱規劃文件中的 <a href="lync-server-2013-planning-for-media-bypass.md">在 Lync Server 2013 中規劃媒體旁路</a>。</td>
    </tr>
    </tbody>
    </table>


8.  如果有已知的媒體終端點 (例如 PSTN 閘道，因為媒體終端的 IP 與訊號終端相同)，則選取 **\[集中式媒體處理\]** 核取方塊。如果主幹沒有已知的媒體終端點，請清除此核取方塊。

9.  如果主幹對等端可支援接收來自 中繼伺服器的 SIP REFER 要求，請選取 \[啟用傳送轉接至閘道\] 核取方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果在選取 [啟用媒體旁路] 選項的情況下停用此選項，另需其他設定。如果主幹對等不支援接收中繼伺服器的 SIP REFER 要求且媒體旁路已啟用，您還必須執行 <strong>Set-CsTrunkConfiguration</strong> Cmdlet 停用作用中通話和保留通話的 RTCP，以支援適當的媒體旁路狀況。如需詳細資訊，請參閱 <a href="lync-server-2013-lync-server-management-shell.md">Lync Server 管理命令介面</a>文件。<br />
    或者，如果您要讓轉接的電話受到媒體旁路處理，且閘道並不支援 SIP REFER 要求，也可以選取 [啟用使用協力廠商通話控制進行轉接] 。</td>
    </tr>
    </tbody>
    </table>


10. (選用) 若要啟用主幹間路由，請將 PSTN 使用方式記錄關聯至並設定至此主幹組態。與此主幹組態相關聯的 PSTN 使用方式將會針對所有透過非源自 Lync 端點的主幹進來的來電進行套用。若要管理關聯至主幹組態的 PSTN 使用方式記錄，請使用下列其中一種方法：
    
      - 若要從 企業語音部署中可用之所有 PSTN 使用方式記錄的清單中選取一或多筆記錄，請按一下 \[選取\] 。反白選取想要與此主幹組態關聯的記錄，然後按一下 \[確定\] 。
    
      - 若要從此主幹組態中移除 PSTN 使用方式記錄，請選取記錄，然後按一下 \[移除\] 。
    
      - 若要定義新的 PSTN 使用方式記錄，並將它與此主幹組態關聯，請執行下列動作：
        
        1.  按一下 **\[新增\]** 。
        
        2.  在 \[名稱\] 欄位中，為記錄指定唯一的描述性名稱。
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>PSTN 使用方式記錄名稱在 企業語音部署內必須是唯一的。儲存記錄之後，就無法編輯 [名稱] 欄位。</td>
            </tr>
            </tbody>
            </table>
        
        3.  使用下列其中一種方法來關聯及設定此 PSTN 使用方式記錄的路由：
            
              - 若要在 企業語音部署內所有可用路由的清單中選取一或多個路由，請按一下 \[選取\] 。反白選取想要與此 PSTN 使用方式記錄關聯的路由，然後按一下 \[確定\] 。
            
              - 若要從 PSTN 使用方式記錄中移除路由，請選取路由，然後按一下 \[移除\] 。
            
              - 若要定義新的路由，並將它關聯至此 PSTN 使用方式記錄，請按一下 \[新增\] 。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中建立語音路由](lync-server-2013-create-a-voice-route.md)＞。
            
              - 若要編輯與此 PSTN 使用方式記錄關聯的路由，請選取路由，然後按一下 \[顯示詳細資料\] 。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中修改語音路由](lync-server-2013-modify-a-voice-route.md)＞。
        
        4.  按一下 \[確定\] 。
    
      - 若要編輯已與此主幹組態關聯的 PSTN 使用方式記錄，請執行下列動作：
        
        1.  選取想要編輯的 PSTN 使用方式記錄，然後按一下 \[顯示詳細資料\] 。
        
        2.  使用下列其中一種方法來關聯及設定此 PSTN 使用方式記錄的路由：
            
              - 若要在 企業語音部署內所有可用路由的清單中選取一或多個路由，請按一下 \[選取\] 。反白選取想要與此 PSTN 使用方式記錄關聯的路由，然後按一下 \[確定\] 。
            
              - 若要從 PSTN 使用方式記錄中移除路由，請選取路由，然後按一下 \[移除\] 。
            
              - 若要定義新的路由，並將它關聯至此 PSTN 使用方式記錄，請按一下 \[新增\] 。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中建立語音路由](lync-server-2013-create-a-voice-route.md)＞。
            
              - 若要編輯與此 PSTN 使用方式記錄關聯的路由，請選取路由，然後按一下 \[顯示詳細資料\] 。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中修改語音路由](lync-server-2013-modify-a-voice-route.md)＞。
        
        3.  按一下 \[確定\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>根據與所設定主幹關聯的 中繼伺服器對等端來關聯 PSTN 使用方式記錄相當重要。如果 中繼伺服器同儕節點是 PSTN 閘道或工作階段邊界控制器 (SBC)，強烈建議主幹組態不要關聯至會將路由導向至 PSTN 目的地或任何其他透過 Lync Server 連線之下游系統的 PSTN 使用方式記錄。</td>
    </tr>
    </tbody>
    </table>


11. 排列 PSTN 使用方式記錄，以獲得最佳效能。若要變更清單中某筆記錄的位置，請選取 PSTN 使用方式記錄，然後按一下向上或向下箭頭。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>PSTN 使用方式記錄在主幹組態中列出的順序相當重要。 Lync Server 會從上到下周遊清單。</td>
    </tr>
    </tbody>
    </table>


12. 若要針對位於網路位址轉譯 (NAT) 或防火牆後且位於支援栓的 SBC 之後的用戶端來啟用媒體旁路，應該選取 \[啟用 RTP 栓\] 。

13. 若要將來電記錄資訊傳送至 中繼伺服器的閘道對等點，應該選取 \[啟用轉送來電記錄\] 。

14. 若要允許 中繼伺服器端與閘道端 (還有相反方向) 之間轉送 P-Asserted-Identity (PAI) 來電建立者資訊，應該選取 \[啟用轉送 P-Asserted-Identity 資料\] 。

15. 若要啟用快速容錯移轉，應該選取 \[啟用外撥路由容錯移轉計時器\] 。與此主幹關聯的閘道可以在 10 秒內通知正在處理外撥通話。如果 中繼伺服器未收到此通知，則會重新路由至其他主幹。在會有延遲來耽擱回應時間或是閘道需要超過 10 秒鐘才能回應的網路上，應該停用快速容錯移轉。

16. (選用) 關聯並設定主幹的 \[撥打號碼轉譯規則\] 。這些轉譯規則會套用至外撥電話的撥打號碼
    
      - 若要從 企業語音部署內所有可用轉譯規則的清單中選擇一或多個規則，請按一下 \[選取\] 。在 \[選取轉譯規則\] 中按一下要與主幹關聯的規則，然後按一下 \[確定\] 。
    
      - 若要定義新的轉譯規則並與主幹建立關聯，請按一下 \[新增\] 。如需關於定義新規則的詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中定義轉譯規則](lync-server-2013-defining-translation-rules.md)。
    
      - 若要編輯已與主幹相關聯的轉譯規則，請按一下規則名稱，然後再按一下 \[顯示詳細資料\] 。如需詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中定義轉譯規則](lync-server-2013-defining-translation-rules.md)。
    
      - 若要複製現有轉譯規則以便用來定義新規則，請按一下規則名稱，再依序按一下 \[複製\] 和 \[貼上\] 。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中定義轉譯規則](lync-server-2013-defining-translation-rules.md)＞。
    
      - 若要移除主幹中的轉譯規則，請反白選取規則名稱，然後再按一下 \[移除\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您已在關聯的主幹對等端上設定轉譯規則，請勿再將轉譯規則與主幹建立關聯，因為這兩個規則可能會產生衝突。</td>
    </tr>
    </tbody>
    </table>


17. (選用) 關聯並設定主幹的 \[撥打號碼轉譯規則\] 。這些轉譯規則會套用至外撥電話中的撥打號碼。
    
      - 若要從 企業語音部署內所有可用轉譯規則的清單中選擇一或多個規則，請按一下 \[選取\] 。在 \[選取轉譯規則\] 中按一下要與主幹關聯的規則，然後按一下 \[確定\] 。
    
      - 若要定義新的轉譯規則並與主幹建立關聯，請按一下 \[新增\] 。如需關於定義新規則的詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中定義轉譯規則](lync-server-2013-defining-translation-rules.md)。
    
      - 若要編輯已與主幹相關聯的轉譯規則，請按一下規則名稱，然後再按一下 \[顯示詳細資料\] 。如需詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中定義轉譯規則](lync-server-2013-defining-translation-rules.md)。
    
      - 若要複製現有轉譯規則以便用來定義新規則，請按一下規則名稱，再依序按一下 \[複製\] 和 \[貼上\] 。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中定義轉譯規則](lync-server-2013-defining-translation-rules.md)＞。
    
      - 若要移除主幹中的轉譯規則，請反白選取規則名稱，然後再按一下 \[移除\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您已在關聯的主幹對等端上設定轉譯規則，請勿再將轉譯規則與主幹建立關聯，因為這兩個規則可能會產生衝突。</td>
    </tr>
    </tbody>
    </table>


18. 確定主幹的轉譯規則是以正確順序排列。若要變更規則在清單中的位置，請反白選取規則名稱，然後按向上或向下箭頭。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server 2013 會從上往下周遊轉譯規則清單，並使用第一個符合撥號號碼的規則。如果您設定的主幹會使撥號號碼符合不只一個轉譯規則，請務必將限制較多的規則排在限制較少的規則上方。例如，如果您包含的轉譯規則中有一個規則符合所有 11 位數號碼，另有一個轉譯規則僅符合開頭為 +1425 的 11 位數號碼，則請務必將符合所有 11 位數號碼的規則排在另一個限制較多規則的「下方」 。</td>
    </tr>
    </tbody>
    </table>


19. 完成主幹的設定時，請按一下 \[確定\] 。

20. 在 **\[主幹組態\]** 頁面上，按一下 **\[認可\]** ，再按一下 **\[全部認可\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您只要建立或修改了主幹組態，就必須執行 [全部認可] 命令來發行組態變更。如需詳細資訊，請參閱作業文件中的 <a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中發佈擱置變更至語音路由設定</a>。</td>
    </tr>
    </tbody>
    </table>


完成主幹的設定後，請選擇全域媒體旁路選項以繼續設定媒體旁路，如部署文件之＜ [Lync Server 2013 中的全域媒體旁路選項](lync-server-2013-global-media-bypass-options.md)＞所述。

## 請參閱

#### 工作

[在 Lync Server 2013 中設定無媒體旁路的主幹](lync-server-2013-configure-a-trunk-without-media-bypass.md)  

#### 概念

[在 Lync Server 2013 中設定媒體旁路](lync-server-2013-configure-media-bypass.md)  
[Lync Server 2013 中的全域媒體旁路選項](lync-server-2013-global-media-bypass-options.md)  

#### 其他資源

[在 Lync Server 2013 中定義轉譯規則](lync-server-2013-defining-translation-rules.md)

