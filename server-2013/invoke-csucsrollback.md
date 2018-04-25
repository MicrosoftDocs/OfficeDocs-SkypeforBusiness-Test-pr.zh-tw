---
title: Invoke-CsUcsRollback
TOCTitle: Invoke-CsUcsRollback
ms:assetid: 0aed0286-e552-4d47-93bc-3375cab48a03
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204661(v=OCS.15)
ms:contentKeyID: 49290041
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsUcsRollback

 

_**上次修改主題的時間：** 2015-03-09_

從統一連絡人存放區中移除使用者的連絡人，並將該連絡人資訊改為儲存在 Lync Server 2013 中。統一連絡人存放區可讓使用者維護一組連絡人，方便使用 Lync 2013、Microsoft Outlook 及/或 Microsoft Outlook Web Access 加以存取。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Invoke-CsUcsRollback -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將使用者 Ken Myer 從統一連絡人存放區中移除。

    Invoke-CsUcsRollback -Identity "Ken Myer"

## 範例 2

範例 2 會從統一連絡人存放區中，移除屬於 atl-cs-001.litwareinc.com 登錄器集區的所有使用者。為達成此目的，命令會先呼叫 **Get-CsUser** Cmdlet 搭配 Filter 參數；{RegistrarPool –eq "atl-cs-001.litwareinc.com"} 篩選值會將傳回的資料限制在屬於 atl-cs-001.litwareinc.com 集區的使用者。然後將那些使用者帳戶管線傳送到 **Invoke-CsUcsRollback** Cmdlet，以將每個使用者從統一連絡人存放區中移除。為了隱藏每次 Cmdlet 復原使用者帳戶時都會出現的確認提示，會使用下列語法加入 Confirm 參數：-Confirm:$False

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Invoke-CsUcsRollback -Confirm:$False

## 詳細描述

Lync Server 2013 中所導入的統一連絡人存放區可讓系統管理員選擇將使用者的連絡人存放在 Microsoft Exchange Server 2013，而不存放在 Lync Server；相對地，使用者也因此而能從 Microsoft Outlook、Outlook Web Access 及 Lync 2013 存取相同的連絡人集合。(除此之外，您也可繼續將連絡人存放在 Lync Server 中，讓使用者可以分別維護兩組連絡人：一組供 Outlook 與 Outlook Web Access 使用，一組供 Lync 2013 使用。)

若要充分發揮統一連絡人存放區的功能，必須 (首要事項) 為使用者指派可以讓使用者使用統一連絡人存放區的 User Services 原則。若其他所有先決條件均已符合，當使用者下次登入 Lync Server 2013時，便會自動將其連絡人從 Lync Server 移至統一連絡人存放區。如需詳細資訊，請參閱 Set-CsUserServicesPolicy Cmdlet 的＜說明＞主題。

此後若想要將這些連絡人再移回 Lync Server (並清空統一連絡人存放區)，必須執行兩項作業。首先是為使用者指派新的 User Services 原則，禁止其使用統一連絡人存放區。接著再使用 **Invoke-CsUcsRollback** Cmdlet 手動將連絡人從統一連絡人存放區移轉回 Lync Server。只變更 User Services 原則並不會從統一連絡人存放區移除使用者的連絡人。您必須呼叫 **Invoke-CsUcsRollback** Cmdlet 才可達成此目的。

注意：從技術面看，只呼叫 **Invoke-CsUcsRollback** Cmdlet 而不修改 User Services 原則，雖可從統一連絡人存放區中移除使用者的連絡人，但此變更僅為暫時性的改變。若不變更 User Services 原則，待 7 天的等待期一過，使用者的連絡人會自動移回統一連絡人存放區。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsUcsRollback"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Invoke-CsUcsRollback** Cmdlet 所執行的功能。

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
<td><p>指出所要復原之使用者帳戶的 Identity。使用者識別通常可以使用下列四種格式的其中一種來指定：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。</p>
<p>您也可以利用使用者的 Active Directory 辨別名稱來參考使用者帳戶。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為 &quot; Smith&quot; 字串值的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。若要防止每次復原使用者帳戶時，都會出現確認提示，請使用下列語法：</p>
<p>-Confirm:$False</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站擷取使用者資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-dc-001) 或其完整網域名稱 (FQDN) (例如，atl-dc-001.litwareinc.com)。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過管線傳遞代表已從統一連絡人存放區移除之使用者帳戶的使用者物件。根據預設，<strong>Invoke-CsUcsRollback</strong> Cmdlet 不會透過管線傳遞物件。</p></td>
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

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Invoke-CsUcsRollback** Cmdlet 接受管線傳送的字串值輸入，代表使用者帳戶的 Identity。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[New-CsUserServicesPolicy](new-csuserservicespolicy.md)  
[Set-CsUserServicesPolicy](set-csuserservicespolicy.md)  
[Test-CsUnifiedContactStore](test-csunifiedcontactstore.md)

