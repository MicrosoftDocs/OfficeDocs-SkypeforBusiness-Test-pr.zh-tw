---
title: Test-CsPresence
TOCTitle: Test-CsPresence
ms:assetid: 09a5faf6-4e80-4a3b-ac84-aec9778ee9b5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398148(v=OCS.15)
ms:contentKeyID: 49290028
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPresence

 

_**上次修改主題的時間：** 2015-03-09_

測試使用者是否能夠登入 Lync Server、發佈自己的目前狀態資訊，以及訂閱其他使用者所發佈的目前狀態資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsPresence -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-PublisherSipAddress <String>] [-RegistrarPort <Int32>] [-SubscriberSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPresence -PublisherCredential <PSCredential> -PublisherSipAddress <String> -SubscriberCredential <PSCredential> -SubscriberSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPresence [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-SubscriberSipAddress <String>]

## 範例

## 範例 1

範例 1 檢查預先設定的一組測試使用者是否可以登入 atl-cs-001.litwareinc.com 集區；測試使用者登入之後，**Test-CsPresence** Cmdlet 會接著檢查兩位使用者是否可以交換目前狀態資訊。只有已針對 atl-cs-001.litwareinc.com 集區定義測試使用者時，此命令才有作用。如果已經定義，則此命令會判斷第一位測試使用者是否可以登入系統，然後檢查此使用者是否可以與針對集區定義之第二位測試使用者交換目前狀態資訊。

如果尚未定義登錄器，則命令會失敗，因為其不知道要用哪些使用者進行測試。如果您未定義集區的測試使用者，則必須加入 SubscriberSipAddress 和 PublisherSipAddress 參數，還有做為目前狀態訂閱者及目前狀態發行者之使用者的對應認證。接著，**Test-CsPresence** Cmdlet 便會使用兩個指定的使用者進行檢查。

    Test-CsPresence -TargetFqdn atl-cs-001.litwareinc.com 

## 範例 2

範例 2 所示的命令會測試一對使用者 (litwareinc\\pilar 和 litwareinc\\kenmyer) 是否能夠登入 Lync Server，然後交換目前狀態資訊。為達此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet 建立一個包含使用者 Pilar Ackerman 之名稱與密碼的 Windows PowerShell 認證物件 (因為已加上登入名稱 litwareinc\\pilar 做為參數，所以系統管理員只需要在 \[Windows PowerShell 認證要求\] 對話方塊輸入 Pilar Ackerman 帳戶的密碼)。然後，產生的認證物件會儲存在名稱為 $cred1 的變數中。第二個命令會執行相同的動作，但這次會傳回 Ken Myer 帳戶的認證物件。

在已有這兩個認證物件的情況下，範例中的第三個命令會判斷這兩個使用者是否可以登入 Lync Server，然後交換目前狀態資訊。為了執行此工作，會呼叫 **Test-CsPresence** Cmdlet 搭配下列參數：TargetFqdn (登錄器集區的 FQDN)、SubscriberSipAddress (某位測試使用者的 SIP 位址)、SubscriberCredential (Windows PowerShell 物件，包含同一位使用者的認證)、PublisherSipAddress (另一位測試使用者的 SIP 位址)，以及 PublisherCredential (Windows PowerShell 物件，包含另一位使用者的認證)。

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPresence -TargetFqdn atl-cs-001.litwareinc.com -SubscriberSipAddress "sip:pilar@litwareinc.com" -SubscriberCredential $cred1 -PublisherSipAddress "sip:kenmyer@litwareinc.com" -PublisherCredential $cred2

## 詳細描述

**Test-CsPresence** Cmdlet 是 Lync Server 綜合交易的範例。Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員手動執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

綜合交易通常以兩種不同的方式進行。許多系統管理員會使用 **CsHealthMonitoringConfiguration** Cmdlet 來設定其每個登錄器集區的測試使用者。通常這些使用者是測試帳戶，而不是屬於真正使用者的帳戶。利用設定給集區的這些測試帳戶，系統管理員可以直接對該集區執行綜合交易，而無須指定測試所用使用者帳戶的身分識別 (和其認證)。

或者，系統管理員可以使用實際的使用者帳戶執行綜合交易。例如，如果有兩個使用者無法交換立即訊息，系統管理員可以使用上述兩個使用者帳戶 (而非一組測試帳戶) 執行綜合交易，然後嘗試診斷並解決問題。如果您決定使用實際的使用者帳戶執行綜合交易，則必須提供每位使用者的登入名稱和密碼。

**Test-CsPresence** Cmdlet 可用於判斷兩位測試使用者是否可以登入 Lync Server，並相互交換目前狀態資訊。為達成此目的，此 Cmdlet 會先將兩個使用者登入系統。如果兩者都登入成功，則第一個測試使用者會要求接收第二個使用者的目前狀態資訊。第二個使用者會發行此資訊，而 **Test-CsPresence** Cmdlet 會驗證該資訊已成功傳輸給第一個使用者。交換目前狀態資訊之後，兩個測試使用者接著會登出 Lync Server。

誰可以執行這個 Cmdlet：若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPresence"}

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
<td><p><em>PublisherCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的使用者認證物件。傳遞到 PublisherCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，此程式碼會傳回的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您要使用集區的狀況監控組態設定執行測試，則不需要發行者認證。</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriberCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的使用者認證物件。傳遞到 SubscriberCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\pilar 的認證物件，並將該物件儲存於名為 $y 的變數中：</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您要使用集區的狀況監控組態設定執行測試，則不需要訂閱者認證。</p></td>
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
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，您可使用下列語法，將輸出儲存於名為 $TestOutput 的變數中：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="even">
<td><p><em>PublisherSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的 SIP 位址。例如：-PublisherSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。PublisherSipAddress 參數必須參考與 PublisherCredential 相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>登錄程式服務所使用的 SIP 連接埠。如果登錄程式使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriberSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的 SIP 位址。例如：-SubscriberSipAddress &quot;sip:pilar@litwareinc.com&quot;。SubscriberSipAddress 參數必須參考與 SubscriberCredential 相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsPresence** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsPresence** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsRegistration](test-csregistration.md)

