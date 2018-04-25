---
title: Test-CsPstnPeerToPeerCall
TOCTitle: Test-CsPstnPeerToPeerCall
ms:assetid: 839cf83f-b667-4cbe-b1ab-28f54a8a9d0b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398662(v=OCS.15)
ms:contentKeyID: 49291522
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPstnPeerToPeerCall

 

_**上次修改主題的時間：** 2015-03-09_

測試使用者配對是否可以利用公用交換電話網路 (PSTN) 閘道撥打對等通話。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsPstnPeerToPeerCall -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPstnPeerToPeerCall -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPstnPeerToPeerCall [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

範例 1 會檢查一對預先設定的測試使用者是否可以登入 atl-cs-001.litwareinc.com 集區；在測試使用者登入之後，**Test-CsPstnPeerToPeerCall** Cmdlet 會接著檢查這兩位使用者是否可以透過 PSTN 閘道進行對等通話。只有已針對 atl-cs-001.litwareinc.com 集區定義測試使用者時，此命令才有作用。若已定義，則命令會判斷第一位使用者是否可以登入系統，然後檢查此使用者是否可以呼叫針對此集區定義的第二位使用者。

若尚未定義測試使用者，則此命令將會因為不知道在執行測試時要採用哪些使用者而失敗。若您未定義集區的測試使用者，而且不是在伺服器平台模式中執行，則必須加上 SenderSipAddress 和 ReceiverSipAddress 參數，以及擔任測試帳戶之使用者的對應認證。然後，**Test-CsPstnPeerToPeerCall** Cmdlet 會使用這兩位指定的使用者進行檢查。

    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com 

## 範例 2

範例 2 所示的命令會測試一組使用者 (litwareinc\\pilar 和 litwareinc\\kenmyer) 是否能登入 Lync Server，然後透過 PSTN 閘道進行對等通話。為達此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet 建立包含使用者 Pilar Ackerman 之名稱與密碼的 Windows PowerShell 認證物件 (因為已加上登入名稱 litwareinc\\pilar 做為參數，所以系統管理員只需要在 \[Windows PowerShell 認證要求\] 對話方塊輸入 Pilar Ackerman 帳戶的密碼)。然後，產生的認證物件會儲存在名為 $cred1 的變數中。第二個命令會執行相同的動作，但會傳回 Ken Myer 帳戶的認證物件。

有了這兩個認證物件，範例中的第三個命令會判斷這兩位使用者是否可以登入 Lync Server，然後在 PSTN 閘道上進行對等通話。為了執行此工作，會呼叫 **Test-CsPstnPeerToPeerCall** Cmdlet 並搭配下列參數：TargetFqdn (登錄器集區的 FQDN)、SenderSipAddress (第一位測試使用者的 SIP 位址)、SenderCredential (包含這同一位使用者之憑證的 Windows PowerShell 物件)、ReceiverSipAddress (另一位測試使用者的 SIP 位址) 和 ReceiverCredential (包含另一位使用者之憑證的 Windows PowerShell 物件)。

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:jhaas@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## 範例 3

範例 3 顯示如何在伺服器平台模式中使用 Test-CsPstnPeerToPeerCall Cmdlet。在此模式中，可以指定測試使用者的 SIP 位址，但不包含使用者認證。以此方式執行時，Lync Server 會使用憑證來驗證這兩位測試使用者。

    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:jhaas@litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com" 

## 詳細描述

**Test-CsPstnPeerToPeerCall** Cmdlet 是 Lync Server「綜合交易」的範例。Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員手動執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

綜合交易通常以兩種不同的方式進行。許多系統管理員會使用 **CsHealthMonitoringConfiguration** Cmdlet 來設定其每個登錄器集區的測試使用者。這些測試使用者是已預先設定要搭配使用綜合交易的一對使用者。(通常這些使用者是測試帳戶，而不是屬於真正使用者的帳戶)。利用對集區設定的測試使用者，系統管理員只要對集區執行綜合交易，無須指定測試中牽涉之使用者帳戶的識別身分 (並提供其認證)。

另一種方式是系統管理員會使用真正的使用者帳戶來執行綜合交易。例如，如果兩個使用者無法交換立即訊息，則系統管理員可以使用這兩個有問題的使用者帳戶 (而非一對測試帳戶) 執行綜合交易，然後嘗試診斷及解決問題。如果您決定使用實際的使用者帳戶執行綜合交易，則必須提供每位使用者的登入名稱和密碼。

**Test-CsPstnPeerToPeerCall** Cmdlet 也可以在伺服器平台模式中使用。如果是這樣的情況，您只需指定使用者的 SIP 位址，Lync Server 將使用憑證來驗證那些使用者。

當您呼叫 **Test-CsPstnPeerToPeerCall** 時，此 Cmdlet 會先嘗試將這兩位測試使用者登入 Lync Server。假設登入成功，Cmdlet 接著會讓使用者 1 嘗試在 PSTN 閘道上撥打電話給使用者 2；**Test-CsPstnPeerToPeerCall** Cmdlet 會使用撥號對應表、語音原則，以及其他指派給這位測試使用者的原則與組態設定撥打這通電話。如果測試依計畫進行，Cmdlet 將會確認使用者 2 可以接聽電話，然後將這兩個測試帳戶從系統登出。

**Test-CsPstnPeerToPeerCall** Cmdlet 會實際撥打一通電話來確認可進行連線，同時跨網路傳輸雙音多頻 (DTMF) 代碼來判斷是否可透過連線傳送媒體。但是，來電是由 Cmdlet 本身接聽，而且不需手動終止來電 (也就是說，不需要人員接聽，然後掛斷來電)。

誰可以執行這個 Cmdlet：若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPstnPeerToPeerCall"}

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
<td><p>要測試之兩個使用者帳戶中之第一個的使用者認證物件。傳給 ReceiverCredential 的值應該是以 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\pilar 的認證物件，並將該物件儲存於名為 $y 的變數中：</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您是在集區的狀況監控組態下執行測試，或者如果您正在伺服器平台模式中執行，則不需要接收者認證。</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試之兩個使用者帳戶中之第二個的使用者認證物件。傳給 SenderCredential 的值應該是以 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您是在集區的狀況監控組態下執行測試，或者如果您正在伺服器平台模式中執行，則不需要傳送者認證。</p></td>
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
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>測試中所使用的驗證類型。允許的值為：</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>附註：指定變數名稱時，請勿在前面加上 $ 字元。若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似下列的命令：</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的 SIP 位址。例如：-ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;。ReceiverSIPAddress 參數必須參照與 ReceiverCredential 相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。如果登錄器使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的 SIP 位址。例如：-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。SenderSipAddress 參數必須參照與 SenderCredential 相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsPstnPeerToPeerCall** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsPstnPeerToPeerCall** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsPstnOutboundCall](test-cspstnoutboundcall.md)

