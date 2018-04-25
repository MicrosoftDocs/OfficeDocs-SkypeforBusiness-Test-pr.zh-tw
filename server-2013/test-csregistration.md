---
title: Test-CsRegistration
TOCTitle: Test-CsRegistration
ms:assetid: 9e38cb36-c97a-43f2-97fe-64759f663be2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412737(v=OCS.15)
ms:contentKeyID: 49291838
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsRegistration

 

_**上次修改主題的時間：** 2015-03-09_

測試使用者登入 Lync Server 的能力。**Test-CsRegistration** Cmdlet 是一種「綜合交易」︰用於監控健康狀況與效能之一般 Lync Server 活動的模擬。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsRegistration -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsRegistration -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsRegistration [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

範例 1 會針對集區 atl-cs-001.litwareinc.com 測試登錄器服務。只有已針對集區 atl-cs-001.litwareinc.com 定義測試使用者時，此命令才有作用。如果已定義，則命令會判斷第一個測試使用者是否可以登入 Lync Server。

如果尚未定義測試使用者，則此命令會因為不知道登入的是哪個使用者而失敗。如果尚未針對集區定義測試使用者，則必須加入 UserSipAddress 參數以及此命令在嘗試登入時應使用的使用者認證。

    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com 

## 範例 2

範例 2 所示的命令會測試特定使用者 (itwareinc\\pilar) 登入 Lync Server 的能力。為達此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet 建立一個包含使用者 Pilar Ackerman 之名稱與密碼的 Windows PowerShell 認證物件。(因為已加上登入名稱 litwareinc\\pilar 做為參數，所以系統管理員只需要在 \[Windows PowerShell 認證要求\] 對話方塊輸入 Pilar Ackerman 帳戶的密碼)。然後，產生的認證物件會以名稱為 $cred1 的變數儲存。

接著，第二個命令會檢查此使用者是否可以登入集區 atl-cs-001.litwareinc.com。為了執行此工作，會呼叫 **Test-CsRegistration** Cmdlet 並搭配下列三個參數：TargetFqdn (登錄器集區的 FQDN)、UserCredential (包含 Pilar Ackerman 使用者認證的 Windows PowerShell 物件) 及 UserSipAddress (對應至所提供使用者認證的 SIP 位址)。

    $cred1 = Get-Credential "litwareinc\pilar"
    
    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:pilar@litwareinc.com"

## 詳細描述

**Test-CsRegistration** Cmdlet 是 Lync Server「綜合交易」的範例。Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員手動執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

綜合交易通常以兩種不同的方式進行。許多系統管理員會使用 CsHealthMonitoringConfiguration Cmdlet 來設定其每個登錄器集區的測試使用者。這些測試使用者是已預先設定要搭配使用綜合交易的一對使用者。(通常這些使用者是測試帳戶，而不是屬於真正使用者的帳戶)。利用對集區設定的測試使用者，系統管理員只要對集區執行綜合交易，無須指定測試中牽涉之使用者帳戶的識別身分 (並提供其認證)。

或者，系統管理員可以使用實際的使用者帳戶執行綜合交易。例如，如果有兩個使用者無法交換立即訊息，系統管理員可以使用上述兩個使用者帳戶 (而非一組測試帳戶) 執行綜合交易，然後嘗試診斷並解決問題。如果您決定使用實際的使用者帳戶執行綜合交易，則必須提供每位使用者的登入名稱和密碼。

**Test-CsRegistration** Cmdlet 可讓您驗證組織中的使用者是否可以登入 Lync Server。為了執行這項檢查，**Test-CsRegistration** Cmdlet 需要一個測試帳戶。若您已為所要測試的集區設定了測試使用者，便無須指定帳戶。**Test-CsRegistration** Cmdlet 會自動使用指派給該集區的第一個測試帳戶 (如需詳細資訊，請參閱 [New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md) Cmdlet 說明主題)。或者，您可以使用未指派給集區的帳戶進行測試。這可讓您即使未設定測試使用者，也可執行測試。這同時也可讓您測試特定使用者是否能登入 Lync Server (若您選擇使用此方法，必須提供要測試帳戶的使用者名稱和密碼)。

當您執行 **Test-CsRegistration** Cmdlet 時，此 Cmdlet 會嘗試將測試使用者登入到 Lync Server，如果成功，則會中斷測試使用者與系統的連線。在此期間都不會有任何使用者介入，也不會影響任何實際的使用者。例如，假設測試帳戶 sip:kenmyer@litwareinc.com 對應到擁有 Lync Server 實際帳戶的實際使用者。在該情況下，測試將會在不干擾實際的 Ken Myer 的情況下進行。當 Ken Myer 測試帳戶從系統登出時，Ken Myer 這個人仍然維持登入狀態。

加入 Verbose 參數可讓您取得 **Test-CsRegistration** Cmdlet 為了完成測試所採取之所有動作的詳細說明。

誰可以執行這個 Cmdlet：若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsRegistration"}

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
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試之帳戶的使用者認證物件。傳送至 UserCredential 的值必須是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參考。例如，這個程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件以名稱為</p>
<p>$x 的變數儲存：$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。如果您是在集區的運作狀況監視組態設定下執行測試，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>選用</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>測試中所使用的驗證類型。允許的值為：</p>
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
<p>注意：指定變數名稱時，請勿在前面加上 $ 字元。若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似如下的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似如下的命令：</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如有指定此參數，會將 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>登錄程式服務所使用的 SIP 連接埠。如果登錄程式使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要測試之使用者帳戶的 SIP 位址；例如：-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。UserSipAddress 參數必須參考與 UserCredential 相同的使用者帳戶。如果您是在集區的運作狀況監視組態設定下執行測試，則不需要此參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsRegistration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsRegistration** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

