---
title: Lync Server 2013：建立或修改群組搜尋工作流程
TOCTitle: 建立或修改群組搜尋工作流程
ms:assetid: dcb9effb-5d12-4dee-80fc-ab9654222d5a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205321(v=OCS.15)
ms:contentKeyID: 49292533
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立或修改群組搜尋工作流程

 

_**上次修改主題的時間：** 2013-09-11_

使用下列其中一個程序，建立或修改群組搜尋工作流程。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可使用 Lync Server 管理命令介面或回應群組設定工具來建立和修改群組搜尋工作流程。您可從 Lync Server 控制台存取回應群組設定工具，也可在網頁瀏覽器中輸入下列 URL，直接開啟網頁：<strong>https://</strong><em>&lt;webPoolFqdn&gt;</em><strong>/RgsConfig</strong>。</td>
</tr>
</tbody>
</table>


## 使用 回應群組設定工具 建立或修改群組搜尋工作流程

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[回應群組\] ，然後按一下 \[工作流程\] 。

4.  在 \[工作流程\] 頁面上，按一下 \[建立或編輯工作流程\] 。

5.  在 \[選取服務\] 搜尋欄位中，輸入 **ApplicationServer** 服務的部分或全部名稱，該服務主控您要建立或變更的工作流程。在產生的服務清單中，按一下想要的服務，然後按一下 \[確定\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>回應群組設定工具即會開啟。您也可以在網頁瀏覽器中輸入下列 URL 來直接開啟回應群組設定工具：<strong>https://</strong><em>&lt;webPoolFqdn&gt;</em><strong>/RgsConfig</strong>。</td>
    </tr>
    </tbody>
    </table>


6.  執行下列其中一項作業：
    
      - 在 \[建立新的工作流程\] 下，按一下 \[群組搜尋\] 旁邊的 \[建立\]。
    
      - 在 \[管理現有工作流程\] 下，找到想要變更的工作流程，然後在 \[動作\] 下，按一下 \[編輯\] 。

7.  如果您準備好讓使用者開始撥號至工作流程，請選取 \[啟用工作流程\] 。
    
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
    <td>全域外部存取原則即適用於 回應群組應用程式。您可以使用 Lync Server 控制台或是使用 Set-CsExternalAccessPolicy Cmdlet，將 EnableOutsideAccess 參數設定為 True，來設定回應群組同盟的全域原則。請記住，除非另外指派網站或使用者原則，否則所有使用者都會套用全域原則設定。因此，在為回應群組變更此設定之前，請確定同盟設定符合您的組織需求。如需如何將原則套用至使用者的詳細資訊，請參閱＜ <a href="lync-server-2013-manage-external-access-policy-for-your-organization.md">在 Lync Server 2013 中管理外部使用存取原則</a>＞。如需同盟設定的詳細資訊，請參閱＜ <a href="set-csexternalaccesspolicy.md">Set-CsExternalAccessPolicy</a>＞。</td>
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
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>工作流程的主要 URI 是識別和參考工作流程的方式。您輸入的 SIP URI 會建立為 Active Directory 網域服務 中的連絡人物件。若要建立 URI，該物件在 Active Directory 中不得重複。</td>
    </tr>
    </tbody>
    </table>


11. 在 \[顯示名稱\] 中，輸入想要針對工作流程顯示的名稱 (例如，銷售 回應群組)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請不要在顯示名稱中包含 &quot;&lt;&quot; 或 &quot;&gt;&quot; 字元。下列是保留的顯示名稱，因此請不要使用它們：[RGS Presence Watcher] 或 [宣告服務] 。</td>
    </tr>
    </tbody>
    </table>


12. 在 \[電話號碼\] 下，輸入回應群組的線路 URI (例如，+14255550165)。

13. 在 \[顯示號碼\] 中，輸入想要針對回應群組顯示的號碼 (例如，+1 (425) 555-0165)。

14. (選用) 在 \[描述\] 中，輸入要在 Lync 用戶端的連絡人卡片顯示的工作流程描述。

15. 如果這是受回應群組管理員管理的工作流程，請在 \[工作流程類型\] 中，選取 \[受管理\] 。執行下列動作以將 回應群組管理員指派給該工作流程：
    
    1.  輸入此工作流程的管理員的 SIP URI，然後按一下 \[新增\] 。
    
    2.  輸入工作流程要新增的其他管理員的 SIP URI，然後按一下 \[新增\] 。
    
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


16. 在 \[步驟 2 選取語言\] 下，按一下要用於語音辨識及文字轉語音的語言。

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
    
      - 若要使用聲波 (.wav) 或 Windows Media 音訊 (.wma) 檔案錄音做為歡迎訊息，請按一下 \[選取錄音\] 。如果您想要上傳新的音訊檔案，請按一下 \[一筆記錄\] 連結。在新的瀏覽器視窗中按一下 \[瀏覽\] ，並選取想要使用的音訊檔案，然後按一下 \[開啟\] 。按一下 \[上傳\] 載入音訊檔案。
        
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


18. 在 \[步驟 4 指定您的上班時間\] 的 \[您的時區\] 中，按一下工作流程的時區。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此時區即為工作流程的來電者和代理所在之時區，可用來計算開啟和關閉的時間。例如，如果工作流程設定為使用「北美東部時區」，而工作流程排定為早上 7:00 開啟，晚上 11:00 關閉，則開啟和關閉的時間就會分別假設為東部時區 7:00 和東部時區 23:00。(您必須使用 24 小時時間標記法輸入時間)。</td>
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
        <td>您至少先前必須已定義一個預設排程，才能選取此選項。您可以使用 <strong>New-CSRgsHoursOfBusiness</strong> Cmdlet，來定義預設排程。如需詳細資訊，請參閱＜ <a href="lync-server-2013-optional-define-response-group-business-hours.md">(選用) 在 Lync Server 2013 中定義回應群組營業時間</a>＞。</td>
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
        <td>當您選取預設排程時，[日期] 、[開啟] 及 [關閉] 會自動填入回應群組可用的日期及時數。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要使用只套用至此工作流程的自訂排程，請按一下 \[使用自訂排程\] 。

20. 如果您是建立此工作流程的自訂排程，請按一下回應群組可用之一星期的哪幾天的核取方塊。

21. 如果您是建立自訂排程，請輸入回應群組可用時每個星期幾的 \[開啟\] 及 \[關閉\] 時間。
    
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
        <td>所有使用者提供的音訊檔案都必須符合特定要求。如需所支援音訊檔案格式的詳細資訊，請參閱＜ <a href="lync-server-2013-technical-requirements-for-response-group.md">Lync Server 2013 中回應群組的技術需求</a>＞。</td>
        </tr>
        </tbody>
        </table>


23. 指定在播放訊息之後如何處理通話 (如果有設定訊息)：
    
      - 若要中斷來電，按一下 \[中斷通話\] 。
    
      - 若要將電話轉接至語音信箱，請按一下 \[轉接至語音信箱\]，然後輸入語音信箱位址。語音信箱位址的格式為：*\<username\>*@*\<domainName\>* (例如 bob@contoso.com)。
    
      - 若要將電話轉接至其他使用者，請按一下 \[轉接至 SIP URI\]，然後輸入使用者位址。使用者位址的格式為：*\<username\>*@*\<domainName\>*。
    
      - 若要將電話轉接至其他電話號碼，請按一下 \[轉接至電話號碼\]，然後輸入電話號碼。電話號碼的格式為：*\<number\>*@*\<domainName\>* (例如 +14255550121@contoso.com)，其中的網域名稱用於將來電者路由至正確的目的地。

24. 在 \[步驟 5 指定您的假日\] 下，按一下可定義回應群組沒上班之天數的一或多個假日集的核取方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您需要先定義假日及假日集，再設定工作流程。使用 <strong>New-CsRgsHoliday</strong> 及 <strong>New-CsRgsHolidaySet</strong> Cmdlet，可定義假日及假日集。如需詳細資訊，請參閱＜ <a href="lync-server-2013-optional-define-response-group-holiday-sets.md">(選用) 在 Lync Server 2013 中定義回應群組假日集</a>＞。</td>
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
    
      - 若要將電話轉接至語音信箱，請按一下 \[轉接至語音信箱\]，然後輸入語音信箱位址。語音信箱位址的格式為：*\<username\>*@*\<domainName\>* (例如 bob@contoso.com)。
    
      - 若要將電話轉接至其他使用者，請按一下 \[轉接至 SIP URI\]，然後輸入使用者位址。使用者位址的格式為：*\<username\>*@*\<domainName\>*。
    
      - 若要將電話轉接至其他電話號碼，請按一下 \[轉接至電話號碼\]，然後輸入電話號碼。電話號碼的格式為：*\<number\>*@*\<domainName\>* (例如 +14255550121@contoso.com)，其中的網域名稱用於將來電者路由至正確的目的地。

27. 在 \[步驟 6 設定佇列\] 的 \[選取要接聽來電的佇列\] 下，選取想要保留來電者直到代理人有空的佇列。

28. 在 \[步驟 7 設定等候音樂\] 下，選擇您要來電者在等候代理人時所聆聽的音樂，方法如下：
    
      - 若要使用預設的等候音樂錄音，按一下 \[使用預設\] 。
    
      - 若要使用音訊檔案錄音做為等候音樂，請按一下 \[選取等候音樂\] 。如果您想要上傳新的音訊檔案，請按一下 \[音樂檔案\] 連結。在新的瀏覽器視窗中按一下 \[瀏覽\] ，並選取想要使用的檔案，然後按一下 \[開啟\] 。按一下 \[上傳\] 載入音訊檔案。
        
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


29. 按一下 \[部署\] 。

## 使用 Windows PowerShell 建立或修改群組搜尋工作流程

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  建立要在歡迎訊息播放的提示，然後以變數的形式儲存。在命令列中執行：
    
        $promptWM = New-CsRgsPrompt -TextToSpeechPrompt "<text for TTS prompt>"
    
    例如：
    
        $promptWM = New-CsRgsPrompt -TextToSpeechPrompt "Welcome to Contoso. Please wait for an available agent."
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要使用音訊檔案做為提示，請使用 <strong>Import-CsRgsAudioFile</strong> Cmdlet。如需詳細資訊，請參閱＜ <a href="import-csrgsaudiofile.md">Import-CsRgsAudioFile</a>＞。</td>
    </tr>
    </tbody>
    </table>


4.  取得來電將會導向的佇列或問題識別。在命令列中執行：
    
        $qid = (Get-CsRgsQueue -Name "Help Desk").Identity
    
    如需建立佇列的詳細資訊，請參閱＜ [New-CsRgsQueue](new-csrgsqueue.md)＞。

5.  定義於營業時間開啟工作流程時要採取的預設動作，然後以變數的形式儲存。在命令列中執行：
    
        $actionWM = New-CsRgsCallAction -Prompt <saved prompt from previous step> -Action <action to be taken> -QueueID $qid
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>對於群組搜尋工作流程，預設動作必須將電話導向佇列。這是作用中工作流程所需的必要參數。非作用中的工作流程則不需要該參數。</td>
    </tr>
    </tbody>
    </table>
    
    例如：
    
        $actionWM = New-CsRgsCallAction -Prompt $promptWM -Action TransferToQueue -QueueID $qid.Identity

6.  如果您想要定義營業時間與假日，您必須先加以建立，然後才能建立或修改工作流程。如需詳細資訊，請參閱＜ [(選用) 在 Lync Server 2013 中定義回應群組營業時間](lync-server-2013-optional-define-response-group-business-hours.md)＞及＜ [(選用) 在 Lync Server 2013 中定義回應群組假日集](lync-server-2013-optional-define-response-group-holiday-sets.md)＞。

7.  如果您想要針對下班時間或假日的來電提供提示，請使用 **New-CsRgsPrompt** Cmdlet 來定義提示，然後使用 **New-CsRgsCallAction** 定義要在提示後採取的動作。如需詳細資訊，請參閱＜ [New-CsRgsPrompt](new-csrgsprompt.md)＞及＜ [New-CsRgsCallAction](new-csrgscallaction.md)＞。

8.  擷取 Lync Server 回應群組服務的服務名稱，然後指派給一個變數。在命令中執行：
    
        $serviceId="service:"+(Get-CSService | ?{$_.Applications -like "*RGS*"}).ServiceId;

9.  建立或修改工作流程。若要建立工作流程，請使用 **New-CsRgsWorkflow**。若要修改工作流程，請使用 **Set-CsRgsWorkflow**。在命令列中輸入：
    
        $workflowHG = New-CsRgsWorkflow -Parent <service ID for the Response Group service> -Name "<hunt group name>" [-Description "<hunt group description>"] -PrimaryUri "<SIP address for the workflow>" [-LineUri "<Phone number for the workflow>"] [-DisplayNumber "<Phone number displayed in Lync>"] [-Active <$true | $false>] [-Anonymous <$true | $false>] [-DefaultAction <variable from preceding step>] [-EnabledForFederation <$true | $false>] [-Managed <$true | $false>] [-MangersByUri <SIP addresses for Response Group Managers who can manage the workflow>]
    
    例如：
    
        $workflowHG = New-CsRgsWorkflow -Parent $serviceID -Name "Human Resources" -Description "Human Resources workflow" -PrimaryUri "sip:humanresources@contoso.com" -LineUri "TEL:+14255551219" -DisplayNumber "555-1219" -Active $true -Anonymous $true -DefaultAction $actionWM -EnabledForFederation $false -Managed $true -ManagersByUri "sip:bob@contoso.com", "mindy@contoso.com"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>指定為工作流程管理員的所有使用者都必須獲指派 CsResponseGroupManager 角色。</td>
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
    <td>如需其他選用參數的詳細資訊，請參閱＜ <a href="new-csrgsworkflow.md">New-CsRgsWorkflow</a>＞及＜ <a href="set-csrgsworkflow.md">Set-CsRgsWorkflow</a>＞。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 工作

[(選用) 在 Lync Server 2013 中定義回應群組假日集](lync-server-2013-optional-define-response-group-holiday-sets.md)  

#### 概念

[(選用) 在 Lync Server 2013 中定義回應群組營業時間](lync-server-2013-optional-define-response-group-business-hours.md)  

#### 其他資源

[New-CsRgsWorkflow](new-csrgsworkflow.md)  
[Set-CsRgsWorkflow](set-csrgsworkflow.md)  
[New-CsRgsPrompt](new-csrgsprompt.md)  
[New-CsRgsCallAction](new-csrgscallaction.md)

