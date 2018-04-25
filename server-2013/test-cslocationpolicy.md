---
title: Test-CsLocationPolicy
TOCTitle: Test-CsLocationPolicy
ms:assetid: 49f7d148-d46d-4bcc-af9d-6a3a0fdde8ee
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425962(v=OCS.15)
ms:contentKeyID: 49290825
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLocationPolicy

 

_**上次修改主題的時間：** 2015-03-09_

根據參數值中指定的條件執行測試，以決定所要使用的位置原則。位置原則所含的設定可以指定是否要套用增強型 9-1-1 (E9-1-1)，以及增強型 9-1-1 (E9-1-1) 的套用方式。E9-1-1 可協助接聽 911 緊急通話的人員判別來電者的地理位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsLocationPolicy -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsLocationPolicy -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsLocationPolicy [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Subnet <String>]

## 範例

## 範例 1

此範例會判斷目前使用者 (或目前設定的使用者) 的位置原則。TargetFqdn 為必要項。

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com 

## 範例 2

範例 2 中的第一行是呼叫 Windows PowerShell **Get-Credential** Cmdlet。此 Cmdlet 會擷取使用者認證，並當做安全性物件將其傳回。唯一提供給此 Cmdlet 的參數為使用者識別碼。執行此 Cmdlet 會開啟一個對話方塊，其中會預先填入提供的使用者識別碼，而且會有一個可讓您輸入使用者密碼的文字方塊。這些使用者認證會儲存為變數 $cred。

第 2 行會呼叫 **Test-CsLocationPolicy** Cmdlet。與範例 1 類似，我們提供目標 FQDN。不過，在此範例中使用的不是預先設定的使用者，我們會針對 SIP 位址為 kenmyer@litwareinc.com 的使用者執行測試。我們將該值 (含 sip:首碼) 傳遞至 UserSipAddress 參數，而該使用者的認證 (以 $cred 變數儲存) 會傳遞至 UserCredential 參數。

    $cred = Get-Credential "litwareinc\kenmyer"
    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred -UserSipAddress "sip:kenmyer@litwareinc.com"

## 範例 3

此範例和範例 2 類似，但不會指定使用者認證。未指定使用者認證呼叫 **Test-CsLocationPolicy** Cmdlet 時，執行這個 Cmdlet 的電腦上的伺服器憑證會用來驗證及探索使用者的位置原則。如果電腦沒有伺服器憑證，您必須依範例 2 所示指定憑證。呼叫 **Get-CsCertificate** Cmdlet，藉此找出電腦上是否有伺服器憑證。

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com"

## 範例 4

此範例會判斷子網路 ID 為 172.15.11.0 之子網路的位置原則。如果子網路未與位置原則相關聯，則會擷取目前設定之使用者的位置原則。

注意：位置原則是在子網路上設定，方法為，將 **Set-CsNetworkSite** Cmdlet 的 LocationPolicy 參數設為位置原則識別碼，然後將 **Set-CsNetworkSubnet** Cmdlet 的 NetworkSiteId 參數設為該網站的識別碼。例如：

Set-CsNetworkSite Portland –LocationPolicy Reno

Set-CsNetworkSubnet 175.15.11.0 –NetworkSiteID Portland

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -Subnet 172.15.11.0

## 詳細描述

位置原則用來套用與 E9-1-1 功能和用戶端位置相關的設定。位置原則會判斷使用者是否已啟用 E9-1-1，如果是，則會決定緊急電話的行為。例如，您可以使用位置原則來定義組成緊急電話的數字 (在美國為 911)、是否應自動告知公司的安全部門，以及應如何路由傳送來電。此 Cmdlet 會傳回在特定集區、子網路、交換器、或無線存取點上的特定用戶端撥打電話時，將使用之位置原則的資訊。

如果此 Cmdlet 的呼叫中未指定使用者，則將測試目前設定的使用者。若要尋找目前設定的使用者，請呼叫 **Get-CsHealthMonitoringConfiguration** Cmdlet。若要設定已設定的使用者，請呼叫 **Set-CsHealthMonitoringConfiguration** Cmdlet。

如果找到使用者或子網路的位置原則，測試將會成功。預設傳回的資訊包括位置原則的名稱 (如果指派個別使用者原則) 以及使用者或子網路是否啟用 E9-1-1。加入 Windows PowerShell 一般參數詳細資訊以擷取關於測試的其他資訊。

您可以針對使用者或網路子網路測試位置原則。如果您針對子網路執行測試 (透過指定 Subnet 參數的值)，Cmdlet 就會嘗試解析該子網路的位置原則。如果該子網路未指派位置原則，則會擷取已設定之使用者的位置原則。如果成功擷取子網路原則，則輸出將包含開頭為 subnet-tagid 的 LocationPolicyTagID 值。如果找不到子網路的位置原則，則 LocationPolicyTagID 的開頭為 user-tagid。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsLocationPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsLocationPolicy"}

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
<td><p>指定使用者或子網路所屬之集區的完整網域名稱 (FQDN) (若未指定使用者，則會假設為預先設定或目前的使用者)。</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>包含正在測試其位置原則之使用者帳戶的使用者 ID 和密碼的物件。您可以呼叫 <strong>Get-Credential</strong> Cmdlet、填入適當的資訊，並將輸出儲存為變數以擷取認證物件。</p></td>
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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注意：指定變數名稱時，請勿在前面加上 $ 字元。若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似下列的命令：</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，您可使用下列語法，將輸出儲存於名為 $TestOutput 的變數中：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>登錄器服務的連接埠號碼。</p></td>
</tr>
<tr class="even">
<td><p><em>Subnet</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>您想要測試其位置原則之網路子網路的 ID (IP 位址)。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>您想要測試其位置原則之使用者的 SIP 位址。其格式必須為 sip:&lt;使用者識別碼&gt;，例如 sip:kenmyer@litwareinc.com。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Test-CsLocationPolicy** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Set-CsLocationPolicy](set-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Grant-CsLocationPolicy](grant-cslocationpolicy.md)  
[Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)  
[Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)  
[Set-CsNetworkSite](set-csnetworksite.md)

