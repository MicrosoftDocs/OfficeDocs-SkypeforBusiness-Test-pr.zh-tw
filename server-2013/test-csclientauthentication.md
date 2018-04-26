---
title: Test-CsClientAuthentication
TOCTitle: Test-CsClientAuthentication
ms:assetid: 6a25b2c6-0cb2-473c-af92-0be5cead8a19
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619181(v=OCS.15)
ms:contentKeyID: 49291207
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsClientAuthentication

 

_**上次修改主題的時間：** 2015-03-09_

判斷使用者是否可以使用從憑證佈建服務下載的憑證登入 Lync Server。Lync Server 2013 中已導入此 Cmdlet。它取代了 Lync Server 2010 中使用的 **Test-CSClientAuth** Cmdlet。

## 語法

    Test-CsClientAuthentication -UserCredential <PSCredential> -UserSipAddress <String> [-Force <SwitchParameter>] [-LiveIdAuthentication <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] [-TargetUri <String>]

## 範例

## 範例 1

範例 1 所示的命令會測試使用者 litwareinc\\kenmyer 使用用戶端憑證登入登錄器集區 atl-cs-001.litwareinc.com 的功能。為了執行此工作，範例中的第一個命令會使用 **Get-Credential** Cmdlet，以建立認證物件供上述使用者使用。產生的認證物件 (需要您輸入使用者的密碼) 會儲存在名為 $cred1 的變數中。

接著，第二個命令會呼叫 **Test-CsClientAuthentication** Cmdlet，並指定登錄器集區的 FQDN (TargetFqdn)、使用者的 SIP 位址 (UserSipAddress) 以及在初始命令中建立的認證物件 (UserCredential)。

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsClientAuthentication -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred1

## 詳細描述

用戶端憑證提供使用者另一種獲得 Lync Server 驗證的方法。若要判斷使用者是否可以使用用戶端憑證登入系統，您可以執行 **Test-CsClientAuthentication** Cmdlet。當您執行 **Test-CsClientAuthentication** Cmdlet 時，必須指定要測試之登錄器集區和使用者帳戶的 SIP 位址；您也必須能夠提供使用者的登入名稱和密碼。呼叫 **Test-CsClientAuthentication** Cmdlet 後，該 Cmdlet 會連絡憑證佈建服務，並下載指定使用者任何用戶端憑證的複本。如果可以找到用戶端憑證並下載，則 **Test-CsClientAuthentication** Cmdlet 將會嘗試使用該憑證登入。如果登入成功，**Test-CsClientAuthentication** Cmdlet 將會登出並報告該測試成功。

如果找不到憑證或無法下載，或者 Cmdlet 無法使用該憑證登入，則 **Test-CsClientAuthentication** Cmdlet 將會報告測試失敗。

誰可以執行這個指令程式：若要傳回所有獲指派此 Cmdlet 的角色存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsClientAuthentication"}

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
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>要在測試中使用之使用者帳戶的使用者認證物件。傳送至 UserCredential 的值應該是使用 <strong>Get-Credential</strong> 指令程式所取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>測試中要使用之使用者的 SIP 位址。例如：-UserSipAddress sip:kenmyer@litwareinc.com。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>LiveIdAuthentication</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>驗證測試使用者使用其 OrgId (企業 Live ID) 認證登入的功能。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數存在時，會以指定的變數儲存執行 Cmdlet 的詳細輸出。此變數包含兩個方法 (ToHTML 和 ToXML)，可接著用來將該輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要以名稱為 $TestOutput 的記錄器變數儲存輸出，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注意：指定變數名稱時，請不要在前面加上 $ 字元。若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似如下的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似如下的命令：</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數存在時，會以指定的變數儲存執行 Cmdlet 的詳細輸出。例如，若要以名稱為 $TestOutput 的變數儲存輸出，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。如果登錄器使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要測試用戶端驗證之登錄器集區的完整網域名稱 (FQDN)。例如：-TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>憑證佈建服務的 URL。如果未加入此參數，則 <strong>Test-CsClientAuthentication</strong> Cmdlet 將會使用針對登錄器集區設定的憑證佈建服務。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Test-CsClientAuthentication** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsWebServiceConfiguration](get-cswebserviceconfiguration.md)  
[Test-CsRegistration](test-csregistration.md)

