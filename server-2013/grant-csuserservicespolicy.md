---
title: Grant-CsUserServicesPolicy
TOCTitle: Grant-CsUserServicesPolicy
ms:assetid: f68b5c61-9820-4b49-954a-2dd61156bc02
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205388(v=OCS.15)
ms:contentKeyID: 49292831
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsUserServicesPolicy

 

_**上次修改主題的時間：** 2015-03-09_

指派個別使用者的 User Services 原則給一或多位使用者。User Services 原則可決定要將使用者的連絡資訊儲存在 Lync Server 2013 或統一連絡人存放區中。使用者可利用統一連絡人存放區維護一組連絡人，供 Lync 2013、Microsoft Outlook 及/或 Microsoft Outlook Web Access 存取。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Grant-CsUserServicesPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將個別使用者 User Services 原則 RedmondUserServicesPolicy 指派給 Identity (在本例中為 Active Directory 顯示名稱) 為 Ken Myer 的使用者。

    Grant-CsUserServicesPolicy -Identity "Ken Myer" -PolicyName "RedmondUserServicesPolicy"

## 範例 2

範例 2 會取消指派先前指派給 Ken Myer 之任何個別使用者 User Services 原則。將 PolicyName 參數設為 Null 值 ($Null) 即可取消個別使用者原則的指派。

    Grant-CsUserServicesPolicy -Identity "Ken Myer" -PolicyName $Null

## 範例 3

範例 3 會將個別使用者 User Services 原則 RedmondUserServicesPolicy 指派給登錄器集區 atl-cs-001.litwareinc.com 的使用者。為達成此目的，會先呼叫 **Get-CsUser** Cmdlet 搭配 Filter 參數；篩選值 {RegistrarPool –eq "atl-cs-001.litwareinc.com" 可將傳回的資料限制在屬於登錄器集區 atl-cs-001.litwareinc.com 的使用者。然後再將該使用者集合管線傳送到 **Grant-CsUserServicesPolicy** Cmdlet，以將原則 RedmondUserServicesPolicy 指派給集合中的每一位使用者。

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Grant-CsUserServicesPolicy -PolicyName "RedmondUserServicesPolicy"

## 詳細描述

Lync Server 2013 中所導入的統一連絡人存放區可讓系統管理員選擇將使用者的連絡人存放在 Microsoft Exchange Server 2013，而不存放在 Lync Server；相對地，使用者也因此而能從 Microsoft Outlook、Outlook Web Access 及 Lync 2013 存取相同的連絡人集合 (除此之外，您也可繼續將連絡人存放在 Lync Server 2013 中，讓使用者可以分別維護兩組連絡人：一組供 Outlook 與 Outlook Web Access 使用，一組供 Lync 2013 使用)。

若要充分發揮統一連絡人存放區的功能，必須 (首要事項) 為使用者指派可以讓使用者使用統一連絡人存放區的 User Services 原則。User Services 原則 (可在全域、網站或個別使用者範圍設定) 只包含 UcsAllowed 一項屬性。若此屬性設為 True (並假設其他先決條件皆已符合)，當使用者下次登入 Lync Server 2013時，便會自動將其連絡人移轉到統一連絡人存放區。

若此屬性設為 False，將不會執行自動移轉。然而，單純設定 UcsAllowed 並不會將使用者的連絡人從統一連絡人存放區移回 Lync Server。為達成此目的，您必須先為使用者指派不允許使用統一連絡人存放區的 User Services 原則。然後再使用 I**nvoke-UcsRollback** Cmdlet 手動將連絡人從統一連絡人存放區移轉回 Lync Server。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsUserServicesPolicy"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Grant-CsUserServicesPolicy** Cmdlet 所執行的功能。

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
<td><p>表示要指派個別使用者使用者經驗原則的使用者帳戶 Identity。通常可以使用下列四種格式的其中一種來指定使用者身分識別：1) 使用者的 SIP 位址；2) 使用者的使用者主要名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (例如 Ken Myer)。</p>
<p>也可以使用使用者的 Active Directory 辨別名稱來指定使用者身分識別。</p>
<p>此外，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派之原則的「名稱」。簡單來說，PolicyName 是原則 Identity 減去原則範圍 (&quot;tag:&quot;首碼)。例如，Identity 為 tag:Redmond 的原則擁有與 Redmond 相等的 PolicyName；同樣地，Identity 為 tag:RedmondUserExperiencePolicy 的原則則擁有與 RedmondUserExperiencePolicy 相等的 PolicyName。</p>
<p>若要取消指派先前已指派給使用者的個別使用者原則，請將 PolicyName 設定為 Null 值 ($Null)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站擷取使用者資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-dc-001) 或其完整網域名稱 (FQDN) (例如，atl-dc-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過代表已指派原則的使用者帳戶之管線傳遞使用者物件。根據預設，<strong>Grant-CsUserServicesPolicy</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Grant-CsUserServicesPolicy** Cmdlet 會接受代表使用者帳戶 Identity 之字串值的管線傳送資料。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

**Grant-CsUserServicesPolicy** Cmdlet 預設不會傳回值或物件。但是，如果加入 PassThru 參數，Cmdlet 就會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact 的執行個體。

## 請參閱

#### 其他資源

[Get-CsUserServicesPolicy](get-csuserservicespolicy.md)  
[New-CsUserServicesPolicy](new-csuserservicespolicy.md)  
[Remove-CsUserServicesPolicy](remove-csuserservicespolicy.md)  
[Set-CsUserServicesPolicy](set-csuserservicespolicy.md)

