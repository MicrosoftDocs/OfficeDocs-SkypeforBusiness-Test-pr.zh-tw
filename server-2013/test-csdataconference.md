---
title: Test-CsDataConference
TOCTitle: Test-CsDataConference
ms:assetid: bd7f3c98-7b10-494e-adce-a9b20428b6cc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205219(v=OCS.15)
ms:contentKeyID: 49292176
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDataConference

 

_**上次修改主題的時間：** 2015-03-09_

確認一組使用者是否可以參與 Lync Server 2013 Web 會議，會議中包含像是共用或檢視 PowerPoint 投影片、白板或投票等活動。Cmdlet 也會確認 Lync Server Web 會議服務可以探索 Office Web Apps Server，而且用戶端可以透過 Office Web Apps Server 上傳 PowerPoint 檔案以進行廣播。

Lync Server 2013中已導入此 Cmdlet。

## 語法

    Test-CsDataConference -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsDataConference -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsDataConference [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會確認是否可以在集區 atl-cs-001.litwareinc.com 上進行資料會議。此命令假設您已針對指定的集區設定一對測試使用者。如果不存在測試使用者，則命令會失敗。

    Test-CsDataConference -TargetFqdn "atl-cs-001.litwareinc.com"

## 範例 2

範例 2 所示的命令會測試一對使用者 (litwareinc\\pilar 和 litwareinc\\kenmyer) 可以登入 Lync Server 2013，然後舉行資料會議的能力。為達成此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet，來建立包含使用者 Pilar Ackerman 之名稱與密碼的 Windows PowerShell 命令列介面認證物件 (因為已加上登入名稱 (litwareinc\\pilar) 做為參數，所以 \[ Windows PowerShell 認證要求\] 對話方塊只會要求系統管理員輸入 Pilar Ackerman 帳戶的密碼)。接著會將產生的認證物件儲存於名為 $cred1 的變數中。第二個命令會執行相同的動作，只不過這次是傳回 Ken Myer 帳戶的認證物件。

手邊有了認證物件之後，第三個命令會判斷這兩位使用者是否可以登入 Lync Server 2013，然後舉行資料會議。為了執行此工作，會呼叫 **Test-CsDataConference** Cmdlet 搭配下列參數：TargetFqdn (登錄器集區的 FQDN)、SenderSipAddress (第一位測試使用者的 SIP 位址)、SenderCredential (包含這位相同使用者之認證的 Windows PowerShell 物件)、ReceiverSipAddress (另一位測試使用者的 SIP 位址) 和 ReceiverCredential (包含另一位測試使用者之認證的 Windows PowerShell 物件)。

    $credential1 = Get-Credential "litwareinc\pilar"
    $credential2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsDataConference -TargetFqdn "atl-cs-001.litwareinc.com" -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $credential1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $credential2

## 詳細描述

在 Lync Server 2013 中，資料會議是指進行共同作業活動 (例如使用白板或註釋) 的會議。 **Test-CsDataConference** Cmdlet 可讓您確認一對使用者是否可以參與資料會議。

能否舉行資料會議取決於召開會議之使用者 (若是使用 **Test-CsDataConference** Cmdlet，即為「傳送者」) 所獲指派的會議原則。若召集人無法在其會議中加入共同作業活動 (例如，其會議原則的 EnableDataCollaboration 屬性設為 False)， **Test-CsDataConference** Cmdlet 將會失敗。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDataConference"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Test-CsDataConference** Cmdlet 所執行的功能。

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
<td><p><em>ReceiverCredential</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>要測試之兩個使用者帳戶中第一個帳戶的使用者認證物件。傳給 ReceiverCredential 的值應該是以 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\pilar 的認證物件，並將該物件儲存於名為 $y 的變數中：</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要接收者認證。</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的使用者認證物件。傳給 SenderCredential 的值，應是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參照。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要傳送者認證。</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要測試之常設聊天室集區的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.SyntheticTransactions.SipSyntheticTransaction+AuthenticationMechanism</p></td>
<td><p>執行測試時所使用的驗證類型。允許的值為：</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注意：指定變數名稱時，請勿在前面加上 $ 字元。</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的 SIP 位址。例如：</p>
<p>-ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;</p>
<p>ReceiverSIPAddress 參數必須與 ReceiverCredential 參考相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。如果登錄器使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的 SIP 位址。例如：</p>
<p>-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>SenderSipAddress 參數必須與 SenderCredential 參考相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會測試 Join Launcher 參與會議的能力。Join Launcher 可用來協助行動裝置使用者 (進而協助 Mobility Service 使用者) 參與會議。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsDataConference** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsDataConference** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsASConference](test-csasconference.md)

