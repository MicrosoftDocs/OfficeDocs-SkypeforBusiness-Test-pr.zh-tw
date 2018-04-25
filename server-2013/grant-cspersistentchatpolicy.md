---
title: Grant-CsPersistentChatPolicy
TOCTitle: Grant-CsPersistentChatPolicy
ms:assetid: 58889550-167a-4267-9f3d-0f244e898599
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204907(v=OCS.15)
ms:contentKeyID: 49290979
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsPersistentChatPolicy

 

_**上次修改主題的時間：** 2015-03-09_

指派個別使用者的常設聊天室原則給使用者。常設聊天室原則可指定使用者是否可以存取存取常設聊天室。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Grant-CsPersistentChatPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將個別使用者原則 RedmondUsersPersistentChatPolicy 指派給 Active Directory 顯示名稱為 "Ken Myer" 的使用者。

    Grant-CsPersistentChatPolicy -Identity "Ken Myer" -PolicyName "RedmondUsersPersistentChatPolicy"

## 範例 2

範例 2 會將個別使用者原則 RedmondUsersPersistentChatPolicy 指派給在 IT 部門工作的所有使用者。為達成此目的，命令會先呼叫 **Get-CsUser** Cmdlet 並使用 LdapFilter 屬性；篩選值 "Department=IT" 可將傳回的資料限制在 IT 部門工作的使用者。然後再將該使用者集合管線傳送到 **Grant-CsPersistentChatPolicy** Cmdlet，以將 RedmondUsersPersistentChatPolicy 原則指派給集合中每一位使用者。

    Get-CsUser -LdapFilter "Department=IT" | Grant-CsPersistentChatPolicy -PolicyName "RedmondUsersPersistentChatPolicy"

## 範例 3

範例 3 會將個別使用者常設聊天室原則 RedmondUsersPersistentChatPolicy 指派給目前尚未獲指派個別使用者常設聊天室原則的所有使用者。為了執行此工作，命令會先使用 **Get-CsUser** Cmdlet 和 Filter 參數；篩選值 {PersistentChatPolicy –eq $Null} 可將傳回的資料限制在 PersistentChatPolicy 屬性目前為 Null ($Null) 的使用者帳戶。然後再將該使用者集合管線傳送到 **Grant-CsPersistentChatPolicy** Cmdlet，以將 RedmondUsersPersistentChatPolicy 原則指派給集合中每一位使用者。

    Get-CsUser -Filter {PersistentChatPolicy -eq $Null} | Grant-CsPersistentChatPolicy -PolicyName "RedmondUsersPersistentChatPolicy"

## 範例 4

範例 4 所示的命令會針對目前已獲指派個別使用者常設聊天室原則 RedmondUsersPersistentChatPolicy 的任何使用者，取消指派該原則。為了執行此工作，命令會先使用 **Get-CsUser** Cmdlet 和 Filter 參數，傳回目前已獲指派 RedmondUsersPersistentChatPolicy 原則的使用者集合 ({PersistentChatPolicy –eq "RedmondUsersPersistentChatPolicy"} 篩選值可將傳回的項目限制在 PersistentChatPolicy 屬性等於 RedmondUsersPersistentChatPolicy 的使用者帳戶)。然後，此集合會管線傳送到 **Grant-CsPersistentChatPolicy** Cmdlet，以將 PersistentChatPolicy 屬性設為 Null 值 ($Null) 而取消指派個別使用者原則。

取消指派個別使用者原則之後，使用者的常設聊天室功能會由其常設聊天室網站原則 (存在的話) 管理，或 (不存在的話) 由全域常設聊天室原則管理。

    Get-CsUser -Filter {PersistentChatPolicy -eq "RedmondUsersPersistentChatPolicy"} | Grant-CsPersistentChatPolicy -PolicyName $Null

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

預設並不會授與使用者常設聊天室服務的權限。只有受允許使用者存取該服務之常設聊天室原則規範的使用者，才會有該項存取權。當您安裝 Lync 2013時，所有使用者皆由全域常設聊天室原則所管理，無法使用常設聊天室。若要允許所有使用者存取該項服務，只要將此全域原則中的 EnablePersistentChat 屬性設為 True 即可。除此之外也可另外在網站範圍或個別使用者範圍建立其他原則，只授予部分使用者常設聊天室的存取權。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsPersistentChatPolicy"}

**Lync Server 控制台：**若要將常設聊天室原則指派至 Lync Server 控制台 中的使用者，請連按兩下正確的使用者帳戶。在 **\[編輯 Lync Server 使用者\]** 對話方塊中，選取 **\[常設聊天室原則\]** 下拉式清單中的原則，然後按一下 **\[認可\]**。

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>表示要指派個別使用者常設聊天室原則之使用者帳戶的 Identity。使用者 Identity 通常可以使用下列四種格式的其中一種來指定：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (例如 Ken Myer)。也可以利用使用者的 Active Directory 辨別名稱來指定使用者 Identity。</p>
<p>此外，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要指派之原則的「名稱」。PolicyName 只是 Identity 原則減去原則範圍 (&quot;tag:&quot;首碼)。例如，對於 Identity 為 tag:Redmond 的原則，其 PolicyName 等於 Redmond；對於 Identity 為 tag:RedmondUsersPersistentChatPolicy 的原則，其 PolicyName 等於 RedmondUsersPersistentChatPolicy。若要取消指派先前已指派給使用者的個別使用者原則，請將 PolicyName 設為 Null 值 ($Null)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您在指派新原則時，指定所要連絡之網域控制站的完整網域名稱。若未指定此參數， <strong>Grant-CsPersistentChatPolicy</strong> Cmdlet 會連絡第一個可使用的網域控制站。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過代表已指派原則的使用者之管線傳遞使用者物件。根據預設， <strong>Grant-CsPersistentChatPolicy</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串值或 Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy 物件。 **Grant-CsPersistentChatPolicy** Cmdlet 會接受代表使用者帳戶 Identity 之字串值的管線傳送輸入。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

根據預設， **Grant-CsPersistentChatPolicy** Cmdlet 不會傳回物件或值。但是，如果加入 PassThru 參數，Cmdlet 就會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact 的執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatPolicy](get-cspersistentchatpolicy.md)  
[New-CsPersistentChatPolicy](new-cspersistentchatpolicy.md)  
[Remove-CsPersistentChatPolicy](remove-cspersistentchatpolicy.md)  
[Set-CsPersistentChatPolicy](set-cspersistentchatpolicy.md)

