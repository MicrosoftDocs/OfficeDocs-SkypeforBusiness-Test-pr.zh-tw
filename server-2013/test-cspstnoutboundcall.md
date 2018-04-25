---
title: Test-CsPstnOutboundCall
TOCTitle: Test-CsPstnOutboundCall
ms:assetid: 12d940c3-8526-4c8f-8dc1-3fe65a3211bc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398207(v=OCS.15)
ms:contentKeyID: 49290153
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPstnOutboundCall

 

_**上次修改主題的時間：** 2015-03-09_

測試使用者撥電話給公用交換電話網路 (PSTN) 上之電話號碼的能力。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsPstnOutboundCall -TargetPstnPhoneNumber <String> -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPstnOutboundCall -TargetFqdn <String> -TargetPstnPhoneNumber <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPstnOutboundCall [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

範例 1 會檢查預先設定的測試使用者是否可以登入 atl-cs-001.litwareinc.com 集區，然後撥打跨 PSTN 閘道的電話。只有已針對 atl-cs-001.litwareinc.com 集區定義測試使用者時，此命令才有作用。如果已經定義，則此命令將會判斷第一個測試使用者是否可以登入系統，並且 (如果可以登入) 撥打位於 PSTN 網路的電話。

如果尚未定義測試使用者，則此命令將會因為不知道在執行測試時要採用哪個使用者而失敗。如果您未定義集區的測試使用者，則必須加入 UserSipAddress 參數及參與測試之使用者帳戶的對應認證。接著，**Test-CsPstnOutboundCall** Cmdlet 將會使用指定的使用者進行其檢查。

    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -TargetPstnPhoneNumber "+15551234567" 

## 範例 2

範例 2 所示的命令會測試測試使用者 (litwareinc\\kenmyer) 登入 Lync Server 的功能，然後跨 PSTN 閘道撥打電話。為達此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet 建立一個包含使用者 Ken Myer 之名稱與密碼的 Windows PowerShell 認證物件 (因為已加上登入名稱 litwareinc\\kenmyer 做為參數，所以系統管理員只需要在 \[Windows PowerShell 認證要求\] 對話方塊輸入 Ken Myer 帳戶的密碼)。然後，將產生的認證物件儲存在名稱為 $cred1 的變數中。

有了認證物件之後，範例中的第二個命令會判斷測試使用者是否可以登入 Lync Server，然後撥打目標電話號碼 (+15551234567)。為了執行此工作，會呼叫 **Test-CsPstnOutboundCall** Cmdlet 搭配下列參數：TargetFqdn (登錄器集區的 FQDN)、UserSipAddress (撥打電話之使用者的 SIP 位址)、UserCredential (包含測試使用者認證的 Windows PowerShell 物件) 和 TargetPstnPhoneNumber (要撥打的電話號碼)。

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -TargetPstnPhoneNumber "+15551234567" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred1

## 範例 3

範例 3 顯示如何在伺服器平台模式中使用 **Test-CsPstnOutboundCall** Cmdlet。在此模式中，已指定使用者的 SIP 位址，但不包含使用者認證。這樣執行時，Lync Server 會使用憑證來驗證測試使用者。

    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress sip:kenmyer@litwareinc.com -TargetPstnPhoneNumber "+15551234567"

## 詳細描述

**Test-CsPstnOutboundCall** Cmdlet 是 Lync Server「綜合交易」的範例。Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員手動執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

綜合交易通常以兩種不同的方式進行。許多系統管理員會使用 **CsHealthMonitoringConfiguration** Cmdlet 來設定其每個登錄器集區的測試使用者。這些測試使用者是已預先設定要搭配使用綜合交易的一對使用者。(通常這些使用者是測試帳戶，而不是屬於真正使用者的帳戶)。利用對集區設定的測試使用者，系統管理員只要對集區執行綜合交易，無須指定測試中牽涉之使用者帳戶的識別身分 (並提供其認證)。

或者，系統管理員可以使用實際的使用者帳戶執行綜合交易。例如，如果有兩個使用者無法交換立即訊息，系統管理員可以使用上述兩個使用者帳戶 (而非一組測試帳戶) 執行綜合交易，然後嘗試診斷並解決問題。如果您決定使用實際的使用者帳戶執行綜合交易，則必須提供每位使用者的登入名稱和密碼。

Test-CsPstnOutboundCall 也可以在伺服器平台模式中使用。在此情況下，您只需要指定使用者的 SIP 位址，Lync Server 會使用憑證來驗證該使用者。

當您執行 **Test-CsPstnOutboundCall** Cmdlet 時，Cmdlet 會先嘗試將測試使用者登入到 Lync Server。如果登入成功，則此 Cmdlet 會嘗試跨 PSTN 閘道撥打電話。這通電話將會使用撥號對應表、語音原則及其他指派給測試帳戶的原則和設定來撥打。接聽來電時，Cmdlet 會透過網路傳送雙音多頻 (DTMF) 碼，以驗證媒體連線。

進行測試時，**Test-CsPstnOutboundCall** Cmdlet 會撥打實際的電話：目標電話將會響鈴，而且必須接聽以測試是否成功。這通電話也必須由系統管理員手動結束。

誰可以執行這個 Cmdlet：若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPstnOutboundCall"}

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
<td><p><em>TargetFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>要測試之集區的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPstnPhoneNumber</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>進行測試時所要撥打的 PSTN 電話號碼。建議以 E.164 格式指定目標電話號碼，這表示號碼會類似 &quot;+14255551298&quot;，號碼中含有加號 (+) 加上國家/地區撥接碼 (1)、區碼 (425) 和電話號碼 (5551298)。指定電話號碼時，請勿使用虛線、括弧或其他任何字元。</p>
<p>如果不採用 E.164 格式，測試使用者的撥號對應表會附加至號碼尾端。然後，Lync Server 會使用該撥號對應表將號碼正規化為 E.164 格式。如果無法正規化號碼，則無法撥打電話，測試將會失敗。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試之帳戶的使用者認證物件。傳送到 UserCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參照。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存在名稱為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果命令使用以 CsHealthMonitoringConfiguration Cmdlet 所設定的測試使用者，則不需要此參數。如果在伺服器平台模式中執行測試，也不需要指定此參數。在此情況下，Lync Server 會嘗試使用憑證來驗證使用者。</p></td>
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
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
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
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，您可使用下列語法，將輸出儲存於名為 $TestOutput 的變數中：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>登錄程式服務所使用的 SIP 連接埠。如果登錄程式使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要測試之使用者帳戶的 SIP 位址。例如：-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。UserSipAddress 參數必須參考與 UserCredential 相同的使用者帳戶。</p>
<p>如果命令使用以 CsHealthMonitoringConfiguration Cmdlet 所設定的測試使用者，則不需要此參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsPstnOutboundCall** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsPstnOutboundCall** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsPstnPeerToPeerCall](test-cspstnpeertopeercall.md)

