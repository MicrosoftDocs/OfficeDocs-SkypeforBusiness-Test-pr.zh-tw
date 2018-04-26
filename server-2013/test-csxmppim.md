---
title: Test-CsXmppIM
TOCTitle: Test-CsXmppIM
ms:assetid: ffeb05a7-141d-46dc-936f-1f7218521ff8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205423(v=OCS.15)
ms:contentKeyID: 49292937
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsXmppIM

 

_**上次修改主題的時間：** 2015-03-09_

驗證是否可以透過 XMPP 閘道傳送立即訊息。XMPP 閘道可讓 Lync Server 2013 使用者和使用 Extensible Messaging and Presence Protocol (XMPP) 之 IM 及目前狀態提供者的使用者交換立即訊息和目前狀態資訊。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsXmppIM -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsXmppIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsXmppIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Receiver <String> [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

上述範例會針對集區 atl-cs-001.litwareinc.com 驗證 XMPP 立即訊息功能。只有已針對集區 atl-cs-001.litwareinc.com 定義測試使用者時，此命令才有作用。如果已定義，則命令會判斷第一個測試使用者是否可以將 XMPP 立即訊息傳送給 SIP 位址為 adelaney@contoso.com 的使用者。

如果尚未定義測試使用者，命令會因為不知道登入的使用者而失敗。如果您尚未定義集區的測試使用者，必須加入 UserSipAddress 參數，以及登入時命令應使用的使用者認證。

    Test-CsXmppIM -TargetFqdn "atl-cs-001.litwareinc.com" -Receiver "adelany@contoso.com"

## 範例 2

範例 2 所示的命令會測試特定使用者 (itwareinc\\pilar) 能否登入並傳送 XMPP 立即訊息給使用者 adelaney@contoso.com 的能力。為達成此目的，範例中的第一個命令會使用 Get-Credential Cmdlet 建立包含使用者 Pilar Ackerman 之名稱與密碼的 Windows PowerShell 命令列介面認證物件 (因為已加上登入名稱 litwareinc\\pilar 做為參數，所以系統管理員只需要在 \[ Windows PowerShell 認證要求\] 對話方塊輸入 Pilar Ackerman 帳戶的密碼)。然後再將產生的認證物件儲存在名為 $cred1 的變數中。

接著，第二個命令會檢查此使用者是否可以登入集區 atl-cs-001.litwareinc.com 並傳送 XMPP 立即訊息。為達成此目的，會呼叫 **Test-CsXmppIm** Cmdlet 搭配下列四個參數：TargetFqdn (登錄器集區的 FQDN)、Receiver (接收訊息的使用者之 SIP 位址)、UserCredential (包含 Pilar Ackerman 使用者認證的 Windows PowerShell 物件) 以及 UserSipAddress (對應至所提供使用者認證的 SIP 位址)。

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsXmppIM -TargetFqdn "atl-cs-001.litwareinc.com" -Receiver "adelany@contoso.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

## 詳細描述

Extensible Messaging and Presence Protocol (XMPP) 是標準的通訊協定 (XML 格式)，可用於在網際網路上傳送訊息。 XMPP 原名 Jabber，是許多網際網路訊息與通訊應用程式 (包括 Google Talk 與 Facebook Chat) 所支援的通訊協定。 **Test-CsXmppIM** Cmdlet 可驗證使用者是否可與 XMPP 網路上的使用者交換立即訊息。請注意，您必須取得 XMPP 使用者的有效 SIP 位址，且該 SIP 位址所在的網路必須已設為允許 XMPP 的協力廠商。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsXmppIM"}

**Lync Server 控制台：** **Test-CsXmppIM** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>Receiver</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>接收測試訊息的使用者 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>所測試之集區的完整網域名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試之使用者帳戶的使用者認證物件。傳送至 UserCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參照。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p>
<p>如果您使用狀況監控組態設定來進行測試，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>選用</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>要測試之帳戶的使用者認證物件。傳遞到 UserCredential 的值必須是使用 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，這個程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件以名稱為</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot; 的變數中</p>
<p>執行此命令時，您需要提供使用者密碼。如果您是在集區的狀況監控組態設定下進行測試，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
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
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>Int32</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。如果登錄器使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>要測試之使用者帳戶的 SIP 位址；例如：</p>
<p>-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>UserSipAddress 參數必須參考與 UserCredential 相同的使用者帳戶。如果您是在集區的狀況監控組態設定下進行測試，則不需要此參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Test-CsXmppIM** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsXmppIM** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsXmppGatewayConfiguration](set-csxmppgatewayconfiguration.md)

