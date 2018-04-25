---
title: New-CsRgsWorkflow
TOCTitle: New-CsRgsWorkflow
ms:assetid: 1a2ac5b7-cb1d-4a83-801f-f27671e71743
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398246(v=OCS.15)
ms:contentKeyID: 49290250
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsWorkflow

 

_**上次修改主題的時間：** 2015-03-09_

建立新的回應群組工作流程。工作流程可決定回應群組應用程式接聽電話時所要採取的動作。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRgsWorkflow -Name <String> -Parent <RgsIdentity> -PrimaryUri <Uri> [-Active <$true | $false>] [-Anonymous <$true | $false>] [-BusinessHoursID <RgsIdentity>] [-Confirm [<SwitchParameter>]] [-CustomMusicOnHoldFile <AudioFile>] [-DefaultAction <CallAction>] [-Description <String>] [-DisplayNumber <String>] [-EnabledForFederation <$true | $false>] [-Force <SwitchParameter>] [-HolidayAction <CallAction>] [-HolidaySetIDList <Collection>] [-InMemory <SwitchParameter>] [-Language <String>] [-LineUri <Uri>] [-Managed <$true | $false>] [-ManagersByUri <Collection>] [-NonBusinessHoursAction <CallAction>] [-TimeZone <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會在 ApplicationServer:atl-cs-001.litwareinc.com 服務上建立新的工作流程。此工作流程會被命名為 Help Desk，並指派以主要的 URI sip:helpdesk@litwareinc.com。

    New-CsRgsWorkflow -Parent service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk" -PrimaryUri "sip:helpdesk@litwareinc.com" 

## 範例 2

範例 2 所示的命令會建立新的工作流程提示與來電動作，並將這些新項目指派給新的回應群組工作流程。在第一個命令中，**New-CsRgsPrompt** Cmdlet 是用來建立文字轉換語音提示「Welcome to the help desk」。這個新的提示會儲存在名為 $prompt 的變數中。

第二個命令會使用 **Get-CsRgsQueue** Cmdlet 擷取名為 Help Desk 的現有回應群組佇列識別，傳回的識別會儲存在名為 $queue 的變數中。

命令 3 接著會建立新的來電動作 (儲存在名為 $callAction 的變數中)，此動作會參照新的提示 ($prompt) 與擷取的佇列 ($queue)。最後，範例中的最後一個命令會建立名稱為 Help Desk 的新工作流程。此命令會將 PrimaryUri 設為 sip:helpdesk@litwareinc.com，並將 DefaultAction 屬性的值設為在前幾個步驟中建立的來電動作。

    $prompt = New-CsRgsPrompt -TextToSpeechPrompt "Welcome to the help desk."
    $queue = (Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk").Identity
    $callAction = New-CsRgsCallAction -Prompt $prompt -Action TransferToQueue -QueueId $queue
    New-CsRgsWorkflow -Parent service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk" -PrimaryUri "sip:helpdesk@litwareinc.com" -DefaultAction $callAction

## 詳細描述

工作流程是回應群組應用程式中的關鍵元素。每個工作流程只會與一個電話號碼產生關聯，當有人撥打該號碼時，工作流程便會決定如何處理這通電話。例如，系統會將電話路由傳送至一系列的互動語音回應 (IVR) 問題，這些問題會提示來電者輸入額外的資訊 (「硬體支援請按 1。如需要軟體支援，請按 2。」) 或者，來電可能會被放在佇列中並保留來電者，直到代理可接聽來電。代理是否可接聽電話的狀態，也是由工作流程指定的：工作流程可用來設定營業時間 (一星期的哪幾天和哪些時段會有代理接聽電話) 與假日 (哪幾天沒有代理可接聽電話)。

使用 **New-CsRgsWorkflow** Cmdlet 可建立新的工作流程。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRgsWorkflow** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsWorkflow"}

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>指派給工作流程的唯一名稱。Parent 屬性和 Name 屬性的組合可讓您單獨識別工作流程，而不必參考工作流程的全域唯一識別碼 (GUID)。</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>主控新工作流程的服務。例如：-Parent &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>PrimaryUri</em></p></td>
<td><p>必要</p></td>
<td><p>System.Uri</p></td>
<td><p>工作流程的 SIP 位址。例如：-PrimaryUri &quot;sip:helpdesk@litwareinc.com&quot;。PrimaryUri 的開頭必須是 &quot;sip&quot;：首碼。</p></td>
</tr>
<tr class="even">
<td><p><em>Active</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True 時，表示工作流程為使用中，可以接聽電話。如果設為 False (預設值)，工作流程便無法接聽電話。</p>
<p>Active 屬性設為 True 時，系統則會先驗證工作流程再建立之。例如，若未指定 DefaultAction，則不會建立工作流程。如果 Active 設為 False (或未設定)，則不會進行驗證，即使未指定 DefaultAction，仍會建立工作流程。</p></td>
</tr>
<tr class="odd">
<td><p><em>Anonymous</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，則任何時候當各個回應群組代理在接聽電話時，這些代理的識別會加上遮罩。如果設為 False (預設值)，則來電者可看見代理的識別。</p></td>
</tr>
<tr class="even">
<td><p><em>BusinessHoursID</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>工作流程代理一星期有哪幾天和哪些時段可接聽來電。使用 <strong>Get-CsRgsHoursOfBusiness</strong> Cmdlet 可以擷取營業時間 Identities。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="even">
<td><p><em>CustomMusicOnHoldFile</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.AudioFile</p></td>
<td><p>表示當來電者等候接聽時播放的自訂音樂(如果未定義，來電者在等候接聽時會聽到預設的音樂)。自訂音樂必須使用 <strong>Import-CsRgsAudioFile</strong> Cmdlet 匯入。</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultAction</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction</p></td>
<td><p>表示於營業時間開啟工作流程時要採取的動作。必須使用 <strong>New-CsRgsCallAction</strong> Cmdlet 定義 DefaultAction，而且必須將通話引導至佇列或問題。如果工作流程為使用中，則 DefaultAction 為必要項目，但如果未使用工作流程，則可以省略此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓系統管理員新增有關回應群組工作流程的額外資訊。例如，描述可包括工作流程擁有者的連絡人資訊。此描述出現在工作流程的 Lync 連絡人卡片中。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>在 Lync 中顯示的工作流程電話號碼。DisplayNumber 可設定成任何您想要的格式，例如：</p>
<p>-DisplayNumber &quot;555-1219&quot;</p>
<p>-DisplayNumber &quot;1-(425)-555-1219&quot;</p>
<p>-DisplayNumber &quot;1.425.555.1219&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>EnabledForFederation</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示工作流程是否可供同盟網域的使用者使用。如果設為 False，則只有您組織中的使用者能夠存取工作流程。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>HolidayAction</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction</p></td>
<td><p>如果在假日接到電話時要採取的動作。HolidayAction 必須使用 <strong>New-CsRgsCallAction</strong> Cmdlet 定義。</p></td>
</tr>
<tr class="odd">
<td><p><em>HolidaySetIDList</em></p></td>
<td><p>選用</p></td>
<td><p>System.Collections.ObjectModel.Collection</p></td>
<td><p>表示哪幾天工作流程代理不會接聽來電。使用 <strong>Get-CsRgsHolidaySet</strong> Cmdlet 可以擷取假日集 Identities。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>Language</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>用於讀取工作流程文字轉換語音提示的語言。只要作業系統使用下方清單列出的支援語言，語言參數則為選用項目 (請注意，支援的語音語言代表作業系統上可以使用的語言子集)。</p>
<p>如果作業系統並非使用支援的語言，則 Language 參數會變成必要項目，且該參數必須指定支援語言的語言代碼。如果您的作業系統使用不支援的語言，而且您執行 <strong>New-CsRgsWorkflow</strong> Cmdlet 且不包含 Language 參數，則您的命令會失敗。</p>
<p>例如，假設您的作業系統以法羅群島語執行。Windows 作業系統支援此語言，但回應群組應用程式不支援此語言。因此，當您建立新的工作流程時，必須包含 Language 參數及支援的語言。</p>
<p>這是必要步驟，因為，若未指定語言，工作流程會使用作業系統的語言。但是，只有回應群組應用程式支援該語言時，您才能在工作流程中使用該語言。</p>
<p>語言必須使用下列其中一個語言代碼指定：</p>
<p>ca-ES – 卡達隆尼亞文 (西班牙)</p>
<p>da-DK – 丹麥文 (丹麥)</p>
<p>de-DE – 德文 (德國)</p>
<p>en-AU – 英文 (澳大利亞)</p>
<p>en-CA – 英文 (加拿大)</p>
<p>en-GB – 英文 (英國)</p>
<p>en-IN – 英文 (印度)</p>
<p>en-US – 英文 (美國)</p>
<p>es-ES – 西班牙文 (西班牙)</p>
<p>es-MX – 西班牙文 (墨西哥)</p>
<p>fi-FI – 芬蘭文 (芬蘭)</p>
<p>fr-CA – 法文 (加拿大)</p>
<p>fr-FR – 法文 (法國)</p>
<p>it-IT – 義大利文 (義大利)</p>
<p>ja-JP – 日文 (日本)</p>
<p>ko-KR – 韓文 (韓國)</p>
<p>nb-NO – 挪威文，巴克摩 (挪威)</p>
<p>nl-NL – 荷蘭文 (荷蘭)</p>
<p>pl-PL – 波蘭文 (波蘭)</p>
<p>pt-BR – 葡萄牙文 (巴西)</p>
<p>pt-PT – 葡萄牙文 (葡萄牙)</p>
<p>ru-RU – 俄文 (俄羅斯)</p>
<p>sv-SE – 瑞典文 (瑞典)</p>
<p>zh-CN – 中文 (中華人民共和國)</p>
<p>zh-HK – 中文 (香港特別行政區)</p>
<p>zh-TW – 中文 (台灣)</p>
<p>例如：-Language &quot;nl-NL&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>LineUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.Uri</p></td>
<td><p>工作流程的電話號碼。必須使用下列格式指定電話線路統一資源識別元 (URI)：在 TEL:首碼後面加上加號，後面再加上國碼/地區碼、區碼與電話號碼 (只能使用數字：不能有空格、句點或連字號)。例如：-LineUri &quot;TEL:+14255551219&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Managed</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時表示該工作流程將由一或多位使用者來管理。可以用 ManagedByUri 參數來指定那些使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>ManagersByUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.Collections.ObjectModel.Collection</p></td>
<td><p>將要管理工作流程之使用者的 SIP 位址。例如：</p>
<p>-ManagedByUri &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>若要指定多位管理員，請用逗號隔開管理員 SIP 位址：</p>
<p>-ManagedByUri &quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>NonBusinessHoursAction</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction</p></td>
<td><p>如果在工作流程指定的營業時間之外接到來電時，應採取的動作。NonBusinessHoursAction 必須使用 <strong>New-CsRgsCallAction</strong> Cmdlet 定義。</p></td>
</tr>
<tr class="even">
<td><p><em>TimeZone</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>用於決定假日與營業時間的時區資訊。例如：-TimeZone &quot;Pacific Standard Time&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsRgsWorkflow** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsRgsWorkflow** Cmdlet 會建立 Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsWorkflow](get-csrgsworkflow.md)  
[Remove-CsRgsWorkflow](remove-csrgsworkflow.md)  
[Set-CsRgsWorkflow](set-csrgsworkflow.md)

