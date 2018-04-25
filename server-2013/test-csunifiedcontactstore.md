---
title: Test-CsUnifiedContactStore
TOCTitle: Test-CsUnifiedContactStore
ms:assetid: 0aeca874-87da-4bc8-b2f2-c9c7e0d86883
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204662(v=OCS.15)
ms:contentKeyID: 49290040
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsUnifiedContactStore

 

_**上次修改主題的時間：** 2015-03-09_

確認是否可以透過統一連絡人存放區存取使用者的連絡人。統一連絡人存放區可讓使用者維護一組連絡人，方便使用 Lync 2013、Outlook 及/或 Outlook Web Access 加以存取。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsUnifiedContactStore -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsUnifiedContactStore -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsUnifiedContactStore [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

範例 1 所示的命令會驗證是否能夠在統一連絡人存放區中找到的連絡人。為達成此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet，以建立使用者 litwareinc\\kenmyer 的 Windows PowerShell 命令列介面認證物件。請注意，您必須提供此帳戶的密碼，才能建立有效的認證物件，並確定 **Test-CsUnifiedContactStore** Cmdlet 可以執行這項檢查。

範例中的第二個命令會使用所提供的證證物件 ($x) 和的 SIP 位址，以判斷是否能夠在統一連絡人存放區中找到他的連絡人。

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsUnifiedContactStore -TargetFqdn "atl-cs-001.litwareinc.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

## 詳細描述

Lync Server 2013 中所導入的統一連絡人存放區可讓系統管理員選擇將使用者的連絡人存放在 Microsoft Exchange Server 2013，而不存放在 Lync Server；相對地，使用者也因此而能從 Outlook、Outlook Web Access 及 Lync 2013 存取同一組連絡人 (除此之外，您也可繼續將連絡人存放在 Lync Server 中，讓使用者可以分別維護兩組連絡人：一組供 Outlook 與 Outlook Web Access 使用，一組供 Lync 2013 使用)。

您可以執行 **Test-CsUnifiedContactStore** Cmdlet 確認使用者的連絡人是否已經移到統一連絡人存放區。 **Test-CsUnifiedContactStore** Cmdlet 會使用指定的使用者帳戶，連線到統一連絡人存放區，然後擷取使用者的連絡者。若無連絡人可供擷取，此命令將會失敗，並提示下列訊息："No contacts were received for the user. Verify that contacts exist for the user." (未擷取到該使用者的任何連絡人。請檢查該使用者有無連絡人)。

請注意，若使用者已成功地移轉到統一連絡人存放區，導致其連絡人清單中空無連絡人， **Test-CsUnifiedContactStore** Cmdlet 將會失敗。指定的使用者至少須有一位連絡人， **Test-CsUnifiedContactStore** Cmdlet 才會成功。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsUnifiedContactStore"}

Lync Server 控制台：Lync Server 控制台不提供 **Test-csUnifiedContactStore** Cmdlet 所執行的功能。

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
<td><p>要在測試中使用之使用者帳戶的使用者認證物件。傳送至 UserCredential 的值應該是使用 G<strong>et-Credential</strong> Cmdlet 取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果使用透過 <strong>CsHealthMonitoringConfiguration</strong> Cmdlet 設定的測試使用者執行測試，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>選用</p></td>
<td><p>SipSyntheticTransaction + AuthenticationMechanism</p></td>
<td><p>執行測試時所使用的驗證類型。允許的值為：</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>切換參數</p></td>
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
<td><p>要在測試中使用之使用者的 SIP 位址。例如：</p>
<p>-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>如果使用透過 <strong>CsHealthMonitoringConfiguration</strong> Cmdlet 設定的測試使用者執行測試，則不需要此參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Test-CsUnifiedContactStore** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsUnifiedContactStore** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.WebTaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsUserServicesPolicy](new-csuserservicespolicy.md)  
[Set-CsUserServicesPolicy](set-csuserservicespolicy.md)

