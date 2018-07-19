---
title: Lync Server 2013：建立或修改佇列
TOCTitle: 建立或修改佇列
ms:assetid: b9d6366a-839f-4651-a01d-9254546cadeb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205207(v=OCS.15)
ms:contentKeyID: 49292115
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立或修改佇列

 

_**上次修改主題的時間：** 2013-02-23_

使用下列其中一個程序，可建立或修改佇列。

## 若要使用 Lync Server 控制台來建立或修改佇列

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您是受管理工作流程的其中一位委派回應群組管理員，則可建立或修改回應群組佇列，並將它們指派給您管理的工作流程。</td>
    </tr>
    </tbody>
    </table>


2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[回應群組\] ，然後按一下 \[佇列\] 。

4.  在 \[佇列\] 頁面上，執行下列其中一項：
    
      - 若要建立新的佇列，請按一下 \[新增\] 。在 \[選取服務\] 的搜尋欄位中，輸入您要新增佇列的 **ApplicationServer** 服務的部分或完整名稱。在產生的服務清單中，按一下您想要的服務，然後按一下 \[確定\] 。
    
      - 若要修改現有佇列，請在搜尋欄位中輸入佇列的部分或完整名稱。在產生的佇列清單中，按一下想要的佇列，並按一下 \[編輯\] ，然後按一下 \[顯示詳細資料\] 。

5.  在 \[名稱\] 中輸入佇列的識別名稱。

6.  在 \[描述\] 中輸入佇列的描述。

7.  在 \[群組\] 中指定您要指派佇列的群組。執行下列其中一項作業：
    
      - 若要將群組新增至此佇列，請按一下 \[選取\] 。在 \[選取群組\] 搜尋欄位中，輸入您要指派至佇列的代理人群組部分或完整名稱，按一下您要的代理人群組，然後按一下 \[確定\] 。
    
      - 若要從佇列中移除群組，請在代理人群組清單中，按一下要移除的群組，然後按一下 \[移除\] 。
    
      - 若要變更代理人的搜尋順序，請在代理人群組清單中，按一下群組，然後按一下向上箭頭或向下箭頭。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>伺服器搜尋佇列中的有空代理人時，會使用群組順序。也就是說，會先搜尋清單中的第一個群組、接著搜尋清單中的第二個群組，以此類推。</td>
        </tr>
        </tbody>
        </table>


8.  若要指定來電者等候代理人接聽通話之前的最長保留期間，請選取 \[啟用佇列逾時\] 核取方塊，然後執行下列動作：
    
    1.  在 \[逾時期限 (秒)\] 中，指定來電者等候代理人接聽通話的最長秒數。
    
    2.  在 \[撥號動作\] 中，選取通話逾時時進行的動作 (如下所示)：
    
    <!-- end list -->
    
      - 若要在逾時之後中斷通話，請按一下 \[中斷連線\] 。
    
      - 若要將電話轉接至語音信箱，請按一下 \[轉接至語音信箱\]，然後在 \[SIP 位址\] 欄位中，以下列格式輸入語音信箱位址：sip:*\<username\>*@*\<domainname\>* (例如 sip:bob@contoso.com)。
    
      - 若要將電話轉接至其他電話號碼，請按一下 \[轉接至電話號碼\]，然後在 \[SIP 位址\] 欄位中，以下列格式輸入電話號碼：sip:*\<number\>*@*\<domainname\>* (例如 sip:+14255550121@contoso.com)。
    
      - 若要將電話轉接至其他使用者，請按一下 \[轉接至 SIP 位址\]，然後在 \[SIP 位址\] 欄位中，以下列格式輸入使用者的 URI：sip:*\<username\>*@*\<domainname\>*。
    
      - 若要將通話轉接至另一個佇列，請按一下 \[轉接至其他佇列\] ，然後瀏覽至想要使用的佇列。

9.  若要指定佇列可以保留的通話數目上限，請選取 \[啟用佇列溢位\] 核取方塊，然後執行下列動作：
    
    1.  在 \[通話數目上限\] 中，選取想要佇列保留的通話數目上限。
    
    2.  在 \[轉接來電\] 中，選取佇列已滿時要轉接的通話：\[最新通話\] 或 \[最早通話\] 。
    
    3.  在 \[撥號動作\] 中，選取符合溢位臨界值時進行的動作 (如下所示)：
    
    <!-- end list -->
    
      - 若要在逾時之後中斷通話，請按一下 \[中斷連線\] 。
    
      - 若要將電話轉接至語音信箱，請按一下 \[轉接至語音信箱\]，然後在 \[SIP 位址\] 欄位中，以下列格式輸入語音信箱位址：sip:*\<username\>*@*\<domainname\>* (例如 sip:bob@contoso.com)。
    
      - 若要將電話轉接至其他電話號碼，請按一下 \[轉接至電話號碼\]，然後在 \[SIP 位址\] 欄位中，以下列格式輸入電話號碼：sip:*\<number\>*@*\<domainname\>* (例如 sip:+14255550121@contoso.com)。
    
      - 若要將電話轉接至其他使用者，請按一下 \[轉接至 SIP 位址\]，然後在 \[SIP 位址\] 欄位中，以下列格式輸入使用者的 URI：sip:*\<username\>*@*\<domainname\>*。
    
      - 若要將通話轉接至另一個佇列，請按一下 \[轉接至其他佇列\] ，然後瀏覽至想要使用的佇列。

