---
title: New-CsUserServicesPolicy
TOCTitle: New-CsUserServicesPolicy
ms:assetid: 8d7b7f79-f72e-4057-a0d1-188a87af5023
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205072(v=OCS.15)
ms:contentKeyID: 49291626
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsUserServicesPolicy

 

_**上次修改主題的時間：** 2015-03-09_

建立新的 User Services 原則。User Services 原則可指定要將使用者的連絡人儲存在 Lync Server 2013 或統一連絡人存放區中。統一連絡人存放區可讓使用者維護一組連絡人，方便使用 Lync 2013、Microsoft Outlook 及/或 Microsoft Outlook Web Access 加以存取。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsUserServicesPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Tenant <Guid>] [-UcsAllowed <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會為 Redmond 網站建立新的 User Services 原則。此原則所管理之使用者的連絡人不會移至統一連絡人存放區；那是因為 UcsAllowed 參數已設為 False ($False)。

    New-CsUserServicesPolicy -Identity "site:Redmond" -UcsAllowed $False

## 詳細描述

Lync Server 2013 中所導入的統一連絡人存放區可讓系統管理員選擇將使用者的連絡人存放在 Microsoft Exchange Server 2013，而不存放在 Lync Server；相對地，使用者也因此而能從 Microsoft Outlook、Outlook Web Access 及 Lync 2013 存取相同的連絡人集合 (除此之外，您也可繼續將連絡人存放在 Lync Server 2013 中，讓使用者可以分別維護兩組連絡人：一組供 Outlook 與 Outlook Web Access 使用，一組供 Lync 2013 使用)。

若要充分發揮統一連絡人存放區的功能，必須 (首要事項) 為使用者指派可以讓使用者使用統一連絡人存放區的 User Services 原則。User Services 原則 (可在全域、網站或個別使用者範圍設定) 只包含 UcsAllowed 一項屬性。若此屬性設為 True (並假設其他先決條件皆已符合)，當使用者下次登入 Lync Server 2013時，便會自動將其連絡人移轉到統一連絡人存放區。

若此屬性設為 False，將不會執行自動移轉。然而，單純設定 UcsAllowed 並不會將使用者的連絡人從統一連絡人存放區移回 Lync Server。為達成此目的，您必須先為使用者指派不允許使用統一連絡人存放區的 User Services 原則。然後必須使用 **Invoke-UcsRollback** Cmdlet 以「手動」方式將連絡人從統一連絡人存放區移轉回 Lync Server。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsUserServicesPolicy"}

**Lync Server 控制台：**Lync Server 控制台不提供 **New-CsUserServicesPolicy** Cmdlet 所執行的功能。

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>所要建立之原則的唯一識別碼。若要在網站範圍建立原則，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要在服務範圍建立原則，請使用類似下列的語法：-Identity &quot;UserServer:atl-cs-001.litwareinc.com&quot;</p>
<p>請注意，User Server 服務是唯一能裝載 User Services 原則的服務。</p>
<p>在個別使用者範圍也可以建立原則。若要建立個別使用者原則，請使用類似下列的語法：</p>
<p>-Identity &quot;RedmondUserServicesPolicy&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要建立新 User Services 原則之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
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

無。**New-CsUserServicesPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsUserServicesPolicy** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Policy.UserServices.UserServicesPolicy 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsUserServicesPolicy](get-csuserservicespolicy.md)  
[Grant-CsUserServicesPolicy](grant-csuserservicespolicy.md)  
[Remove-CsUserServicesPolicy](remove-csuserservicespolicy.md)  
[Set-CsUserServicesPolicy](set-csuserservicespolicy.md)

