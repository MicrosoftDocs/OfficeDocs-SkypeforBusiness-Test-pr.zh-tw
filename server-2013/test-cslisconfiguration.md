---
title: Test-CsLisConfiguration
TOCTitle: Test-CsLisConfiguration
ms:assetid: 6983d42e-6b93-4365-b0f1-81031d6e251b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398497(v=OCS.15)
ms:contentKeyID: 49291200
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLisConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

測試位置資訊伺服器 (LIS) 的組態。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsLisConfiguration -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsLisConfiguration -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsLisConfiguration -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BssId <String>] [-ChassisId <String>] [-Force <SwitchParameter>] [-Mac <String>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-PortId <String>] [-PortIdSubType <InterfaceAlias | InterfaceName | LocallyAssigned>] [-Subnet <String>]

## 範例

## 範例 1

此範例會測試 FQDN atl-cs-001.litwareinc.com 的 LIS 組態。如果可透過目前使用者權限連線至該 FQDN 的 LIS Web 服務，則為測試成功。如果可找到對應子網路 IP 位址 192.168.0.0 的位置，則會傳回該位置的位址。

若要成功執行此命令，則必須有包含綜合交易使用者的狀況監控組態存在。若要查看狀況監控組態是否存在，請執行 **Get-CsHealthMonitoringConfiguration** Cmdlet。若要建立新的狀況監控組態，請執行 **New-CsHealthMonitoringConfiguration** Cmdlet。

    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0

## 範例 2

此範例與範例 1 完全相同，但增加了 UserSipAddress 參數。若尚未設定任何綜合交易使用者，但執行命令的電腦具備伺服器憑證時，請使用此命令。

    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0 -UserSipAddress sip:kmyer@litwareinc.com

## 範例 3

此範例的第一行會呼叫 Windows PowerShell Cmdlet (**Get-Credential** Cmdlet) 來提示使用者輸入使用者識別碼和密碼。此資訊會以加密方式儲存在變數 $cred 中。

第二行與範例 2 中的命令完全相同，但增加了 UserSipAddress 參數。若尚未設定任何綜合交易使用者，而執行命令的電腦不具伺服器憑證時，請使用此命令。

    $cred = Get-Credential
    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0 -UserSipAddress sip:kmyer@litwareinc.com -UserCredential $cred

## 範例 4

此範例的第一行會呼叫 **Get-Credential** Cmdlet，其會提示使用者輸入使用者識別碼和密碼。此資訊會以加密方式儲存在變數 $cred 中。

第二行會根據遠端使用者的 SIP 位址 (sip:kmyer@litwareinc.com) 來呼叫 Web 服務 URI (https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc) 以測試 LIS 組態，並使用我們在第一行取得的認證，將之傳遞到 WebCredential 參數。如果可透過指定使用者認證連線至該 URI 的 LIS Web 服務，則為測試成功。如果可找到對應子網路 IP 位址 192.168.0.0、MAC 位址 0A-23-00-00-00-AA，或連接埠識別碼 4500 和 ChassisId 0A-23-00-00-00-AA 的位置，則會傳回該位置的位址。

當執行命令的電腦不具伺服器憑證時，請使用此命令。

    $cred = Get-Credential
    Test-CsLisConfiguration -TargetUri https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc -UserSipAddress sip:kmyer@litwareinc.com -WebCredential $cred -Subnet 192.168.0.0 -Mac 0A-23-00-00-00-AA -PortId 4500 -ChassisId 0A-23-00-00-00-AA

## 範例 5

此範例與範例 4 完全相同，但此命令不會使用 WebCredential 參數 (因此不會呼叫 **Get-Credential** Cmdlet)。當執行命令的電腦具備伺服器憑證時，請使用此命令。

    Test-CsLisConfiguration -TargetUri https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc -UserSipAddress sip:kmyer@litwareinc.com -Subnet 192.168.0.0 -Mac 0A-23-00-00-00-AA -PortId 4500 -ChassisId 0A-23-00-00-00-AA

## 詳細描述

