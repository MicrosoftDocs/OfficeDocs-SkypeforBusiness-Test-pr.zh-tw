---
title: Remove-CsUserServicesPolicy
TOCTitle: Remove-CsUserServicesPolicy
ms:assetid: 025f9a94-ff44-4e06-8b14-721f8fd9924f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204629(v=OCS.15)
ms:contentKeyID: 49289912
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUserServicesPolicy

 

_**上次修改主題的時間：** 2015-03-09_

刪除現有的 User Services 原則。User Services 原則可指定要將使用者的連絡資訊儲存在 Lync Server 2013 或統一連絡人存放區中。統一連絡人存放區可讓使用者維護一組連絡人，方便使用 Lync 2013、Microsoft Outlook 及/或 Microsoft Outlook Web Access 加以存取。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsUserServicesPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除個別使用者的 User Services 原則 RedmondUserServicesPolicy。

    Remove-CsUserServicesPolicy -Identity "RedmondUserServicesPolicy"

## 範例 2

範例 2 會刪除在此網站範圍所設定的所有 User Services 原則。為達成此目的，命令會先使用 **Get-CsUserServicesPolicy** Cmdlet 和 Filter 值傳回在網站範圍所設定之所有原則的集合；作法是使用篩選值 "site:\*"。然後再將所產生的集合管線傳送到 **Remove-CsUserServicesPolicy** Cmdlet，以刪除集合中的每個原則。

    Get-CsUserServicesPolicy -Filter "site:*" | Remove-CsUserServicesPolicy

## 範例 3

範例 3 會刪除所有允許使用統一連絡人存放區的 User Services 原則。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsUserServicesPolicy** Cmdlet，以傳回設定供組織使用之所有 User Services 原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 UcsAllowed 屬性等於 (-eq) True ($True) 的原則。接著再將這些原則管線傳送到 **Remove-CsUserServicesPolicy** Cmdlet 移除。

    Get-CsUserServicesPolicy | Where-Object {$_.UcsAllowed -eq $True} | Remove-CsUserServicesPolicy

## 詳細描述

Lync Server 2013 中所導入的統一連絡人存放區可讓系統管理員選擇將使用者的連絡人存放在 Microsoft Exchange Server 2013，而非存放在 Lync Server；因此，使用者就能從存取 Outlook、Outlook Web Access 及 Lync 2013 中的相同連絡人集合 (或者，您也可繼續將連絡人存放在 Lync Server 2013 中，讓使用者可以保留兩組個別的連絡人：一組供 Outlook 與 Outlook Web Access 使用，一組供 Lync 2013使用)。

若要充分發揮統一連絡人存放區的功能，必須 (首要事項) 為使用者指派可以讓使用者使用統一連絡人存放區的 User Services 原則。User Services 原則 (可在全域、網站或個別使用者範圍設定) 只包含 UcsAllowed 一項屬性。若此屬性設為 True (並假設其他先決條件皆已符合)，當使用者下次登入 Lync Server 2013時，便會自動將其連絡人移轉到統一連絡人存放區。

若此屬性設為 False，將不會執行自動移轉。然而，單純設定 UcsAllowed 並不會將使用者的連絡人從統一連絡人存放區移回 Lync Server。為達成此目的，您必須先為使用者指派不允許使用統一連絡人存放區的 User Services 原則。然後必須使用 **Invoke-UcsRollback** Cmdlet 以「手動」方式將連絡人從統一連絡人存放區移轉回 Lync Server。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUserServicesPolicy"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Remove-CsUserServicesPolicy** Cmdlet 所執行的功能。

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
<td><p>要刪除之原則的唯一識別碼。若要移除在網站範圍所設定的原則，可使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要移除在服務範圍所設定的原則，可使用類似下列的語法：</p>
<p>-Identity &quot;UserServer:atl-cs-001.litwareinc.com&quot;</p>
<p>使用者伺服器服務是唯一可以主控 User Services 原則的服務。</p>
<p>個別使用者範圍中的原則也可移除。若要移除個別使用者原則，請使用類似下列的語法：</p>
<p>-Identity &quot;RedmondUserServicesPolicy&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>移除指派給指定 商務用 Skype Online 租用戶的 User Services 原則。移除指派給租用戶的原則時，必須加入 Identity 參數並設定 &quot;global&quot; 參數值：</p>
<p>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Remove-CsUserServicesPolicy** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Poligy.UserServices.UserServicesPolicy 物件執行個體。

## 傳回類型

無。反之，**Remove-CsUserServicesPolicy** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Policy.UserServices.UserServicesPolicy 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsUserServicesPolicy](get-csuserservicespolicy.md)  
[Grant-CsUserServicesPolicy](grant-csuserservicespolicy.md)  
[New-CsUserServicesPolicy](new-csuserservicespolicy.md)  
[Set-CsUserServicesPolicy](set-csuserservicespolicy.md)

