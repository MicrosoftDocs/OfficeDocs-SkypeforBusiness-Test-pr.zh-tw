---
title: Test-CsGroupExpansion
TOCTitle: Test-CsGroupExpansion
ms:assetid: e41db33d-d028-4171-9418-ec04885be2fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399009(v=OCS.15)
ms:contentKeyID: 49292610
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsGroupExpansion

 

_**上次修改主題的時間：** 2015-03-09_

測試使用者能否展開群組。 Lync Server 可讓使用者將 Active Directory 通訊群組設為連絡人。當您「展開」群組時，會顯示每個群組成員的名稱與目前狀態資訊。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsGroupExpansion -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsGroupExpansion -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsGroupExpansion -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -GroupEmailAddress <String> [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

範例 1 所示的命令可連接至登錄器集區 atl-cs-001.litwareinc.com，以確認群組展開。該命令使用 FinanceGroup@litwareinc.com 群組來進行測試。

    Test-CsGroupExpansion -TargetFqdn atl-cs-001.litwareinc.com -GroupEmailAddress FinanceGroup@litwareinc.com 

## 詳細描述

使用者有時需要定期與 Active Directory 通訊群組的所有成員進行通訊對使用者而言是極為平常的事情。例如，該群組可能包含某小組的所有成員，或指派給某特定專案的所有人員。有鑑於此， Lync Server 可讓您將 Active Directory 通訊群組設定為連絡人。若您這麼做，只要處理給群組而非該群組每個個別成員的訊息，您便可在之後將相同的立即訊息傳送給所有的群組成員。

也有可能您需要與該群組某些個人進行通訊 (或檢查其目前狀態)。群組展開可讓您快速輕鬆檢視所有群組成員及其目前狀態。此外，您也可以選取一或多個群組成員，然後將立即訊息傳送給這些成員，而非所有群組成員。

您可以使用 **Set-CsWebServiceConfiguration** Cmdlet 來啟用或停用群組展開。若啟用群組展開，您可以決定是否藉由執行 **Test-CsGroupExpansion** Cmdlet，來使該功能運作。使用此 Cmdlet，您可以使用群組的電子郵件地址來指定 Active Directory 通訊群組。 **Test-CsGroupExpansion** Cmdlet 接著會使用群組展開來擷取群組成員資格，並將擷取的清單與您提供的群組電子郵件地址的成員資格進行比較。如果這兩份清單相符，則群組展開會正確運作。

請注意，您可以下列兩種不同的方式測試群組展開：測試服務本身，或測試相關聯的 Web 服務。

誰可以執行這個 Cmdlet：若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsGroupExpansion"}

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
<td><p><em>GroupEmailAddress</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>目標通訊群組成員的電子郵件地址。例如：-GroupEmailAddress &quot;FinanceGroup@litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要測試之群組展開的登錄器集區完整網域名稱 (FQDN)。例如：-TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p>請注意，您無法在同一個命令中同時使用 TargetUri 參數和 TargetFqdn 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetUri</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>群組展開 Web 服務的統一資源識別元 (URI)。例如：-TargetUri &quot;https://atl-cs-001.litwareinc.com/groupexpansion&quot;。</p>
<p>請注意，您無法在同一個命令中同時使用 TargetUri 參數和 TargetFqdn 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>要在測試中使用之使用者帳戶的使用者認證物件。傳送至 UserCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行這個命令時，您將需要提供使用者密碼。</p>
<p>如果您在登入使用者認證之下執行測試並使用 TargetFqdn 參數，則不需要使用者認證。若您使用 TargetUri 參數則需要使用者認證。</p></td>
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
<td><p><em>External</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您確認外部使用者可使用群組展開。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
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
<td><p>System.Strkng</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。如果登錄器使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要在測試中使用之使用者的 SIP 位址。如果未指定此參數，則 <strong>Test-CsGroupExpansion</strong> Cmdlet 將會使用登入使用者的帳戶來進行檢查。</p></td>
</tr>
<tr class="even">
<td><p><em>WebCredential</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>包含用於存取位置資訊服務的使用者認證物件。此物件可透過呼叫 <strong>Get-Credential</strong> Cmdlet 並提供適當的認證來擷取。</p>
<p>如果指定了 TargetUri 和 UserSipAddress 參數，而且執行命令的電腦不具伺服器憑證，則此為必要參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsGroupExpansion** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsGroupExpansion** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsAddressBookService](test-csaddressbookservice.md)  
[Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