10. 按一下 \[認可\] 。

## 若要使用 Windows PowerShell來建立或修改佇列

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您是受管理工作流程的其中一位委派回應群組管理員，則可建立代理人群組和佇列，並將代理人群組指派給佇列。</td>
    </tr>
    </tbody>
    </table>


2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  建立達到佇列逾時臨界值時要播放的提示，並將其儲存至變數。在命令列中執行：
    
        $promptTO = New-CsRgsPrompt -TextToSpeechPrompt "<text for TTS prompt>"
    
    例如：
    
        "All agents are currently busy. Please call back later."
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要使用音訊檔案做為提示，請使用 <strong>Import-CsRgsAudioFile</strong> Cmdlet。如需詳細資訊，請參閱＜ <a href="https://docs.microsoft.com/powershell/module/skype/Import-CsRgsAudioFile">Import-CsRgsAudioFile</a>＞。</td>
    </tr>
    </tbody>
    </table>


4.  定義達到佇列逾時臨界值時要採取的動作，並將其儲存至變數。在命令列中執行：
    
        $actionTO = New-CsRgsCallAction -Prompt <saved prompt from previous step> -Action <action to be taken>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如需可行動作及其語法的詳細資訊，請參閱 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsCallAction">New-CsRgsCallAction</a>。</td>
    </tr>
    </tbody>
    </table>
    
    例如：
    
        $action = New-CsRgsCallAction -Prompt $promptTO -Action Terminate

5.  建立達到佇列溢位臨界值時要播放的提示，並將其儲存至變數。在命令列中執行：
    
        $promptOV = New-CsRgsPrompt -TextToSpeechPrompt "<text for TTS prompt>"
    
    例如：
    
        $promptOV = New-CsRgsPrompt -TextToSpeechPrompt "Too many calls are waiting. Please call back later."
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要使用音訊檔案做為提示，請使用 <strong>Import-CsRgsAudioFile</strong> Cmdlet。如需詳細資訊，請參閱＜ <a href="https://docs.microsoft.com/powershell/module/skype/Import-CsRgsAudioFile">Import-CsRgsAudioFile</a>＞。</td>
    </tr>
    </tbody>
    </table>


6.  定義達到佇列溢位臨界值時要採取的動作，並將其儲存至變數。在命令列中執行：
    
        $actionOV = New-CsRgsCallAction -Prompt <saved prompt from previous step> -Action <action to be taken>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如需可行動作及其語法的詳細資訊，請參閱 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsCallAction">New-CsRgsCallAction</a>。</td>
    </tr>
    </tbody>
    </table>
    
    例如：
    
        $action = New-CsRgsCallAction -Prompt $promptOV -Action Terminate

7.  擷取「回應群組」服務的服務名稱，並指派為變數。在命令列中執行：
    
        $serviceId="service:"+(Get-CSService | ?{$_.Applications -Like "*RGS*"}).ServiceId;

8.  取得要指派給佇列之代理人群組的身分識別。在命令列中執行：
    
        $agid = (Get-CsRgsAgentGroup -Name "Help Desk").Identity;
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如需建立代理人群組的詳細資訊，請參閱 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsAgentGroup">New-CsRgsAgentGroup</a>。</td>
    </tr>
    </tbody>
    </table>


9.  建立佇列。在命令列中執行：
    
        $q = New-CsRgsQueue -Parent <saved service ID from previous step> -Name "<name of queue>" [-Description "<description for queue>"] [-TimeoutThreshold <# seconds before call times out>] [-TimeoutAction <saved timeout action>] [-OverflowThreshold <# calls queue can hold>] [-OverflowCandidate <call to be acted on when overflow threshold met>] [-OverflowAction <saved overflow action>] [-AgentGroupIDList(<agent group identity>)];
    
    例如：
    
        $q = New-CsRgsQueue -Parent $serviceId -Name "Help Desk" -Description "Contoso Help Desk" -TimeoutThreshold 300 -TimeoutAction $actionTO -OverflowThreshold 10 -OverflowCandidate NewestCall -OverflowAction $actionOV -AgentGroupIDList($agid.Identity;

10. 確認佇列已建立。執行：
    
        Get-CsRgsQueue -Name "Help Desk"

## 請參閱

#### 其他資源

[New-CsRgsQueue](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsQueue)  
[Set-CsRgsQueue](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsRgsQueue)  
[New-CsRgsPrompt](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsPrompt)  
[New-CsRgsCallAction](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsCallAction)  
[Get-CsRgsQueue](https://docs.microsoft.com/powershell/module/skype/Get-CsRgsQueue)  
[Import-CsRgsAudioFile](https://docs.microsoft.com/powershell/module/skype/Import-CsRgsAudioFile)  
[Remove-CsRgsQueue](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsRgsQueue)

