---
title: Test-CsAudioConferencingProvider
TOCTitle: Test-CsAudioConferencingProvider
ms:assetid: 9e00081e-5825-4ee9-a838-3c91ad054589
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205117(v=OCS.15)
ms:contentKeyID: 49291817
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAudioConferencingProvider

 

_**上次修改主題的時間：** 2015-03-09_

測試以查看使用者是否可以連線至其音訊會議提供者。音訊會議提供者是提供組織會議服務的第三方公司。總而言之，音訊會議提供者可讓處於異地且未連線至公司網路或網際網路的使用者，參與會議的語音部分。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsAudioConferencingProvider -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsAudioConferencingProvider -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAudioConferencingProvider [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-DialoutUserCredential <PSCredential>] [-DialoutUserSipAddress <String>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## 範例

## 範例 1

範例 1 會檢查針對集區 atl-cs-001.litwareinc.com 定義的測試使用者是否能夠連線至其音訊會議提供者。此命令需要至少有一位針對集區定義的測試使用者。如果沒有任何針對 atl-cs-001.litwareinc.com 定義的測試使用者，則此命令會失敗，因為 **Test-CsAudioConferencingProvider** Cmdlet 會不知道測試要採用哪位使用者。如果尚未針對集區定義測試使用者，則必須加入 UserSipAddress 參數以及此命令在驗證音訊會議提供者連線時應採用的使用者帳戶認證。

    Test-CsAudioConferencingProvider -TargetFqdn atl-cs-001.litwareinc.com

## 範例 2

範例 2 所示的命令會測試特定使用者 (litwareinc\\kenmyer) 連線至其音訊會議提供者的能力。為達成此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet，以建立一個包含使用者 Ken Myer 之名稱與密碼的 Windows PowerShell 命令列介面認證物件。(因為已加入登入名稱 litwareinc\\kenmyer 做為參數，所以系統管理員只需要在 \[ Windows PowerShell 認證要求\] 對話方塊輸入 Ken Myer 帳戶的密碼)。產生的認證物件會儲存於名為 $credential 的變數中。

接著，第二個命令會檢查此使用者是否可以連線至其音訊會議提供者。為了執行此工作，會呼叫 **Test-CsAudioConferencingProvider** Cmdlet 並搭配下列三個參數：TargetFqdn (登錄器集區的 FQDN)、UserCredential (包含 Ken Myer 使用者認證的 Windows PowerShell 物件) 及 UserSipAddress (對應至所提供使用者認證的 SIP 位址)。

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAudioConferencingProvider -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

## 詳細描述

音訊會議提供者是提供組織會議服務的第三方公司。總而言之，音訊會議提供者可讓處於異地且未連線至公司網路或網際網路的使用者，參與會議的語音部分。音訊會議提供者通常會提供高階服務，例如現場翻譯、記錄及現場個別會議總機服務。

**Test-CsAudioConferencingProvider** Cmdlet 可用於確認使用者是否能夠連線至其音訊會議提供者。請注意，您可以使用兩種方式來執行此 Cmdlet。許多系統管理員會使用 CsHealthMonitoringConfiguration Cmdlet 針對每個登錄器集區設定測試使用者。這些測試使用者代表已預先設定要搭配使用綜合交易的一對使用者帳戶。(通常這些使用者是測試帳戶，而不是屬於真正使用者的帳戶)。如果已針對集區設定測試使用者，系統管理員只要針對該集區執行 **Test-CsAudioConferencingProvider** Cmdlet，無須指定測試中牽涉之使用者帳戶的識別身分 (並提供其認證)。

或者，系統管理員可以使用實際的使用者帳戶來執行 **Test-CsAudioConferencingProvider** Cmdlet。如果您決定使用實際的使用者帳戶進行測試，則必須提供該帳戶的登入名稱和密碼。

請注意，如果尚未指派音訊會議提供者給 **Test-CsAudioConferencingProvider** Cmdlet 所採用的使用者，則測試會失敗。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsAudioConferencingProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAudioConferencingProvider"}

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
<td><p>字串</p></td>
<td><p>要測試之集區的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試之帳戶的使用者認證物件。傳送給 UserCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參照。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果命令使用以 CsHealthMonitoringConfiguration Cmdlet 所設定的測試使用者，則不需要此參數。</p></td>
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
<td><p><em>DialoutUserCredential</em></p></td>
<td><p>選用</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試之撥出使用者帳戶的使用者認證物件。傳遞給 DialoutUserCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參照。例如，下列程式碼會傳回使用者 litwareinc\pilar 的認證物件，並將該物件儲存在名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>DialoutUserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>要測試之撥出使用者帳戶的 SIP 位址。例如：-DialoutUserSipAddress &quot;sip:pilar@litwareinc.com&quot;。DaloutUserSipAddress 參數必須與 DialoutUserCredential 參考相同的使用者帳戶。</p></td>
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
<td><p>字串</p></td>
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
<td><p>字串</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。如果登錄器使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>如有指定此參數，會測試 Join Launcher 參與會議的能力。Join Launcher 可用來協助行動裝置使用者 (進而協助 Mobility Service 使用者) 參與會議。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>要測試之使用者帳戶的 SIP 位址。例如：-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。UserSipAddress 參數必須參考與 UserCredential 相同的使用者帳戶。</p>
<p>如果命令使用以 CsHealthMonitoringConfiguration Cmdlet 所設定的測試使用者，則不需要此參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Test-CsAudioConferencingProvider** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsAudioConferencingProvider** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

