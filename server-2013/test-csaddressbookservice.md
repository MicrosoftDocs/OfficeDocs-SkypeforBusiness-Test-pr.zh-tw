---
title: Test-CsAddressBookService
TOCTitle: Test-CsAddressBookService
ms:assetid: 8398c9ea-eaab-4a4d-9e09-473ea2b27e22
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398661(v=OCS.15)
ms:contentKeyID: 49291513
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAddressBookService

 

_**上次修改主題的時間：** 2015-03-09_

測試使用者是否可以存取代管通訊錄下載 Web 服務的伺服器。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsAddressBookService -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAddressBookService -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsAddressBookService -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

範例 1 會針對 atl-cs-001.litwareinc.com 集區測試通訊錄下載 Web 服務。此命令會使用針對 atl-cs-001.litwareinc.com 集區預先設定的測試使用者來測試通訊錄下載 Web 服務。

    Test-CsAddressBookService -TargetFqdn atl-cs-001.litwareinc.com 

## 範例 2

範例 2 所示的命令也會測試通訊錄下載 Web 服務伺服器的可用性；但在此範例中，命令會以使用者 Ken Myer (litwareinc\\kenmyer) 的認證執行。為達此目的，第一個命令會使用 **Get-Credential** Cmdlet 建立包含使用者 Ken Myer 之名稱與密碼的 Windows PowerShell 認證物件。(因為已加上登入名稱 (litwareinc\\kenmyer) 做為參數，所以 \[Windows PowerShell 認證要求\] 對話方塊將只會要求系統管理員輸入 Ken Myer 帳戶的密碼)。產生的認證物件會儲存在名為 $cred1 的變數中。

第二個命令使用 **Test-CsAddressBookService** Cmdlet，以測試集區 atl-cs-001.litwareinc.com 的通訊錄下載 Web 服務。為了以 Ken Myer 的使用者認證執行此命令，於是加上 UserCredential 參數和參數值 $cred1。此外，Ken 的 SIP 位址必須使用 UserSipAddress 參數來提供。

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAddressBookService -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:kenmyer@litwareinc.com"

## 範例 3

範例 3 顯示如何對 atl-cs-001.litwareinc.com 測試通訊錄下載 Web 服務。為達成此目的，會呼叫 **Test-CsAddressBookService** Cmdlet 並搭配下列兩個參數：TargetUri (指定通訊錄下載 Web 服務的 URI) 和 UserSipAddress (包含要在此測試中使用之使用者帳戶的 Windows PowerShell SIP 位址)。

``` 


Test-CsAddressBookService -TargetUri https://atl-cs-001.litwareinc.com/abs/handler -UserSipAddress "sip:kenmyer@litwareinc.com"
```

## 詳細描述

**Test-CsAddressBookService** Cmdlet 是「綜合交易」的範例。Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或打給位於公用交換電話網路 (PSTN) 的電話。這些測試可由系統管理員手動執行，或由 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 這類應用程式自動執行。

綜合交易通常以兩種不同的方式進行。許多系統管理員會使用 **CsHealthMonitoringConfiguration** Cmdlet 來設定其每個登錄器集區的測試使用者。這些測試使用者是已預先設定要搭配使用綜合交易的一對使用者。(通常這些使用者是測試帳戶，而不是屬於真正使用者的帳戶)。利用針對集區設定的測試使用者，系統管理員可以對集區執行綜合交易，無須指定測試中牽涉之使用者帳戶的識別身分 (並提供其認證)。

另一種方式是系統管理員會使用真正的使用者帳戶來執行綜合交易。例如，如果兩個使用者無法交換立即訊息，則系統管理員可以使用這兩個使用者帳戶 (而非一對測試帳戶) 執行綜合交易，然後嘗試診斷及解決問題。如果您決定使用實際的使用者帳戶執行綜合交易，則必須提供每位使用者的登入名稱和密碼。

**Test-CsAddressBookService** Cmdlet 提供方法可讓您確認使用者是否可以連線至通訊錄下載 Web 服務。當您執行 **Test-CsAddressBookService** Cmdlet 時，此 Cmdlet 會在指定的集區上連線至通訊錄下載 Web 服務，並要求通訊錄檔案的位置。如果通訊錄下載 Web 服務提供該位置，測試將視為成功。如果要求遭到拒絕，測試將視為失敗。

您有兩種不同的方式來測試通訊錄下載 Web 服務：測試服務本身，或測試相關聯的 Web 服務。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsAddressBookService** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAddressBookService"}

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
<td><p>要測試之通訊錄下載 Web 服務的登錄器集區完整網域名稱 (FQDN)。例如：-TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p>您無法在同一個命令中同時使用 TargetUri 參數和 TargetFqdn 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>通訊錄 Web 查詢服務的統一資源識別元 (URI)。例如：-TargetUri &quot;https://atl-cs-001.litwareinc.com/abs/handler&quot;。</p>
<p>您無法在同一個命令中同時使用 TargetUri 參數和 TargetFqdn 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要在測試中使用之使用者帳戶的使用者認證物件。傳送至 UserCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p></td>
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
<td><p><em>External</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>可讓您確認外部使用者是否可使用 通訊錄下載 Web 服務。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
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
<td><p>要在測試中使用之使用者的 SIP 位址。若未指定此參數，則 <strong>Test-CsAddressBookService</strong> 會使用登入的使用者帳戶進行檢查。</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>選用</p></td>
<td><p>PSCredential</p></td>
<td><p>包含用於存取位置資訊服務的使用者認證物件。此物件可透過呼叫 <strong>Get-Credential</strong> Cmdlet 並提供適當的認證來擷取。</p>
<p>如有指定 TargetUri 和 UserSipAddress 參數，且執行命令的電腦不具伺服器憑證，則此為必要參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsAddressBookService** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsAddressBookService** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)  
[Update-CsAddressBook](update-csaddressbook.md)

