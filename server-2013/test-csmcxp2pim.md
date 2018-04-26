---
title: Test-CsMcxP2PIM
TOCTitle: Test-CsMcxP2PIM
ms:assetid: 443a3b31-6f58-4570-9eaa-310e73c39e03
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690020(v=OCS.15)
ms:contentKeyID: 49290755
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsMcxP2PIM

 

_**上次修改主題的時間：** 2015-03-09_

測試使用者配對使用 Lync Server Mobility Service 交換立即訊息的能力。Mobility Service 可讓行動電話使用者 (例如 iPhone 和 Windows Phone) 交換立即訊息與目前狀態資訊；從內部儲存及擷取語音信箱，而不使用無線提供者；以及利用 \[從公司撥號\] 和 \[電話撥出式會議\] 等 Lync Server 功能。 Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Test-CsMcxP2PIM -ReceiverSipAddress <String> -SenderSipAddress <String> <COMMON PARAMETERS>

    Test-CsMcxP2PIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID> -TargetFqdn <String> [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-RegistrarPort <Int32>]

## 範例

## 範例 1

範例 1 所示的命令會測試一組使用者 (Ken Myer 與 Pilar Ackerman) 是否能使用 Mobility Service 來交換立即訊息。為達此目的，範例中的前兩個命令會使用 **Get-Credential** Cmdlet 建立這兩位使用者的認證物件；Ken Myer 的認證會儲存在名稱為 $credential1 的變數中，而 Pilar Ackerman 的認證會儲存在名稱為 $credential2 的變數中。

認證物件建立好後，最後一個命令會呼叫 **Test-CsMcxP2PIM** Cmdlet，並確定指定目標登錄器集區 (atl-cs-001.litwareinc,com)、驗證類型 (Negotiate) 及兩位使用者的 SIP 位址與認證。

    $credential1 = Get-Credential "litwareinc\kenmyer"
    $credential2 = Get-Credential "litwareinc\pilar"
    
    Test-CsMcxP2PIM -TargetFqdn "atl-cs-001.litwareinc.com" -Authentication Negotiate -SenderSipAddres "sip:kenmyer@litwareinc.com" -SenderCredential $credential1 -ReceiverSipAddress "sip:packerman@litwareinc.com" -ReceiverCredential $credential2

## 詳細描述

Lync Server Mobility Service 將 Lync Server 的許多功能擴充至 Apple iPhone、Windows Phone、Android 電話及 Nokia 電話等行動裝置。使用者可以使用這些電話交換立即訊息和目前狀態資訊、接收新語音信箱的通知，以及執行其他功能。多虧有推入通知服務 (Apple Push Notification Service 和 Microsoft 推播通知服務 )，iPhone 或 Windows Phone 使用者可以接收這些通知，即使 Lync Server 在背景執行亦然。Mobility Service 也讓組織有機會啟用 \[從公司撥號\]。利用 \[從公司撥號\]，使用者可以從其行動電話撥打電話，並將此通話顯示為從公司電話撥出的通話；例如，來電顯示系統會顯示使用者的公司電話號碼，而不是使用者的行動電話號碼。

**Test-CsMcxP2PIM** Cmdlet 用來判斷一組使用者是否可以使用 Mobility Service 來交換立即訊息。請注意，執行此 Cmdlet 並不需要使用行動電話或實際傳送出任何立即訊息。反而，Cmdlet 會確保這兩個使用者能登入 Lync Server 且 Mobility Service 可建立這兩位使用者間交換立即訊息所需的連線。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsMcxP2PIM** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsMcxP2PIM"}

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
<td><p><em>Authentication</em></p></td>
<td><p>必要</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>允許的值包括：TrustedServer、Negotiate、ClientCertificate 及 LiveID。</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的使用者認證物件。傳給 ReceiverCredential 的值應該是以 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\pilar 的認證物件，並將該物件儲存於名為 $y 的變數中：</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的 SIP 位址。例如：</p>
<p>-ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;</p>
<p>ReceiverSipAddress 參數與 ReceiverCredential 參數必須參照相同的使用者帳戶。</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的使用者認證物件。傳給 SenderCredential 的值應該是以 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，此程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的 SIP 位址。例如：</p>
<p>-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>SenderSIPAddress 參數必須與 SenderCredential 參數參考相同的使用者帳戶。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>要測試之集區的完整網域名稱 (FQDN)。</p></td>
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
<td><p>System.Strkng</p></td>
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
</tbody>
</table>


## 輸入類型

無。 **Test-CsMcxP2PIM** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsMcxP2PIM** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

