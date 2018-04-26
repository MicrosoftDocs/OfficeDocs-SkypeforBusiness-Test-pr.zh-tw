---
title: Set-CsUserServicesPolicy
TOCTitle: Set-CsUserServicesPolicy
ms:assetid: fbe18ddf-5094-4d8b-ad27-75b73173b8c4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205414(v=OCS.15)
ms:contentKeyID: 49292908
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUserServicesPolicy

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的 User Services 原則。User Services 可決定要將使用者的連絡人儲存在 Lync Server 2013 或統一連絡人存放區中。使用者可利用統一連絡人存放區維護一組連絡人，供 Lync 2013、Outlook 及/或 Outlook Web Access 存取。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsUserServicesPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsUserServicesPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-UcsAllowed <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會針對個別使用者 User Services 原則 RedmondUserServicesPolicy 停用整合連絡人存放區。這表示受此原則管理的使用者無法在整合連絡人存放區中儲存連絡人。

    Set-CsUserServicesPolicy -Identity "RedmondUserServicesPolicy" -UcsAllowed $False

## 範例 2

在範例 2 中，在網站範圍設定的所有 User Services 原則都會被修改，以停用統一連絡人存放區。為達成此目的，命令會先呼叫 **Get-CsUserServicesPolicy** Cmdlet 和 Filter 參數，傳回在網站範圍所設定之所有原則的集合。然後此集合就會透過管道傳送至 **Set-CsUserServicesPolicy** Cmdlet，以取得集合中的每個原則，並將 UcsAllowed 屬性設為 False ($False)。

    Get-CsUserServicesPolicy -Filter "site:*" | Set-CsUserServicesPolicy -UcsAllowed $False

## 詳細描述

Lync Server 2013 中所導入的統一連絡人存放區可讓系統管理員選擇將使用者的連絡人存放在 Microsoft Exchange Server 2013，而不存放在 Lync Server；相對地，使用者也因此而能從 Outlook、Outlook Web Access 及 Lync 2013 存取同一組連絡人 (除此之外，您也可繼續將連絡人存放在 Lync Server 2013 中，讓使用者可以分別維護兩組連絡人：一組供 Outlook 與 Outlook Web Access 使用，一組供 Lync 2013 使用)。

若要充分發揮統一連絡人存放區的功能，必須 (首要事項) 為使用者指派可以讓使用者使用統一連絡人存放區的 User Services 原則。User Services 原則 (可在全域、網站或個別使用者範圍設定) 只包含 UcsAllowed 一項屬性。若此屬性設為 True (並假設其他先決條件皆已符合)，當使用者下次登入 Lync Server 2013時，便會自動將其連絡人移轉到統一連絡人存放區。

若此屬性設為 False，將不會執行自動移轉。然而，單純設定 UcsAllowed 並不會將使用者的連絡人從統一連絡人存放區移回 Lync Server。為達成此目的，您必須先為使用者指派不允許使用統一連絡人存放區的 User Services 原則。然後必須使用 **Invoke-CsUcsRollback** Cmdlet 以「手動」方式將連絡人從統一連絡人存放區移轉回 Lync Server。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUserServicesPolicy"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Set-CsUserServicesPolicy** Cmdlet 所執行的功能。

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之原則的唯一識別碼。若要修改全域原則，請使用下列語法：</p>
<p>-Identity &quot;global&quot;</p>
<p>若要修改在網站範圍設定的原則，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要修改在服務範圍設定的原則，請使用類似下列的語法：</p>
<p>-Identity &quot;UserServer:atl-cs-001.litwareinc.com&quot;</p>
<p>請注意，UserServer 服務是唯一能主控 User Services 原則的服務。</p>
<p>若未加入此參數，則 <strong>Set-CsUserServicesPolicy</strong> Cmdlet 將會自動修改全域原則。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>所修改的 User Services 原則之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="even">
<td><p><em>UcsAllowed</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時 (預設值)，受此原則影響的使用者會自動移轉至統一連絡人存放區 (假設使用者具有 Microsoft Exchange Server 2013 帳戶並使用 Lync 2013 登入)。設為 False 時，可從統一連絡人存放區移除使用者，但前提是必須使用 <strong>Invoke-CsUcsRollback</strong> Cmdlet「手動」移除。</p></td>
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

**Set-CsUserServicesPolicy** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Policy.UserServices.UserServicesPolicy 物件執行個體。

## 傳回類型

無。反之， **Set-CsUserServicesPolicy** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Policy.UserServices.UserServicesPolicy 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsUserServicesPolicy](get-csuserservicespolicy.md)  
[Grant-CsUserServicesPolicy](grant-csuserservicespolicy.md)  
[New-CsUserServicesPolicy](new-csuserservicespolicy.md)  
[Remove-CsUserServicesPolicy](remove-csuserservicespolicy.md)

