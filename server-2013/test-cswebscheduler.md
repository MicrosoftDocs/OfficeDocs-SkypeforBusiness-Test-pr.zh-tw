---
title: Test-CsWebScheduler
TOCTitle: Test-CsWebScheduler
ms:assetid: 3dbd7ef6-a60f-4350-8831-73818e10863b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204829(v=OCS.15)
ms:contentKeyID: 49290680
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsWebScheduler

 

_**上次修改主題的時間：** 2015-03-09_

驗證使用者是否可以使用 Lync Server 2013 Web Scheduler 以排程線上會議。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsWebScheduler -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsWebScheduler -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsWebScheduler -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 範例

## 範例 1

上述範例會驗證 atl-cs-001.litwareinc.com 集區的 Web 排程器。只有已針對 atl-cs-001.litwareinc.com 集區定義測試使用者時，此命令才有作用。如果已定義，則命令會判斷第一位測試使用者是否能夠使用 Web 排程器來排定線上會議。

如果尚未定義測試使用者，命令會因為不知道登入的使用者而失敗。如果您尚未定義集區的測試使用者，必須加入 UserSipAddress 參數，以及登入時命令應使用的使用者認證。

    Test-CsWebScheduler -TargetFqdn "atl-cs-001.litwareinc.com"

## 範例 2

範例 2 所示的命令會測試特定使用者 (itwareinc\\pilar) 使用 Web 排程器以排定線上會議的能力。為達成此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet 建立一個包含使用者 Pilar Ackerman 之名稱與密碼的 Windows PowerShell 命令列介面認證物件 (因為已加上登入名稱 litwareinc\\pilar 做為參數，所以 \[ Windows PowerShell 認證要求\] 對話方塊只需要系統管理員輸入 Pilar Ackerman 帳戶的密碼)。然後，產生的認證物件會儲存在名為 $cred1 的變數中。

接著，第二個命令會檢查此使用者是否可以登入 atl-cs-001.litwareinc.com 集區，以及排定線上會議。為了執行此工作，會呼叫 **Test-CsWebScheduler** Cmdlet 搭配下列三個參數：TargetFqdn (登錄器集區的 FQDN)；UserCredential (包含 Pilar Ackerman 使用者認證的 Windows PowerShell 物件)；及 UserSipAddress (對應至所提供使用者認證的 SIP 位址)。

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsWebScheduler -TargetFqdn "atl-cs-001.litwareinc.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

## 詳細描述

Web 排程器可讓非 Microsoft Outlook 使用者排程線上會議。這項新功能 (集結了 Microsoft Lync Server 2010 Resource Kit 隨附之 Web 排程器工項的功能) 可讓使用者：

  - 排程新的線上會議。

  - 列出自己所排程的所有會議。

  - 檢視/修改現有的會議。

  - 刪除現有的會議。

  - 使用預先設定的 SMTP 郵件伺服器，傳送電子郵件邀請給會議參與者。

  - 加入現有的會議。

**Test-CsWebScheduler** Cmdlet 可讓您確認特定的使用者是否可以使用 Web 排程器排程會議。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsWebScheduler"}

**Lync Server 控制台：** **Test-CsWebScheduler** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>TargetUri</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>Web 排程器的統一資源識別元 (URI)。請注意，您無法在同一個命令中同時使用 TargetUri 參數和 TargetFqdn 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試之帳戶的使用者認證物件。傳遞到 UserCredential 的值必須是使用 Get-Credential Cmdlet 取得的物件參考。例如，這個程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件以名稱為</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。如果您是在集區的狀況監控組態設定下進行測試，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>選用</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>允許的值為：</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>可讓您驗證外部使用者是否可使用 Web 排程器。</p></td>
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
<td><p>要測試之使用者帳戶的 SIP 位址；例如：</p>
<p>-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>UserSipAddress 參數必須參考與 UserCredential 相同的使用者帳戶。如果您是在集區的狀況監控組態設定下進行測試，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>選用</p></td>
<td><p>PSCredential</p></td>
<td><p>要在測試中使用之使用者帳戶的使用者認證物件。傳送至 UserCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 所取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot; 的變數中</p>
<p>如果指定了 TargetUri 參數或 UserSipAddress 參數，而且執行命令的電腦不具伺服器憑證，則需要此參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Test-CsWebScheduler** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsWebScheduler** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.WebTaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsWebServer](set-cswebserver.md)

