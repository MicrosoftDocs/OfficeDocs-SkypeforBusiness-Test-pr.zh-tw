---
title: Test-CsUcwaConference
TOCTitle: Test-CsUcwaConference
ms:assetid: 4e01c4d6-7b81-4932-a8e1-4d14989b71bd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619178(v=OCS.15)
ms:contentKeyID: 49290871
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsUcwaConference

 

_**上次修改主題的時間：** 2015-03-09_

測試一組使用者排程、加入，並使用整合通訊 Web API (UCWA) 進行線上會議的功能。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsUcwaConference -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-OrganizerSipAddress <String>] [-ParticipantSipAddress <String>] [-RegistrarPort <Int32>] <COMMON PARAMETERS>

    Test-CsUcwaConference -OrganizerCredential <PSCredential> -OrganizerSipAddress <String> -ParticipantCredential <PSCredential> -ParticipantSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsUcwaConference [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-ParticipantSipAddress <String>]

## 範例

## 範例 1

範例 1 所示的命令可確認一對測試使用者能夠參與集區 atl-cs-001.litwareinc.com 上的 UCWA 會議。請注意，如果您未針對 atl-cs-001.litwareinc.com 預先定義一對狀況監控組態的測試使用者，這個命令將會失敗。

    Test-CsUcwaConference -TargetFqdn "atl-cs-001.litwareinc.com"

## 範例 2

範例 2 所示的命令會測試一組使用者 (litwareinc\\pilar 和 litwareinc\\kenmyer) 參與 UCWA 會議的功能。為達成此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet 建立一個包含使用者 Pilar Ackerman 之名稱與密碼的 Windows PowerShell 命令列介面認證物件。(因為已加上登入名稱 litwareinc\\pilar 做為參數，所以產生的 \[ Windows PowerShell 認證要求\] 對話方塊將只會要求系統管理員輸入 Pilar Ackerman 帳戶的密碼。) 然後，產生的認證物件會以名稱為 $cred1 的變數儲存。第二個命令會執行相同的程序，但這次會傳回 Ken Myer 帳戶的認證物件。

手邊有了這兩個認證物件之後，此範例中的第三個命令會判斷這兩個使用者是否能參與 UCWA 會議。為了執行此工作，會呼叫 **Test-CsUcwaConference** Cmdlet 並搭配下列參數：TargetFqdn (登錄器集區的 FQDN)、OrganizerSipAddress (會議召集人的 SIP 位址)、OrganizerCredential ( Windows PowerShell 物件，包含同一位使用者的認證)、ParticipantSipAddress (另一位測試使用者的 SIP 位址)，以及 ParticipantCredential ( Windows PowerShell 命令列介面物件，包含另一位使用者的認證)。

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsUcwaConference -TargetFqdn atl-cs-001.litwareinc.com -OrganizerSipAddress "sip:pilar@litwareinc.com" -OrganizerCredential $cred1 -ParticipantSipAddress "sip:kenmyer@litwareinc.com" -ParticipantCredential $cred2

## 詳細描述

**Test-CsUcwaConference** Cmdlet 可驗證一組測試使用者是否能夠排程、加入並使用整合通訊 Web API (UCWA) 進行線上會議。為達成此目的，Cmdlet 使用 Lync Server Web 票證服務以驗證兩個測試使用者，並透過 Lync Server 註冊。接著，Cmdlet 會使用召集人認證召開會議，然後邀請參與者加入會議。 **Test-CsUcwaConference** Cmdlet 可在有人加入會議後，驗證該使用者是否能夠進行像是交換立即訊息和執行集區等事項，然後終止會議，再將兩個測試使用者解除註冊。

**Test-CsUcwaConference** Cmdlet 也可以用來判斷匿名的使用者是否能參與線上會議。

請注意，除非集區已安裝 UCWA，否則不可對 Microsoft Lync Server 2010 集區執行 **Test-CsUcwaConference** Cmdlet。如果尚未安裝 UCWA，則無法呼叫 **Test-CsUcwaConference** Cmdlet。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsUcwaConference"}

**Lync Server 控制台：** **Test-CsUcwaConference** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>OrganizerCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>做為會議召集人之使用者帳戶的使用者認證物件。傳遞到 OrganizerCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您是在集區的狀況監控組態設定下執行測試，則不需要召集人認證。</p></td>
</tr>
<tr class="even">
<td><p><em>ParticipantCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>做為會議參與者的使用者帳戶可用的使用者認證物件。傳遞到 ParticipantCredential 的值必須是使用 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\pilar 的認證物件，並將該物件儲存於名為 $y 的變數中：</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您是在集區的狀況監控組態設定下執行測試，則不需要參與者認證。</p></td>
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
<td><p>執行測試時所使用的驗證類型。允許的值為：</p>
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
<td><p><em>OrganizerSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>會議召集人的 SIP 位址。例如：-OrganizerSipAddress &quot;sip:pilar@litwareinc.com&quot;。OrganizerSIPAddress 參數必須與 OrganizerCredential 參考相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注意：指定變數名稱時，請勿在前面加上 $ 字元。</p>
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
<td><p><em>ParticipantSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>會議參與者的 SIP 位址。例如：-ParticipantSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。 ParticipantSIPAddress 參數必須參考與 ParticipantCredential 相同的使用者帳戶。</p>
<p>如果您是使用集區的健康狀況監控組態設定執行測試，便不需要 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。如果登錄器使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Test-CsUcwaConference** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsUcwaConference** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.WebTaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsASConference](test-csasconference.md)  
[Test-CsDataConference](test-csdataconference.md)  
[Test-CsAVConference](test-csavconference.md)

