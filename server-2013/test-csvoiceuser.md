---
title: Test-CsVoiceUser
TOCTitle: Test-CsVoiceUser
ms:assetid: f29c3b43-d315-4964-ab5c-9fb14612db34
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413013(v=OCS.15)
ms:contentKeyID: 49292790
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoiceUser

 

_**上次修改主題的時間：** 2015-03-09_

指出應根據語音規則、路由及原則來傳送指定使用者之通話的路由。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsVoiceUser -DialedNumber <PhoneNumber> -SipUri <UserIdParameter> [-Force <SwitchParameter>]

## 範例

## 範例 1

此範例會根據 SIP 位址為 sip:kmyer@litwareinc.com 的使用者來執行語音使用者測試。此測試會根據由 DialedNumber 參數 ("+14255559999") 所提供的電話號碼來執行。如果沒有識別出相符的規則或路由，此 Cmdlet 會傳回 null 值。請注意，我們也會包含 Verbose 參數。Verbose 是常見的 Windows PowerShell 參數，會在執行測試時顯示其他資訊，例如，會針對此測試載入哪一個撥號對應表和語音原則。

    Test-CsVoiceUser -DialedNumber "+14255559999" -SipUri "sip:kmyer@litwareinc.com" -Verbose

## 範例 2

此範例會針對所有已啟用 Lync Server 或 Office Communications Server 的使用者執行語音路由測試。命令一開始會呼叫 **Get-CsUser** Cmdlet，它會傳回已針對 Lync Server 或 Office Communications Server 啟用的所有使用者集合。此範例接著會將使用者集合傳送給 **ForEach-Object** Cmdlet。此 Cmdlet 會查看每個個別使用者物件，並執行指定於大括號 ({}) 內的動作。

第一個動作是輸出目前使用者的顯示名稱 (目前使用者是利用 $\_ 字元來表示；因此，顯示名稱會位於 $\_ 的 DisplayName 屬性中)。我們現在會看見正在測試哪個使用者帳戶。接著，呼叫 **Test-CsVoiceUser** Cmdlet，將目前使用者的 DialedNumber ("+14255559999") 及 SipUri 傳送給它。在此範例中，我們所使用的是使用者的 SIP 位址 ($\_.SipAddress)。

最後，因為輸出預設為表格格式且可能截斷以符合螢幕寬度，所以我們會將測試結果傳送到 **Format-List** Cmdlet，如此，將可看見每位使用者的顯示名稱，後面加上一行來顯示每個輸出欄位。

    Get-CsUser | ForEach-Object {$_.DisplayName; Test-CsVoiceUser -DialedNumber "+14255559999" -SipUri $_.SipAddress} | Format-List

## 詳細描述

當使用者撥打電話時，該通電話所採用以到達其目的地的路由會視指派給該使用者的原則和撥號對應表而定。若已指定使用者的 SIP 位址與電話號碼，此 Cmdlet 會傳回已轉譯成 E.164 格式的電話號碼 (以使用者的撥號對應表為依據)、支援該轉譯的正規化規則、號碼模式符合該電話號碼的第一個路由 (以路由 Priority 為依據)，以及將該使用者的語音原則連結至語音路由的電話使用方式。

此 Cmdlet 可用來判斷特定的電話號碼是否將根據使用者設定以預期方式進行路由與轉譯，而且可協助進行個別使用者所遇到之問題的疑難排解。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsVoiceUser** Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoiceUser"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
<td><p>要測試的電話號碼。</p>
<p>完整資料類型：Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
</tr>
<tr class="even">
<td><p><em>SipUri</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>據以執行此測試之使用者的 SIP URI。這是如同 CsUser Cmdlet 中所使用之使用者的 Identity。您可以使用下列四種格式的其中一種來指定使用者的 Identity：1) 使用者的 SIP 位址；2) 使用者的使用者主要名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (例如 Ken Myer)。請注意，無法使用 SamAccountName 做為識別身分。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏當您執行 Cmdlet 時可能發生的任何確認提示字元或非嚴重錯誤訊息。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

傳回 type Microsoft.Rtc.Management.Voice.OcsVoiceUserTestResult 類型的物件。

## 請參閱

#### 其他資源

[Get-CsUser](get-csuser.md)

