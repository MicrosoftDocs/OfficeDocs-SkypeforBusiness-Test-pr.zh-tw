---
title: Test-CsPersistentChatMessage
TOCTitle: Test-CsPersistentChatMessage
ms:assetid: 08c6db0b-23e2-4fbe-8276-181275a40daf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204656(v=OCS.15)
ms:contentKeyID: 49290011
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPersistentChatMessage

 

_**上次修改主題的時間：** 2015-03-09_

驗證一對使用者能否使用常設聊天室服務 (舊名為群組聊天服務) 交換訊息。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsPersistentChatMessage -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPersistentChatMessage -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPersistentChatMessage [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ChatRoomUri <String>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Setup <$true | $false>] [-TestUser1SipAddress <String>] [-TestUser2SipAddress <String>]

## 範例

## 範例 1

範例 1 所示的命令會測試使用者配對 (litwareinc\\pilar 與 litwareinc\\kenmyer) 是否可以登入 Lync Server 2013，並使用常設聊天室服務交換訊息的功能。為達成此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet 建立包含使用者 Pilar Ackerman 之名稱與密碼的 Windows PowerShell 命令列介面認證物件 (因為已加上登入名稱 (litwareinc\\pilar) 做為參數，所以 \[ Windows PowerShell 認證要求\] 對話方塊只會要求系統管理員輸入 Pilar Ackerman 帳戶的密碼)。然後將產生的認證物件儲存在名為 $cred1 的變數中。第二個命令會執行相同的動作，但會傳回 Ken Myer 帳戶的認證物件。

在已有認證物件的情況下，第三個命令會判斷這兩位使用者是否可以登入 Lync Server 2013，並使用常設聊天室交換訊息。為了執行此工作，會呼叫 **Test-CsPersistentChatMessage** Cmdlet 搭配下列參數：TargetFqdn (登錄器集區的 FQDN)、SenderSipAddress (第一位測試使用者的 SIP 位址)、SenderCredential (包含這位相同使用者之憑證的 Windows PowerShell 物件)、ReceiverSipAddress (另一位測試使用者的 SIP 位址)，以及 ReceiverCredential (包含另一位測試使用者之憑證的 Windows PowerShell 物件)。

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPersistentChatMessage -TargetFqdn atl-persistentchat-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## 詳細描述

**Test-CsPersistentChatMessage** Cmdlet 會驗證使用者配對是否可以使用常設聊天室服務交換訊息。為達成此目的，此 Cmdlet 會先將兩位使用者登入 Lync Server 2013，再將其連線到常設聊天室並相互交換訊息，然後離開聊天室並登出兩位使用者。請注意，下列兩種情況會造成呼叫此 Cmdlet 失敗：一是未建立任何聊天室，一是未為兩個測試使用者帳戶指派授與常設聊天至服務存取權的常設聊天室原則。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPersistentChatMessage"}

Lync Server 控制台：**Test-CsPersistentChatMessage** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>要測試之兩個使用者帳戶中第一個帳戶的使用者認證物件。傳給 ReceiverCredential 的值應該是以 Get-Credential Cmdlet 取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\pilar 的認證物件，並將該物件儲存於名為 $y 的變數中：</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要接收者認證。</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的使用者認證物件。傳給 SenderCredential 的值，應是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參照。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要傳送者認證。</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>字串</p></td>
<td><p>要測試之登錄器集區的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>選用</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>執行測試時所使用的驗證類型。允許的值為：</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>ChatRoomUri</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>聊天室位置，由 Persistent Chat Server 的完整網域名稱與聊天室名稱組成。例如：</p>
<p>-ChatRoomIdentity &quot;atl-persistentchat-001.litwareinc.com\ITChatRoom&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>切換參數</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注意：指定變數名稱時，請勿在前面加上 $ 字元。</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput. ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput. ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的 SIP 位址。例如：</p>
<p>-ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;</p>
<p>ReceiverSIPAddress 參數必須與 ReceiverCredential 參考相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。如果登錄器使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的 SIP 位址。例如：</p>
<p>-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>SenderSipAddress 參數必須與 SenderCredential 參考相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>Setup</em></p></td>
<td><p>選用</p></td>
<td><p>布林值</p></td>
<td><p>讓此 Cmdlet 可以在無權存取 Lync Server 拓撲的監看員節點電腦上執行。若要執行此作業，請在有權存取該拓撲的電腦上執行 <strong>Test-CsPersistentChatMessage</strong> 搭配 Setup 參數。如此之後，您便可以在您的監看員節點電腦上執行此 Cmdlet。</p>
<p>使用 Setup 參數時也必須使用 TestUser1SipAddress 與 TestUser2SipAddress 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>TestUser1SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>Setup 參數中第一位測試使用者的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>TestUser2SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>Setup 參數中第二位測試使用者的 SIP 位址。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Test-CsPersistentChatMessage** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsPersistentChatMessage** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Grant-CsPersistentChatPolicy](grant-cspersistentchatpolicy.md)  
[New-CsPersistentChatPolicy](new-cspersistentchatpolicy.md)  
[Set-CsPersistentChatPolicy](set-cspersistentchatpolicy.md)

