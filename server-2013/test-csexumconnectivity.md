---
title: Test-CsExUMConnectivity
TOCTitle: Test-CsExUMConnectivity
ms:assetid: 2eb541d2-5f09-483c-adc2-4abb16391ea5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204784(v=OCS.15)
ms:contentKeyID: 49290469
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsExUMConnectivity

 

_**上次修改主題的時間：** 2015-03-09_

驗證測試使用者是否可以連線至 Exchange Unified Messaging。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsExUMConnectivity -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsExUMConnectivity -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsExUMConnectivity [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

上述的範例會針對 atl-cs-001.litwareinc.com 集區測試 Exchange Unified Messaging 連線。只有已針對 atl-cs-001.litwareinc.com 集區定義測試使用者時，此命令才有作用。如果已定義，則命令會判斷第一個測試使用者是否可以連線至 Unified Messaging。如果尚未設定集區的測試使用者，命令將會失敗。

    Test-CsExUMConnectivity -TargetFqdn "atl-cs-001.litwareinc.com"

## 範例 2

範例 2 所示的命令會為使用者 litwareinc\\kenmyer 測試 Exchange Unified Messaging 連線。為達成此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet，以建立使用者 litwareinc\\kenmyer 的 Windows PowerShell 命令列介面 認證物件。請注意，您必須提供此帳戶的密碼，才能建立有效的認證物件，並確定 **Test-CsExUMConnectivity** Cmdlet 可以執行這項檢查。

範例中的第二個命令會使用所提供的 ($x) 認證物件的使用者的 SIP 位址，來判斷此使用者是否能夠連線至 Exchange Unified Messaging。

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsExUMConnectivity -TargetFqdn "atl-cs-001.litwareinc.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

## 範例 3

範例 3 所示的命令是範例 2 所示命令的變化，但此範例會加入 OutLoggerVariable 參數，以產生 **Test-CsExUMConnectivity** Cmdlet 採取之每個步驟的詳細記錄及步驟的成功或失敗。為達成此目的，會加入 OutLoggerVariable 參數搭配 ExumText 參數值，以將詳細記錄資訊儲存在名為 $ExumTest 的變數中。範例的最後一個命令會使用 ToXML() 方法將記錄資訊轉換為 XML 格式。然後再使用 Out-File Cmdlet，將該 XML 資料寫入名為 C:\\Logs\\ExumTest.xml 的檔案中。

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsExUMConnectivity -TargetFqdn "atl-cs-001.litwareinc.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential -OutLoggerVariable ExumTest
    
    $ExumTest.ToXML() | Out-File C:\Logs\ExumTest.xml

## 詳細描述

**Test-CsExUMConnectivity** Cmdlet 可驗證指定的使用者是否可以連線至 Microsoft Exchange Server 2013 Unified Messaging 服務。請注意，此 Cmdlet 只可驗證是否可連線至該服務，而無法測試服務本身。若要測試 Unified Messaging 服務 (若是執行綜合交易 Cmdlet，只會在使用者信箱中留下語音信箱訊息)，請使用 [Test-CsExUMVoiceMail](test-csexumvoicemail.md) Cmdlet。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsExUMConnectivity"}

**Lync Server 控制台：** **Test-CsExUMConnectivity** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>要測試 Exchange Unified Messaging 連線之集區的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要在測試中使用之使用者帳戶的使用者認證物件。傳送至 UserCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參照。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果使用透過 CsHealthMonitoringConfiguration Cmdlet 設定的測試使用者執行測試，則不需要此參數。</p></td>
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
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。如果登錄器使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要在測試中使用之使用者的 SIP 位址。例如：</p>
<p>-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>如果使用透過 CsHealthMonitoringConfiguration Cmdlet 設定的測試使用者執行測試，則不需要此參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsExUMConnectivity** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsExUMConnectivity** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsExUMVoiceMail](test-csexumvoicemail.md)

