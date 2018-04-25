---
title: Lync Server 2013：建立或修改互動式工作流程
TOCTitle: 建立或修改互動式工作流程
ms:assetid: bc7bb1bc-bf6a-4636-ae93-c56fa22613fa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205213(v=OCS.15)
ms:contentKeyID: 49292134
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立或修改互動式工作流程

 

_**上次修改主題的時間：** 2013-09-11_

使用下列其中一個程序，可以建立或修改互動工作流程。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可使用 Lync Server 管理命令介面或回應群組設定工具來建立或修改互動工作流程。您可從 Lync Server 控制台存取回應群組設定工具，也可在網頁瀏覽器中輸入下列 URL，直接開啟網頁：<strong>https://</strong> <em>&lt;webPoolFqdn&gt;</em><strong>/RgsConfig</strong> 。</td>
</tr>
</tbody>
</table>


## 若要使用 回應群組設定工具 來建立或修改互動工作流程

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[回應群組\] ，然後按一下 \[工作流程\] 。

4.  在 \[工作流程\] 頁面上，按一下 \[建立或編輯工作流程\] 。

5.  在 \[選取服務\] 搜尋欄位中，輸入裝載您要建立或修改之工作流程的 **ApplicationServer** 服務的部分或完整名稱。在產生的服務清單中，按一下您想要的服務，然後按一下 \[確定\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>回應群組設定工具即會開啟。您可以在網頁瀏覽器中輸入下列 URL 來直接開啟回應群組設定工具：<strong>https://</strong><em>&lt;webPoolFqdn&gt;</em><strong>/RgsConfig</strong>。</td>
    </tr>
    </tbody>
    </table>


6.  執行下列其中一項作業：
    
      - 在 \[建立新的工作流程\] 的 \[互動\] 旁邊，按一下 \[建立\] 。
    
      - 在 \[管理現有工作流程\] 下，找到想要變更的工作流程，然後在 \[動作\] 下，按一下 \[編輯\] 。

7.  如果尚未準備好讓使用者開始撥號至工作流程，請清除 \[啟用工作流程\] 核取方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您即將建立受管理的工作流程，則必須選取 [啟用工作流程] 。在儲存作用中的受管理工作流程之後，您可予以修改和停用。</td>
    </tr>
    </tbody>
    </table>


8.  若要讓同盟使用者撥號給群組，請選取 \[針對同盟啟用\] 核取方塊。您也必須要有為同盟設定的 回應群組應用程式適用的外部存取原則。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>全域外部存取原則會套用到 回應群組應用程式。您可使用 Lync Server 控制台或使用 <strong>Set-CsExternalAccessPolicy</strong> Cmdlet 將 EnableOutsideAccess 參數設為 True，以設定回應群組同盟的全域原則。請注意，除非使用者已指派網站或使用者原則，否則全域原則設定會套用到所有使用者。因此，在變更回應群組的這個設定時，請確定同盟設定符合您組織的需求。如需關於原則如何套用到使用者的詳細資訊，請參閱 <a href="lync-server-2013-manage-external-access-policy-for-your-organization.md">在 Lync Server 2013 中管理外部使用存取原則</a>。如需同盟設定的詳細資訊，請參閱 Lync Server 管理命令介面 文件中的 <strong>Set-CsExternalAccessPolicy</strong>。</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>主控於 Lync Online 中的使用者無法撥電話給主控於內部部署中的回應群組。在混合式部署中，以及內部部署與 Lync Online 部署同盟的情況下，都有這個限制。</td>
    </tr>
    </tbody>
    </table>


9.  若要在通話期間隱藏代理人的身分識別，請選取 \[啟用代理人匿名\] 核取方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>雖然代理人或來電者可以在建立通話之後新增 IM 及視訊，但是匿名通話不能以立即訊息 (IM) 或視訊開始。匿名代理人也可以保留通話、轉接通話 (無條件轉接及諮詢轉接)，以及駐留及擷取通話。匿名通話不支援會議、應用程式共用和桌面共用、檔案傳輸、白板和資料共同作業，以及通話記錄。使用 Lync VDI 外掛程式的代理人可以匿名方式接聽來電，但無法以匿名方式撥出電話。</td>
    </tr>
    </tbody>
    </table>


10. 在 \[輸入要接聽電話的群組位址\] 下，輸入將接聽撥給工作流程之來電的主要 SIP 統一資源識別元 (URI) 位址。

11. 在 \[顯示名稱\] 中，輸入想要用戶端針對工作流程顯示的名稱 (例如，Sales IVR Response Group)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請不要在顯示名稱中包含 &quot;&lt;&quot; 或 &quot;&gt;&quot; 字元。下列是保留的顯示名稱，因此請不要使用它們：[RGS Presence Watcher] 或 [宣告服務]。</td>
    </tr>
    </tbody>
    </table>


12. 在 \[電話號碼\] 中，輸入回應群組的線路 URI (例如，+14255550165)。

13. 在 \[顯示號碼\] 中，輸入想要針對回應群組顯示的號碼 (例如，+1 (425) 555-0165)。

14. (選用) 在 \[描述\] 中，輸入要顯示在 Lync 的連絡人卡片的工作流程描述。

15. 如果這是受回應群組管理員管理的工作流程，請在 \[工作流程類型\] 中，選取 \[受管理\] 。執行下列動作以將 回應群組管理員指派給該工作流程：
    
    1.  為此工作流程輸入管理員的 SIP URI，然後按一下 \[新增\] 。
    
    2.  輸入要新增至此工作流程之其他管理員的 SIP URI，然後按一下 \[新增\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>指派為回應群組管理員的每位使用者，必須獲指派 CsResponseGroupManager 角色。如果未將此角色指派給使用者，他們將無法管理回應群組。</td>
    </tr>
    </tbody>
    </table>


16. 在 \[步驟 2 選取語言\] 下，按一下要用於語音辨識及文字轉換語音的語言。

17. 如果您想要設定歡迎訊息，請在 \[步驟 3 設定歡迎訊息\] 下選取 \[播放歡迎訊息\] 核取方塊，然後執行下列其中一個動作：
    
      - 若要以文字輸入為來電者轉換成語音的歡迎訊息，按一下 \[使用文字轉語音\] ，然後在文字方塊中輸入歡迎訊息。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>請不要在輸入的文字中包括 HTML 標籤。如果您包括 HTML 標籤，則會收到錯誤訊息。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要使用 Wave 或 Windows Media 音訊檔案錄音做為歡迎訊息，請按一下 \[選取錄音\] 。如果您想要上傳新的音訊檔案，請按一下 \[一筆記錄\] 連結。在新的瀏覽器視窗中按一下 \[瀏覽\] ，並選取想要使用的音訊檔案，然後按一下 \[開啟\] 。按一下 \[上傳\] 載入音訊檔案。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>所有使用者提供的音訊檔案都必須符合特定要求。如需所支援檔案格式的詳細資訊，請參閱＜ <a href="lync-server-2013-technical-requirements-for-response-group.md">Lync Server 2013 中回應群組的技術需求</a>＞。</td>
        </tr>
        </tbody>
        </table>


18. 在 \[步驟 4 指定您的上班時間\] 的 \[您的時區\] 方塊中，按一下工作流程的時區。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此時區即為工作流程的來電者和代理所在之時區，可用來計算開啟和關閉的時間。例如，如果工作流程設定為使用「北美東部時區」，而工作流程排定為早上 7:00 開啟，晚上 11:00 關閉，則開啟和關閉的時間就會分別假設為東部時區 7:00 和東部時區 11:00:00。(您必須使用 24 小時時間標記法輸入時間)。</td>
    </tr>
    </tbody>
    </table>


19. 執行下列其中一項，以選取想要使用的上班時間排程類型：
    
      - 若要使用預先定義的上班時間排程，請按一下 \[使用預設排程\] ，然後從下拉式清單中選取想要使用的排程。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>您至少先前必須已定義一個預設排程，才能選取此選項。 您可以使用 <strong>New-CSRgsHoursOfBusiness</strong> Cmdlet，來定義預設排程。如需詳細資訊，請參閱 <a href="lync-server-2013-optional-define-response-group-business-hours.md">(選用) 在 Lync Server 2013 中定義回應群組營業時間</a>。當您選取預設排程時，[天] 、[開啟] 和 [關閉] 都會自動填入回應群組可供使用的日期和小時。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要使用只套用至此工作流程的自訂排程，請按一下 \[使用自訂排程\] 。

20. 如果您是建立此工作流程的自訂排程，請按一下回應群組可用之一星期的哪幾天的核取方塊。

21. 如果您是建立自訂排程，請輸入回應群組可用時的 \[開啟\] 及 \[關閉\] 時間。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>[開啟] 及 [關閉] 時間必須使用 24 小時時間標記法。例如，如果您辦公室平日的辦公時間為 9 點到 5 點，而且會在中午用餐時間關閉，則會將上班時間指定為 [開啟] 9:00、[關閉] 12:00、[開啟] 13:00 以及 [關閉] 17:00。</td>
    </tr>
    </tbody>
    </table>


22. 如果您想要在辦公室關閉時播放訊息，請選取 \[在回應群組下班時播放訊息\] 核取方塊，然後執行下列其中一項，以指定要播放的訊息：
    
      - 若要以文字輸入為來電者轉換成語音的訊息，請按一下 \[使用文字轉語音\] ，然後在文字方塊中輸入訊息。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>請不要在輸入的文字中包括 HTML 標籤。如果您包括 HTML 標籤，則會收到錯誤訊息。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要使用音訊檔案錄音做為訊息，請按一下 \[選取錄音\] 。如果您想要上傳新的音訊檔案，請按一下 \[一筆記錄\] 連結。在新的瀏覽器視窗中按一下 \[瀏覽\] ，並選取想要使用的檔案，然後按一下 \[開啟\] 。按一下 \[上傳\] 載入音訊檔案。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>所有使用者提供的音訊檔案都必須符合特定要求。如需所支援檔案格式的詳細資訊，請參閱＜ <a href="lync-server-2013-technical-requirements-for-response-group.md">Lync Server 2013 中回應群組的技術需求</a>＞。</td>
        </tr>
        </tbody>
        </table>


23. 指定在播放訊息之後如何處理通話 (如果有設定訊息)：
    
      - 若要中斷來電，按一下 \[中斷通話\] 。
    
      - 若要將電話轉接至語音信箱，請按一下 \[轉接至語音信箱\]，然後輸入語音信箱位址。語音信箱位址的格式為：*\<username\>*@*\<domainname\>* (例如 bob@contoso.com)。
    
      - 若要將電話轉接至其他使用者，請按一下 \[轉接至 SIP URI\]，然後輸入使用者位址。使用者位址的格式為：*\<username\>*@*\<domainname\>*。
    
      - 若要將電話轉接至其他電話號碼，請按一下 \[轉接至電話號碼\]，然後輸入電話號碼。電話號碼的格式為：*\<number\>*@*\<domainname\>* (例如 +14255550121@contoso.com)，其中的網域名稱用於將來電者路由至正確的目的地。

24. 在 \[步驟 5 指定您的假日\] 下，按一下可定義回應群組沒上班之天數的一或多個假日集的核取方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您需要先定義假日及假日集，再設定工作流程。使用 <strong>New-CsRgsHoliday</strong> 及 <strong>New-CsRgsHolidaySet</strong> Cmdlet，可定義假日及假日集。如需詳細資訊，請參閱 <a href="lync-server-2013-optional-define-response-group-holiday-sets.md">(選用) 在 Lync Server 2013 中定義回應群組假日集</a>。</td>
    </tr>
    </tbody>
    </table>


25. 如果您想要在假日時播放訊息，請選取 \[在假日期間播放訊息\] 核取方塊，然後執行下列其中一項，以指定要播放的訊息：
    
      - 若要以文字輸入為來電者轉換成語音的訊息，請按一下 \[使用文字轉語音\] ，然後在文字方塊中輸入訊息。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>請不要在輸入的文字中包括 HTML 標籤。如果您包括 HTML 標籤，則會收到錯誤訊息。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要使用音訊檔案錄音做為訊息，請按一下 \[選取錄音\] 。如果您想要上傳新的音訊檔案，請按一下 \[一筆記錄\] 連結。在新的瀏覽器視窗中按一下 \[瀏覽\] ，並選取想要使用的檔案，然後按一下 \[開啟\] 。按一下 \[上傳\] 載入音訊檔案。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>所有使用者提供的音訊檔案都必須符合特定要求。如需所支援音訊檔案格式的詳細資訊，請參閱＜ <a href="lync-server-2013-technical-requirements-for-response-group.md">Lync Server 2013 中回應群組的技術需求</a>＞。</td>
        </tr>
        </tbody>
        </table>


26. 指定在播放訊息之後如何處理通話 (如果有設定訊息)：
    
      - 若要中斷來電，按一下 \[中斷通話\] 。
    
      - 若要將電話轉接至語音信箱，請按一下 \[轉接至語音信箱\]，然後輸入語音信箱位址。語音信箱位址的格式為：*\<username\>*@*\<domainname\>* (例如 bob@contoso.com)。
    
      - 若要將電話轉接至其他使用者，請按一下 \[轉接至 SIP URI\]，然後輸入使用者位址。使用者位址的格式為：*\<username\>*@*\<domainname\>*。
    
      - 若要將電話轉接至其他電話號碼，請按一下 \[轉接至電話號碼\]，然後輸入電話號碼。電話號碼的格式為：*\<number\>*@*\<domainname\>* (例如 +14255550121@contoso.com)，其中的網域名稱用於將來電者路由至正確的目的地。

27. 在 \[步驟 6 設定等候音樂\] 中，選擇您要來電者在等候代理時所聆聽的音樂，方法如下：
    
      - 若要使用預設的等候音樂錄音，按一下 \[使用預設\] 。
    
      - 若要使用音訊檔案錄音做為等候音樂，請按一下 \[選取音樂檔案\] 。如果您想要上傳新的音訊檔案，請按一下 \[音樂檔案\] 連結。在新的瀏覽器視窗中按一下 \[瀏覽\] ，並選取想要使用的檔案，然後按一下 \[開啟\] 。按一下 \[上傳\] 載入音訊檔案。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>所有使用者提供的音訊檔案都必須符合特定要求。如需所支援檔案格式的詳細資訊，請參閱＜ <a href="lync-server-2013-technical-requirements-for-response-group.md">Lync Server 2013 中回應群組的技術需求</a>＞。</td>
        </tr>
        </tbody>
        </table>


28. 在 \[步驟 7 設定互動語音回應\] 的 \[使用者將聽到下列文字或錄製的訊息\] 標題下，依下列方式指定要詢問來電者的問題：
    
      - 若要以文字格式輸入問題，按一下 \[使用文字轉語音\] ，然後在文字方塊中輸入問題。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>請不要在輸入的文字中包括 HTML 標籤。如果您包括 HTML 標籤，則會收到錯誤訊息。</td>
        </tr>
        </tbody>
        </table>
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>文字轉語音引擎會將 &quot;#&quot; 符號轉譯為「號碼」一詞。如果需要在提示中提及 # 鍵，則應該使用按鍵名稱，而非使用該符號。例如，「如果要與銷售人員交談，請按井字鍵」。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要使用包含問題的預錄音訊檔案，請按一下 \[選取錄音\] ，然後按一下 \[一筆記錄\] 連結以上傳檔案。在新的瀏覽器視窗中按一下 \[瀏覽\] ，並選取音訊檔案，然後按一下 \[開啟\] 。按一下 \[上傳\] 載入檔案，然後在文字方塊中選擇性地輸入問題 (如此可將問題和來電者的回應轉送給回應代理人)。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>所有使用者提供的音訊檔案都必須符合特定要求。如需所支援檔案格式的詳細資訊，請參閱＜ <a href="lync-server-2013-technical-requirements-for-response-group.md">Lync Server 2013 中回應群組的技術需求</a>＞。</td>
        </tr>
        </tbody>
        </table>


29. 在 \[回應 1\] 中，藉由下列動作指定問題的第一個可能答覆：
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請不要在任何語音回應中使用引號 (&quot;)。引號會導致 IVR 失敗。</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以選擇讓來電者使用語音及 (或) 英數鍵台輸入來進行答覆。</td>
    </tr>
    </tbody>
    </table>
    
      - 如果您想要讓來電者使用語音來回應，請在 \[輸入語音回應\] 中輸入答覆。
    
      - 如果您想要讓來電者按鍵台上的按鍵來回應，請在 \[數字\] 中按一下鍵台數字。

30. 指定是否要將來電者路由傳送到佇列或詢問另一個問題，如下所述：
    
      - 若要將來電者路由傳送到佇列，請按一下 \[傳送到佇列\] ，並在 \[選取佇列\] 中按一下想要使用的佇列。
    
      - 若要詢問另一個問題，請按一下 \[詢問另一個問題\] ，然後按一下 \[使用文字轉語音\] ，並輸入問題，或按一下 \[選取錄音\] 。使用本節中的回應分組，指定其他問題最多四個可能回應，以及用於每個回應的佇列。若要指定第三個或第四個可能的回應，請按一下 \[回應 3\] 核取方塊或 \[回應 4\] 核取方塊。

31. 重複步驟 28 及 29 指定可能的回應，以及針對每個回應採取的動作，以指定原始問題最多三個可能的答案。若要指定第三個或第四個可能的答案，請按一下 \[回應 3\] 核取方塊或 \[回應 4\] 核取方塊。

32. 按一下 \[部署\] 。

## 若要使用 Windows PowerShell 來建立或修改互動工作流程

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  擷取「回應群組」服務的服務名稱，並指派為變數。在命令列中執行：
    
        $serviceId="service:"+(Get-CSService | ?{$_.Applications -like "*RGS*"}).ServiceId;

4.  互動工作流程需要兩個以上佇列，以及兩個以上代理人群組。首先請建立代理人群組。 執行：
    
        $AGSupport = New-CsRgsAgentGroup -Parent $serviceId -Name "Technical Support" [-AgentAlertTime "20"] [-ParticipationPolicy "Informal"] [-RoutingMethod LongestIdle] [-AgentsByUri("sip:agent1@contoso.com", "sip:agent2@contoso.com")]
        $AGSales = New-CsRgsAgentGroup -Parent $serviceId -Name "Sales Team" [-AgentAlertTime "20"] [-ParticipationPolicy "Informal"] [-RoutingMethod LongestIdle] [-AgentsByUri("sip:bob@contoso.com", "sip:alice@contoso.com")]

5.  建立佇列。 執行：
    
        $QSupport = New-CsRgsQueue -Parent $ServiceId -Name "Contoso Support" -AgentGroupIDList($AG-Support.Identity)
        $QSales = New-CsRgsQueue -Parent $ServiceId -Name "Contoso Sales" -AgentGroupIDList($AG-Sales.Identity)

6.  建立第一個回應群組提示。執行：
    
        $SupportPrompt = New-CsRgsPrompt -TextToSpeechPrompt "Please be patient while we connect you with Contoso Technical Support."

7.  接著建立提示後執行的動作。執行：
    
        $SupportAction = New-CsRgsCallAction -Prompt $SupportPrompt -Action TransferToQueue -QueueID $QSupport.Identity

8.  建立第一個回應群組回答。執行：
    
        $SupportAnswer = New-CsRgsAnswer -Action $SupportAction [-DtmfResponse 1]

9.  現在建立第二個提示、呼叫動作以及回答。首先建立提示。執行：
    
        $SalesPrompt = New-CsRgsPrompt -TextToSpeechPrompt "Please hold while we connect you with Contoso Sales."

10. 建立第二個呼叫動作。執行：
    
        $SalesAction = New-CsRgsCallAction -Prompt $SalesPrompt -Action TransferToQueue -QueueID $QSales.Identity

11. 建立第二個回應群組回答。執行：
    
        $SalesAnswer = New-CsRgsAnswer -Action $SalesAction [-DtmfResponse 2]

12. 建立頂層提示。執行：
    
        $TopLevelPrompt = New-CsRgsPrompt -TextToSpeechPrompt "Thank you for calling Contoso. For Technical Support, press 1. For a Sales Representative, press 2."

13. 建立頂層問題。執行：
    
        $TopLevelQuestion = New-CsRgsQuestion -Prompt $TopLevelPrompt [-AnswerList ($SupportAnswer, $SalesAnswer)]

14. 現在建立工作流程。執行：
    
        $IVRAction = New-CsRgsCallAction -Action TransferToQuestion [-Question $Question]
        $IVRWorkflow = New-CsRgsWorkflow -Parent $ServiceId -Name "Contoso Helpdesk" [-Description "The Contoso Helpdesk line."] -PrimaryUri "sip:helpdesk@contoso.com" [-LineUri tel:+14255554321] [-DisplayNumber "+1 (425) 555-4321"] [-Active $true] [-Anonymous $true] [-DefaultAction $IVRAction] [-Managed $true] [-ManagersByURI ("sip:mindy@contoso.com", "sip:bob@contoso.com")]
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>所有已被指定為回應群組管理員的使用者，都必須獲指派 CsResponseGroupManager 角色。如果未指派此角色給使用者，他們就無法管理回應群組。</td>
    </tr>
    </tbody>
    </table>

