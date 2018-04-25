---
title: Test-CsWebApp
TOCTitle: Test-CsWebApp
ms:assetid: 0333a4a5-9bd5-4a45-aea8-e7af1a394ec3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh689989(v=OCS.15)
ms:contentKeyID: 49289923
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsWebApp

 

_**上次修改主題的時間：** 2015-03-09_

確認通過驗證的使用者可以使用 Lync Web App 加入 Lync Server 會議。 Lync Server 2010 中已導入此 Cmdlet。

此 Cmdlet 已不再適用於內部部署版本的 Lync Server 2013。系統管理員應改用 [Test-CsUcwaConference](test-csucwaconference.md) Cmdlet 來執行這些測試。

## 語法

    Test-CsWebApp -User2Credential <PSCredential> -User2SipAddress <String> -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsWebApp -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsWebApp -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

範例 1 會確認針對 atl-cs-001.litwareinc.com 集區設定的一對測試使用者是否可以使用 Lync Web App 加入會議。只有已使用 **CsHealthMonitoringConfiguration** Cmdlet 設定集區的測試使用者，此命令才會成功。

    Test-CsWebApp -TargetFqdn atl-cs-001.litwareinc.com

## 範例 2

範例 2 所示的命令會確認使用者 Ken Myer 和 Pilar Ackerman 是否可以使用 Lync Web App 加入會議。為了使用實際的使用者帳戶，範例中的前兩個命令會使用 Get-Credential Cmdlet 建立兩位使用者 (litwareinc\\kenmyer 和 litwareinc\\pilar) 的 Windows PowerShell 命令列介面認證物件。這些認證物件 (儲存在變數 $cred1 和 $cred2 中) 接著會做為範例中最後一個命令之 UserCredential 和 User2Credential 參數的參數值。除了使用者認證參數，還加入了 UserSipAddress 和 User2SipAddress 參數，以及測試中所使用之兩個使用者帳戶的 SIP 位址。

    $cred1 = Get-Credential "litwareinc\kenmyer"
    $cred2 = Get-Credential "litwareinc\pilar"
    
    Test-CsWebApp -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred1 -User2SipAddress "sip:pilar@litwareinc.com" -User2Credential $cred2

## 詳細描述

**Test-CsWebApp** Cmdlet 可讓系統管理員確認經驗證的使用者可運用 Lync Web App 以加入會議。當您執行 **Test-CsWebApp** Cmdlet 時，Cmdlet 會嘗試使用 Web 票證服務為一組成對測試使用者取得 Web 票證。若能取得票證，且測試使用者通過驗證，則 **Test-CsWebApp** Cmdlet 接著會嘗試使用 Lync Web App 連線至 Lync Server。完成連線後，Cmdlet 會接著嘗試為立即訊息、應用程式共用及資料共同作業建立個別會議。

許多系統管理員會使用 **CsHealthMonitoringConfiguration** Cmdlet 來設定其每個登錄器集區的測試使用者。這些測試使用者代表已預先設定要搭配綜合交易使用的一對使用者帳戶 (這些通常是測試帳戶，而不是屬於真正使用者的帳戶)。如果針對集區設定測試使用者，系統管理員可以對該集區執行 **Test-CsWebApp** Cmdlet，而不需要指定測試中涉及的使用者帳戶 Identity (並提供其認證)。

或者，系統管理員可以使用實際的使用者帳戶來執行 **Test-CsWebApp** Cmdlet。如果您決定使用實際的使用者帳戶進行測試，則必須提供每個帳戶的登入名稱和密碼。

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
<td><p>要測試之集區的完整網域名稱 (FQDN)。例如：</p>
<p>-TargetFqdn atl-cs-001.litwareinc.com</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>必要</p></td>
<td><p>字串</p></td>
<td><p>Reach 伺服器的統一資源識別元 (URI)。例如：</p>
<p>-TargetUri &quot;https://atl-cs-001.litwareinc.com/reach&quot;</p>
<p>您無法在同一個命令中同時使用 TargetUri 參數和 TargetFqdn 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>User2Credential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的使用者認證物件。傳遞到 User2Credential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，這個程式碼會傳回的認證物件，並將該物件以名稱為 $y 的變數儲存：</p>
<p>$y = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p></td>
</tr>
<tr class="even">
<td><p><em>User2SipAddress</em></p></td>
<td><p>必要</p></td>
<td><p>字串</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的 SIP 位址。例如：</p>
<p>-User2SipAddress &quot;sip:pilar@litwareinc.com&quot;</p>
<p>如果使用透過 <strong>CsHealthMonitoringConfiguration</strong> Cmdlet 設定的測試使用者執行測試，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的使用者認證物件。傳遞到 UserCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，這個程式碼會傳回使用者 litwareinc\pilar 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>選用</p></td>
<td><p>SipSyntheticTransaction + AuthenticationMechanism</p></td>
<td><p>執行測試時所使用的驗證類型。允許的值為：</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>若使用，則會促使 <strong>Test-CsWebApp</strong> Cmdlet 測試 Reach 伺服器的外部 Web 轉送。若未使用此參數，則 Cmdlet 會測試內部 Web 轉送。Web 轉送可做為內部網路與網際網路之間的中繼。</p></td>
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
<td><p><em>UserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>字串</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的 SIP 位址。例如：</p>
<p>-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>如果使用透過 CsHealthMonitoringConfiguration Cmdlet 設定的測試使用者執行測試，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>選用</p></td>
<td><p>PSCredential</p></td>
<td><p>要在測試中使用之使用者帳戶的使用者認證物件。傳送至 UserCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>如果指定了 TargetUri 參數或 UserSipAddress/User2SipAddress 參數，而且執行命令的電腦不具伺服器憑證，則此為必要參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Test-CsWebApp** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

