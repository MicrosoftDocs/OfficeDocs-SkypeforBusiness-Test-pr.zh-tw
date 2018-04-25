---
title: Test-CsMcxConference
TOCTitle: Test-CsMcxConference
ms:assetid: c6ca9019-1535-489d-a42e-1a50070b2f67
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690045(v=OCS.15)
ms:contentKeyID: 49292267
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsMcxConference

 

_**上次修改主題的時間：** 2015-03-09_

測試三位使用者參與 Lync Server 2013 Mobility Service 會議的能力。Mobility Service 可讓行動電話使用者 (例如 iPhone 和 Windows Phone) 交換立即訊息與目前狀態資訊；從內部儲存及擷取語音信箱，而不使用無線提供者；以及利用 \[從公司撥號\] 和 \[電話撥出式會議\] 等 Lync Server 功能。 Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Test-CsMcxConference -OrganizerCredential <PSCredential> -OrganizerSipAddress <String> -User2Credential <PSCredential> -User2SipAddress <String> -UserCredential <PSCredential> -UserSipAddress <String> <COMMON PARAMETERS>

    Test-CsMcxConference -OrganizerSipAddress <String> -User2SipAddress <String> -UserSipAddress <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID> -TargetFqdn <String> [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-RegistrarPort <Int32>]

## 範例

## 範例 1

範例 1 所示的命令會確認是否可以使用下列三個使用者帳戶進行 Mobility Service 會議：Ken Myer (會議召集人)、Pilar Ackerman 及 Aidan Delaney。為了執行這項測試，您必須先建立每個使用者帳戶的認證。前三行程式碼會建立這些物件，並以變數 $organizerCred (Ken Myer)、$user1Cred (Pilar Ackerman) 及 $user2Cred (Aidan Delaney) 儲存。

建立認證物件之後，您可以接著呼叫 **Test-CsMcxConference** Cmdlet，確定指定目標登錄器集區 (atl-cs-001.litwareinc,com)、驗證類型 (Negotiate)，以及做為會議參與者之三個使用者帳戶的 SIP 位址和認證。

    $organizerCred = Get-Credential "litwareinc\kenmyer"
    $user1Cred = Get-Credential "litwareinc\packerman"
    $user2Cred = Get-Credential "litwareinc\adelaney"
    
    Test-CsMcxConference -TargetFqdn "atl-cs-001.litwareinc.com" -Authentication Negotiate -OrganizerSipAddress "sip:kenmyer@litwareinc.com" -OrganizerCredential $organizerCred -UserSipAddress "sip:pilar@litwareinc.com" -UserCredential $user1Cred -User2SipAddress "sip:adelaney@litwareinc.com" -User2Credential $user2Cred

## 詳細描述

Mobility Service 將 Lync Server 的許多功能擴充至 Apple iPhone、Windows Phone、Android 電話及 Nokia 電話等行動裝置。使用者可以使用這些電話交換立即訊息和目前狀態資訊、接收新語音信箱的通知，以及執行其他功能。多虧有推入通知服務 (Apple Push Notification Service 和 Microsoft Push Notification Service)，iPhone 或 Windows Phone 使用者可以接收這些通知，即使 Lync 在背景執行亦然。Mobility Service 也讓組織有機會啟用 \[從公司撥號\]。利用 \[從公司撥號\]，使用者可以從其行動電話撥打電話，並將此通話顯示為從公司電話撥出的通話；例如，來電顯示系統會看見使用者的公司電話號碼，而不是使用者的行動電話號碼。

**Test-CsMcxConference** Cmdlet 可用來決定三人一組的使用者是否可以使用 Mobility Service 參與會議。請注意，執行此 Cmdlet 不需要使用行動電話或實際建立真正的會議。相反地，此 Cmdlet 會確認這三位使用者能夠登入 Lync Server，以及 Mobility Service 能夠建立進行會議所需的連線。此 Cmdlet 也會確認會議召集人能夠傳送立即訊息給其他兩位會議參與者。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsMcxConference** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsMcxConference"}

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
<td><p><em>OrganizerCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>做為會議召集人之使用者帳戶的使用者認證物件。傳遞到 OrganizerCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，這個程式碼會傳回使用者 litwareinc\adelaney 的認證物件，並將該物件儲存於名為 $z 的變數中：</p>
<p>$z = Get-Credential &quot;litwareinc\adelaney&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>OrganizerSipAddress</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>做為會議召集人之使用者帳戶的 SIP 位址。例如：</p>
<p>-OrganizerSipAddress &quot;sip:adelaney@litwareinc.com&quot;</p>
<p>OrganizerSipAddress 參數必須與 OrganizerCredential 參數參考相同的使用者帳戶。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>要測試之集區的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="odd">
<td><p><em>User2Credential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的使用者認證物件。傳遞到 Use2rCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，這個程式碼會傳回使用者 litwareinc\kenmyer 的認證物件，並將該物件以名稱為 $y 的變數儲存：</p>
<p>$y = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p></td>
</tr>
<tr class="even">
<td><p><em>User2SipAddress</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>要測試的兩個使用者帳戶中，第二個使用者帳戶的 SIP 位址。例如：</p>
<p>-User2SipAddress &quot;sip:pilar@litwareinc.com&quot;</p>
<p>User2SipAddress 參數必須與 User2Credential 參數參考相同的使用者帳戶。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>必要</p></td>
<td><p>PSCredential</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的使用者認證物件。傳遞到 UserCredential 的值應該是使用 <strong>Get-Credential</strong> Cmdlet 取得的物件參考。例如，這個程式碼會傳回使用者 litwareinc\pilar 的認證物件，並將該物件儲存於名為 $x 的變數中：</p>
<p>$x = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>執行此命令時，您需要提供使用者密碼。</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>必要</p></td>
<td><p>String</p></td>
<td><p>要測試的兩個使用者帳戶中，第一個使用者帳戶的 SIP 位址。例如：</p>
<p>-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>UserSipAddress 參數必須與 UserCredential 參數參考相同的使用者帳戶。</p></td>
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
</tbody>
</table>


## 輸入類型

無。 **Test-CsMcxConference** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsMcxConference** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

