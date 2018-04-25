---
title: Test-CsIM
TOCTitle: Test-CsIM
ms:assetid: 2fdab54c-5ec4-4db5-b29c-a3efaae68f66
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425802(v=OCS.15)
ms:contentKeyID: 49290484
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsIM

 

_**上次修改主題的時間：** 2015-03-09_

測試兩位使用者交換立即訊息的能力。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-EmailHost <String>] [-Force <SwitchParameter>] [-IsSsl <$true | $false>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Password <String>] [-Port <UInt16>] [-TestLegalIntercept <SwitchParameter>] [-Username <String>] [-WaitSeconds <Int16>]

## 範例

## 範例 1

範例 1 會檢查預先設定的測試使用者配對是否可以登入 atl-cs-001.litwareinc.com 集區，然後交換立即訊息。只有已針對 atl-cs-001.litwareinc.com 集區定義測試使用者時，此命令才有作用。如有定義，此命令會判斷兩位使用者是否可以登入系統，如果可以，則可以交換立即訊息。

若尚未定義測試使用者，則此命令將會因為不知道在執行測試時要採用哪些使用者而失敗。如果您未定義集區的登錄器，則必須加上 SenderSipAddress 及 eceiverSipAddress 參數，還有 IM 工作階段中所涉及之使用者的對應認證。接著，**Test-CsIM** Cmdlet 便會使用兩個指定的使用者進行檢查。

    Test-CsIm -TargetFqdn atl-cs-001.litwareinc.com

## 範例 2

範例 2 所示的命令會測試一組使用者 (litwareinc\\pilar 和 litwareinc\\kenmyer) 是否能夠登入 Lync Server，然後交換立即訊息。為達此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet 建立一個包含使用者 Pilar Ackerman 之名稱與密碼的 Windows PowerShell 認證物件 (因為已加上登入名稱 litwareinc\\pilar 做為參數，所以系統管理員只需要在 \[Windows PowerShell 認證要求\] 對話方塊輸入 Pilar Ackerman 帳戶的密碼)。然後，產生的認證物件會儲存在名稱為 $cred1 的變數中。第二個命令會執行相同的動作，但這次會傳回 Ken Myer 帳戶的認證物件。

手邊有了這兩個認證物件之後，此範例中的第三個命令會判斷這兩個使用者是否可以登入 Lync Server，然後交換立即訊息。為達成此目的，會呼叫 **Test-CsIM** Cmdlet 搭配下列參數：TargetFqdn (登錄器集區的 FQDN)；SenderSipAddress (第一個測試使用者的 SIP 位址)；SenderCredential (包含該使用者之認證的 Windows PowerShell 物件)；-ReceiverSipAddress (其他測試使用者的 SIP 位址)；以及 ReceiverCredential (包含其他使用者之認證的 Windows PowerShell 物件)。

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsIm -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## 詳細描述

**Test-CsIM** Cmdlet 是 Lync Server「綜合交易」的範例。Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員手動執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

綜合交易通常以兩種不同的方式進行。許多系統管理員會使用 **CsHealthMonitoringConfiguration** Cmdlet 來設定其每個登錄器集區的測試使用者。這些測試使用者是已預先設定要搭配使用綜合交易的一對使用者。(通常這些使用者是測試帳戶，而不是屬於真正使用者的帳戶)。利用對集區設定的測試使用者，系統管理員只要對集區執行綜合交易，無須指定測試中牽涉之使用者帳戶的識別身分 (並提供其認證)。

或者，系統管理員可以使用實際的使用者帳戶執行綜合交易。例如，如果有兩個使用者無法交換立即訊息，系統管理員可以使用上述兩個使用者帳戶 (而非一組測試帳戶) 執行綜合交易，以嘗試診斷並解決問題。如果您決定使用實際的使用者帳戶執行綜合交易，則必須提供每個使用者的認證。

**Test-CsIM** Cmdlet 會從嘗試將一組測試使用者登入 Lync Server 開始。假設這兩個登入都成功，則 Cmdlet 會起始兩個測試使用者之間的立即訊息 (IM) 工作階段 (使用者 1 邀請使用者 2 進行 IM 工作階段，而使用者 2 接受邀請)。確認訊息可以在兩個使用者之間進行交換後，**Test-CsIM** Cmdlet 會結束 IM 工作階段，並將兩個使用者登出系統。

誰可以執行這個 Cmdlet：若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsIM"}

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
<td><p>PSCredential</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的使用者認證物件。傳給 ReceiverCredential 的值應該是以 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\pilar 的認證物件，並將該物件儲存於名為 $y 的變數中：</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要接收者認證。</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的使用者認證物件。傳給 SenderCredential 的值應該是以 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，此程式碼會傳回的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要傳送者認證。</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>要測試之集區的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>選用</p></td>
<td><p>SipSyntheticTransaction + AuthenticationMechanism</p></td>
<td><p>測試中所使用的驗證類型。允許的值為：</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>EmailHost</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>合法監聽測試中所使用之使用者的電子郵件主機。例如：</p>
<p>-EmailHost &quot;litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>IsSsl</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>此參數設為 True 時，會指定該測試是使用安全通訊端層 (SSL) 通訊協定來進行。</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注意：指定變數名稱時，請勿在前面加上 $ 字元。若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似下列的命令：</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如果有，執行 Cmdlet 所產生的詳細輸出就會儲存在指定變數中。例如，您可使用下列語法，將輸出儲存於名為 $TestOutput 的變數中：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="even">
<td><p><em>Password</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>合法監聽測試中所使用的密碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>Port</em></p></td>
<td><p>選用</p></td>
<td><p>UInt16</p></td>
<td><p>用於合法監聽服務的通訊埠。</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的 SIP 位址。例如：-ReceiverSipAddress &quot;sip:jhaas@litwareinc.com&quot;。ReceiverSipAddress 參數必須參考與 ReceiverCredential 相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>登錄程式服務所使用的 SIP 連接埠。如果登錄程式使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的 SIP 位址。例如：-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。SenderSipAddress 參數必須與 SenderCredential 參考相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>TestLegalIntercept</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>使用此參數時，會指示 Test-CsIM 針對指定的使用者，測試合法監聽服務。</p></td>
</tr>
<tr class="even">
<td><p><em>Username</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>合法監聽測試中所使用之使用者的使用者名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>WaitSeconds</em></p></td>
<td><p>選用</p></td>
<td><p>Int16</p></td>
<td><p>指定系統應等候合法監聽服務回應的時間量 (以秒為單位)。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsIM** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsIM** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsGroupIM](test-csgroupim.md)

