---
title: Test-CsExUMVoiceMail
TOCTitle: Test-CsExUMVoiceMail
ms:assetid: 88734ae8-1339-4080-a4bb-544181f6d1d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205058(v=OCS.15)
ms:contentKeyID: 49291570
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsExUMVoiceMail

 

_**上次修改主題的時間：** 2015-03-09_

驗證使用者是否可以連線到 Exchange Unified Messaging，並留語音信箱訊息給另一位使用者。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsExUMVoiceMail -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] [-WaveFile <String>] <COMMON PARAMETERS>

    Test-CsExUMVoiceMail -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] [-WaveFile <String>] <COMMON PARAMETERS>

    Test-CsExUMVoiceMail [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

上述的範例會針對 atl-cs-001.litwareinc.com 集區測試 Exchange Unified Messaging 語音信箱連線。只有已針對 atl-cs-001.litwareinc.com 集區定義測試使用者時，此命令才有作用。如果已定義，則命令會判斷第一位測試使用者是否可以使用 Unified Messaging 語音信箱。如果尚未設定集區的測試使用者，命令將會失敗。

    Test-CsExUMVoiceMail -TargetFqdn "atl-cs-001.litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com"

## 範例 2

範例 2 所示的命令會測試使用者 litwareinc\\kenmyer 的 Exchange Unified Messaging 語音信箱連線。為達成此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet，以建立使用者 litwareinc\\kenmyer 的 Windows PowerShell 命令列介面認證物件。請注意，您必須提供此帳戶的密碼，才能建立有效的認證物件，並確保 **Test-CsExUMVoiceMail** Cmdlet 可以執行這項檢查。

範例中的第二個命令會使用所提供的 ($x) 證證物件和使用者 litwareinc\\kenmyer 的 SIP 位址，來判斷此使用者是否能夠連線至 Exchange Unified Messaging 語音信箱。

    $credential = Get-Credential "litwareinc\pilar"
    
    Test-CsExUMVoiceMail -TargetFqdn "atl-cs-001.litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $credential

## 範例 3

範例 3 所示的命令是範例 1 所示命令的變化；但此範例會加入 OutLoggerVariable 參數，以產生 **Test-CsExUMVoiceMail** Cmdlet 所執行之各步驟的詳細記錄，以及各步驟的成功或失敗。為達成此目的，會加入 OutLoggerVariable 參數搭配 ExumText 參數值，以將詳細記錄資訊儲存在名為 $ExumTest 的變數中。範例的最後一個命令會使用 ToXML() 方法將記錄資訊轉換為 XML 格式。然後再使用 Out-File Cmdlet，將該 XML 資料寫入名為 C:\\Logs\\VoicemailTest.xml 的檔案中。

    Test-CsExUMVoiceMail -TargetFqdn "atl-cs-001.litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -OutLoggerVariable VoicemailTest
    
    $VoicemailTest.ToXML() | Out-File C:\Logs\VoicemailTest.xml

## 詳細描述

**Test-CsExUMVoiceMail** Cmdlet 可讓系統管理員驗證使用者是否可以存取及使用 Microsoft Exchange Server 2013 Unified Messaging 服務。為達成此目的，此 Cmdlet 會連線到 Unified Messaging 服務，並在指定的信箱中留下語音信箱訊息。這可以是系統提供的語音信箱訊息，或是您自己錄音的自訂 .WAV 檔案。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsExUMVoiceMail"}

**Lync Server 控制台：**Test-CsExUMVoiceMail Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>SenderCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>將要留語音信箱訊息之使用者帳戶的使用者認證物件。傳遞至 SenderCredential 的值必須是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參照。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要傳送者認證。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>要測試之集區的完整網域名稱 (FQDN)。例如：</p>
<p>-TargetFqdn atl-cs-001.litwareinc.com</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>選用</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>執行測試時所使用的驗證類型。允許的值為：</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>附註：指定變數名稱時，請勿在前面加上 $ 字元。</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要接收測試語音信箱之使用者帳戶的 SIP 位址 (此 SIP 位址必須不同於傳送者使用的 SIP 位址)。例如：</p>
<p>-ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;</p>
<p>不需要包含語音信箱收件者的憑證。</p></td>
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
<td><p>String</p></td>
<td><p>要留語音信箱訊息之使用者帳戶的 SIP 位址 (此 SIP 位址必須不同於收件者使用的 SIP 位址)。例如：</p>
<p>-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>SenderSIPAddress 參數必須照與 SenderCredential 相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>WaveFile</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>測試語音信箱服務時可使用之 .WAV 音訊檔案的路徑。若包含此參數， <strong>Test-CsExUMVoiceMail</strong> Cmdlet 將會在連線至 Exchange 語音信箱時，播放指定的 .WAV 檔。若未包含此參數，則會播放預設的音訊檔案。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。Test-CsExUMVoiceMail Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsExUMVoiceMail** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsExUMConnectivity](test-csexumconnectivity.md)

