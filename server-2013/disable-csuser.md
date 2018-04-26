---
title: Disable-CsUser
TOCTitle: Disable-CsUser
ms:assetid: 92e7e29e-2620-4852-9e4a-2fd3569bb095
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398747(v=OCS.15)
ms:contentKeyID: 49291689
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsUser

 

_**上次修改主題的時間：** 2015-03-09_

修改指定使用者的 Active Directory 帳戶，以禁止使用者使用 Lync Server 用戶端 (例如 Lync 2013)。**Disable-CsUser** Cmdlet 只會限制 Lync Server 的相關活動，而不會停用或移除使用者的 Active Directory 帳戶。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Disable-CsUser -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會停用使用者 Ken Myer 的 Lync Server 帳戶。在此範例中，使用者的顯示名稱可用來表示其 Identity。

    Disable-CsUser -Identity "Ken Myer"

## 範例 2

範例 2 會停用財務部門所有使用者的 Lync Server 帳戶。為了執行此工作，命令會先使用 **Get-CsUser** Cmdlet 並搭配 LdapFilter 參數，以傳回屬於財務部門之所有使用者的集合。然後，此集合會管線傳送到 **Disable-CsUser** Cmdlet，以停用集合中的每個帳戶。

    Get-CsUser -LdapFilter "Department=Finance" | Disable-CsUser

## 範例 3

此範例會停用所有目前未指派至登錄器集區的使用者帳戶。為達成此目的，會呼叫 **Get-CsUser** Cmdlet 並搭配 UnassignedUser 參數。此參數可將傳回的資料限制在其使用者帳戶有效，但未被指派到登錄器集區的使用者。然後，此集合會管線傳送到 Disable-CsUser Cmdlet，以停用集合中的每個帳戶。

    Get-CsUser -UnassignedUser | Disable-CsUser

## 詳細描述

**Disable-CsUser** Cmdlet 會從 Active Directory 使用者帳戶中刪除所有與 Lync Server 相關的屬性資訊，以禁止使用者登入 Lync Server。當您執行 **Disable-CsUser** Cmdlet 時，所有與 Lync Server 相關的屬性都會自該帳戶移除，包括任何指派給該帳戶之個別使用者原則的 Identity。之後您可以使用 **Enable-CsUser** Cmdlet 重新啟用帳戶。但您必須重新建立先前與該帳戶相關聯的所有 Lync Server 相關資訊 (例如原則指派)。若要禁止使用者登入 Lync Server，但不想失去帳戶的所有資訊，可改用 **Set-CsUser** Cmdlet。如需詳細資訊，請參閱 [Set-CsUser](set-csuser.md) Cmdlet 說明主題。

以 **Disable-CsUser** Cmdlet 停用帳戶之後，**Get-CsUser** Cmdlet 不會再傳回受影響的使用者；這是因為使用者已無有效的 Lync Server 帳戶。若要擷取已停用使用者帳戶的資訊，請使用 **Get-CsAdUser** Cmdlet。

此外，屬於刪除的使用者帳戶的使用者資料也會從後端資料庫移除；例如，使用者會被從組織的連絡人清單移除，該使用者排程的任何會議也會被一併刪除。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Disable-CsUser** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Disable-CsUser"}

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
<td><p>表示要停用之使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。您也可以使用 Active Directory 辨別名稱來參照使用者帳戶。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以停用使用者帳戶。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-cs-001) 或其完整網域名稱 (FQDN) (例如，atl-cs-001.litwareinc.com)。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您經由管線傳遞代表所要停用使用者帳戶的使用者物件。根據預設，<strong>Disable-CsUser</strong> Cmdlet 不會沿管線傳遞任何物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Disable-CsUser** Cmdlet 接受管線傳送的字串值，該值代表已經針對 Lync Server 啟用的使用者帳戶 Identity。此 Cmdlet 也接受管線傳送的 Active Directory 使用者物件執行個體。

## 傳回類型

**Disable-CsUser** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件的執行個體。

## 請參閱

#### 其他資源

[Enable-CsUser](enable-csuser.md)  
[Get-CsUser](get-csuser.md)