此 Cmdlet 決定是否可依據提供的參數資訊，來連絡位置資訊伺服器 (LIS) Web 服務。如果可連絡 Web 服務，並且可找到與任何提供之參數對應的位置，則會視為已通過測試並會顯示位置。即使找不到位置，只要 Web 服務可連絡，測試還是會傳回通過，但不會含有任何位置資訊。此外，如果您呼叫此 Cmdlet，而未提供任何選用參數，只要 Web 服務可連絡，則測試仍然會通過，但是依然不會傳回任何位置資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsLisConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsConfiguration"}

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
<td><p>您要執行測試之伺服器的完整網域名稱 (FQDN) (格式為 server.litwareinc.com)。</p>
<p>除非指定 TargetUri 參數，否則此為必要參數，在此案例中，您無法指定 TargetFqdn。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>位置資訊服務的統一資源識別元 (URI)。您可以執行下列命令，來擷取位置資訊服務的 URI：Get-CsService –WebServer | Select-Object LIServiceInternalUri</p>
<p>如果為此參數指定值，則 UserSipAddress 參數亦為必要參數。如果您正在執行命令的電腦不具伺服器憑證，您也必須為 WebCredential 參數指定值。</p>
<p>除非您指定 TargetFqdn 參數，否則此參數為必要參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>包含用於存取位置資訊服務的使用者認證物件。此物件可透過呼叫 <strong>Get-Credential</strong> Cmdlet 並提供適當的認證來擷取。</p>
<p>如果指定了 TargetFqdn 和 UserSipAddress 參數，而且如果您正在執行 Cmdlet 的電腦不具伺服器憑證，則此為必要參數。</p></td>
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
<td><p><em>BssId</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>無線存取點的基本服務集識別碼 (BSSID)。此值的格式必須為 nn-nn-nn-nn-nn-nn，例如 12-34-56-78-90-ab。</p></td>
</tr>
<tr class="even">
<td><p><em>ChassisId</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>網路交換器的媒體存取控制 (MAC) 位址。此值的格式必須為 nn-nn-nn-nn-nn-nn，例如 12-34-56-78-90-ab，或 IP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>此參數不支援位置資訊伺服器。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Mac</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>連接埠交換器的 MAC 位址。此值的格式必須為 nn-nn-nn-nn-nn-nn，例如 12-34-56-78-90-ab。</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注意：指定變數名稱時，請勿在前面加上 $ 字元。若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似下列的命令：</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，您可使用下列語法，將輸出儲存於名為 $TestOutput 的變數中：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="even">
<td><p><em>PortId</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>與要測試之位置相關聯的連接埠識別碼。也可包含 MAC 位址或 IP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>PortIdSubType</em></p></td>
<td><p>選用</p></td>
<td><p>PortIDSubType</p></td>
<td><p>連接埠的子類型。此值可以輸入數值或字串，但必須是有效的子類型。有效的子類型為：</p>
<p>1: InterfaceAlias</p>
<p>5: InterfaceName</p>
<p>7: LocallyAssigned</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>登錄器服務的連接埠號碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>Subnet</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>子網路的 IP 位址。此值必須輸入為 IPv4 位址 (以點區隔位數，例如 192.0.2.0)。</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>遠端使用者的 SIP 位址。</p>
<p>如果您為此參數指定值，則 TargetFqdn 或 TargetUri 參數也是必要參數。</p>
<p>當您在指定 TargetFqdn 參數時，唯有當您尚未設定綜合交易使用者時，此參數才會是必要參數。若要查看是否已設定綜合交易使用者，請執行 <strong>Get-CsHealthMonitoringConfiguration</strong> Cmdlet。</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>選用</p></td>
<td><p>PSCredential</p></td>
<td><p>包含用於存取 位置資訊服務 的使用者認證物件。此物件可透過呼叫 <strong>Get-Credential</strong> Cmdlet 並提供適當的認證來擷取。</p>
<p>如果指定了 TargetUri 和 UserSipAddress 參數，而且執行命令的電腦不具伺服器憑證，則此為必要參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Test-CsLisConfiguration** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Export-CsLisConfiguration](export-cslisconfiguration.md)

