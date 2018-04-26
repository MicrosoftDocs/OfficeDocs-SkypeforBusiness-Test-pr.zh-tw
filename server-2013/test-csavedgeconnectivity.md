---
title: Test-CsAVEdgeConnectivity
TOCTitle: Test-CsAVEdgeConnectivity
ms:assetid: 9f3b2c70-9239-4085-a108-43e0b7a308b5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205138(v=OCS.15)
ms:contentKeyID: 49291844
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAVEdgeConnectivity

 

_**上次修改主題的時間：** 2015-03-09_

驗證是否能夠連線到 A/V Edge Server。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsAVEdgeConnectivity -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsAVEdgeConnectivity -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAVEdgeConnectivity [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

範例 1 所示的命令會驗證預先設定的測試使用者是否能連線到 pool atl-cs-001.litwareinc.com 所設定的 A/V Edge Server。請注意，您至少須為 atl-cs-001.litwareinc.com 定義一個健康狀況監視測試使用者，此命令才會成功。

    Test-CsAVEdgeConnectivity -TargetFqdn "atl-cs-001.litwareinc.com"

## 範例 2

在範例 2 中， **Test-CsAVEdgeConnectivity** Cmdlet 會驗證 SIP 位址為 sip:kenmyer@litwareinc.com 的使用者是否能夠連線到 AV Edge Server。為達成此目的，範例中的第一個命令會使用 Get-Credential Cmdlet 擷取使用者 litwareinc\\kenmyer 的 Windows PowerShell 認證物件。請注意，在取得此物件時，您必須提供此帳戶的密碼。取得認證物件之後，第二個命令會使用 **Test-CsAVEdgeConnectivity** Cmdlet 驗證使用者是否能連線到 AV Edge Server。

    $cred = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAVEdgeConnectivity -TargetFqdn "atl-cs-001.litwareinc.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred

## 詳細描述

**Test-CsAVEdgeConnectivity** Cmdlet 可驗證使用者是否能夠連線到指派給登錄器集區的 AV Edge Server。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAVEdgeConnectivity"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Test-CsAVEdgeConnectivity** Cmdlet 所執行的功能。

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
<td><p>System.Strkng</p></td>
<td><p>要測試之集區的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>要測試之帳戶的使用者認證物件。傳遞給 UserCredential 的值必須是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參照。例如下列程式碼會傳回使用 litwareinc\kenmyer 的認證物件，並將該物件儲存在名為</p>
<p>$x:$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。如果您是在集區的狀況監控組態設定下進行測試，則不需要此參數。</p></td>
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
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
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
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
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
<td><p><em>UserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要測試之使用者帳戶的 SIP 位址。例如 -UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。UserSipAddress 參數必須參照 UserCredential 所參照的使用者帳戶。若是使用集區的健康狀況監視組態設定執行此測試，即無須指定此參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsAVEdgeConnectivity** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsAVEdgeConnectivity** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)

