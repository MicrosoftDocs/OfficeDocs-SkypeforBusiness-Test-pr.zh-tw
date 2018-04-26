---
title: Test-CsDialInConferencing
TOCTitle: Test-CsDialInConferencing
ms:assetid: e4aedf4f-77ac-4c8b-9613-07f8ea12c041
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399013(v=OCS.15)
ms:contentKeyID: 49292614
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDialInConferencing

 

_**上次修改主題的時間：** 2015-03-09_

**Test-CsDialInConferencing** Cmdlet 會檢查使用者是否可以參與電話撥入式會議工作階段。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsDialInConferencing -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetPstnPhoneNumber <String>] [-UserSipAddress <String>] [-VerifyConferenceJoin <$true | $false>] <COMMON PARAMETERS>

    Test-CsDialInConferencing -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] [-TargetPstnPhoneNumber <String>] [-VerifyConferenceJoin <$true | $false>] <COMMON PARAMETERS>

    Test-CsDialInConferencing [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

範例 1 會確認預先設定的測試使用者可以參與集區 atl-cs-001.litwareinc.com 上的電話撥入式會議。只有已針對集區 atl-cs-001.litwareinc.com 定義測試使用者時，此命令才有作用。如果已定義，則命令會判斷第一個測試使用者是否可以登入 Lync Server。

如果尚未定義測試使用者，則此命令會因為不知道登入的是哪個使用者而失敗。如果您尚未定義集區的測試使用者，則您必須包含 UserCredential 參數與在嘗試登入時該命令應使用之使用者的認證。

    Test-CsDialInConferencing -TargetFqdn atl-cs-001.litwareinc.com 

## 範例 2

範例 2 所示的命令會測試參與集區 atl-cs-001.litwareinc.com 上之電話撥入式會議特定使用者 (litwareinc\\pilar) 的能力。為達此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet 建立包含使用者 Pilar Ackerman 之名稱與密碼的 Windows PowerShell 認證物件 (因為加上了登入名稱 (litwareinc\\pilar) 做為參數，所以系統管理員只需在 \[Windows PowerShell 認證要求\] 對話方塊中輸入 Pilar Ackerman 帳戶的密碼)。產生的認證物件會儲存在名為 $cred1 的變數中。

接著，第二個命令會檢查使用者 Pilar Ackerman 是否可以登入集區 atl-cs-001.litwareinc.com 並參與電話撥入式會議。為了執行此工作，會呼叫 **Test-CsDialInConferencing** Cmdlet 搭配下列三個參數：TargetFqdn (登錄器集區的 FQDN)、UserCredential (包含 Pilar Ackerman 使用者認證的 Windows PowerShell 物件)，以及 UserSipAddress (對應至所提供使用者認證的 SIP 位址)。

    $cred1 = Get-Credential "litwareinc\pilar"
    
    Test-CsDialInConferencing -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:pilar@litwareinc.com" -UserCredential $cred1

## 詳細描述

**Test-CsDialInConferencing** Cmdlet 是 Lync Server「綜合交易」的範例。Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員手動執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

綜合交易通常以兩種不同的方式進行。許多系統管理員會使用 **CsHealthMonitoringConfiguration** Cmdlet 來設定其每個登錄器集區的測試使用者。這些測試使用者是已預先設定要搭配使用綜合交易的一對使用者。(通常這些使用者是測試帳戶，而不是屬於真正使用者的帳戶)。利用對集區設定的測試使用者，系統管理員只要對集區執行綜合交易，無須指定測試中牽涉之使用者帳戶的識別身分 (並提供其認證)。

另一種方式是系統管理員會使用真正的使用者帳戶來執行綜合交易。例如，如果兩個使用者無法交換立即訊息，則系統管理員可以使用這兩個有問題的使用者帳戶 (而非一對測試帳戶) 執行綜合交易，然後嘗試診斷及解決問題。如果您決定使用實際的使用者帳戶執行綜合交易，則必須提供每位使用者的登入名稱和密碼。

嘗試將測試使用者登入系統以使 **Test-CsDialInConferencing** Cmdlet 運作 (如果您正在使用測試使用者，**Test-CsDialInConferencing** Cmdlet 將使用為該集區設定的第一個測試帳戶)。如果登入成功，Cmdlet 接著會使用該使用者的認證與權限，嘗試使用可用的電話撥入式會議存取號碼。每個撥入嘗試的成功或失敗皆會進行記錄，然後從 Lync Server 登出該測試使用者。

**Test-CsDialInConferencing** Cmdlet 只會確認可以建立適當的連線。Cmdlet 不會實際撥打任何電話或建立任何其他使用者可以加入的電話撥入式會議。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsDialInConferencing** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDialInConferencing"}

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
<td><p>System.String</p></td>
<td><p>要測試之集區的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>要測試之使用者帳戶的使用者認證物件。傳送至 UserCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。如果您使用狀況監視組態設定來進行測試，則此參數不是必要參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.SyntheticTransactions.SipSyntheticTransaction+AuthenticationMechanism</p></td>
<td><p>測試中所使用的驗證類型。允許的值為：</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>附註：指定變數名稱時，請勿在前面加上 $ 字元。若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似下列的命令：</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。如果登錄器使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPstnPhoneNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>PSTN 電話的電話號碼，將用於確認 PSTN 使用者可以加入電話撥入式會議。例如：</p>
<p>-TargetPstnPhoneNumber &quot;+12065551219&quot;</p>
<p>請注意，只有當您使用 VerifyConferenceJoinType 參數時，才應加入 TargetPstnPhoneNumber。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要測試之使用者帳戶的 SIP 位址。例如：-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。UserSipAddress 參數必須參考與 UserCredential 相同的使用者帳戶。如果您使用狀況監視組態設定來進行測試，則此參數不是必要參數。</p></td>
</tr>
<tr class="even">
<td><p><em>VerifyConferenceJoin</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，請確認您可以使用 PSTN 電話來加入電話撥入式會議。執行此測試時，您可以選擇性地加入 TargetPstnPhoneNumber。如果加入此參數，TargetPstnPhoneNumber 就必須指定要用來加入會議的 PSTN 電話。如果未加入 TargetPstnPhoneNumber，則 <strong>Test-CsDialInConferencing</strong> Cmdlet 將使用預先指派給適當電話撥入式會議區域的撥號號碼。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsDialInConferencing** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsDialInConferencing** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsAVConference](test-csavconference.md)

