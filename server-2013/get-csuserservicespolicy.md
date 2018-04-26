---
title: Get-CsUserServicesPolicy
TOCTitle: Get-CsUserServicesPolicy
ms:assetid: 424cd3ca-6df4-4715-97f1-95d2da3b6d90
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204838(v=OCS.15)
ms:contentKeyID: 49290735
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUserServicesPolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之 User Services 原則的資訊。User Services 原則可指定要將使用者的連絡人儲存在 Lync Server 2013 或統一連絡人存放區中。統一連絡人存放區可讓使用者維護一組連絡人，方便使用 Lync 2013、Microsoft Outlook 及/或 Microsoft Outlook Web Access 加以存取。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsUserServicesPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsUserServicesPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織目前所使用之所有 User Services 原則的資訊。

    Get-CsUserServicesPolicy

## 範例 2

範例 2 會傳回單一 User Services 原則 (即為 Redmond 網站設定的原則) 的資訊。

    Get-CsUserServicesPolicy -Identity "site:Redmond"

## 範例 3

範例 3 會傳回在網站範圍設定之所有 User Services 原則的資訊。作法是加入 Filter 參數及篩選值 "site:\*"。

    Get-CsUserServicesPolicy -Filter "site:*"

## 範例 4

範例 4 所示的命令會傳回已停用統一連絡人存放區之 User Services 原則的資訊。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsUserServicesPolicy** Cmdlet，以傳回設定供組織所用之所有 User Services 原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 UcsAllowed 屬性設為 False 的原則。

    Get-CsUserServicesPolicy | Where-Object {$_.UcsAllowed -eq $False}

## 詳細描述

Lync Server 2013 中所導入的統一連絡人存放區可讓系統管理員選擇將使用者的連絡人存放在 Microsoft Exchange Server 2013，而不存放在 Lync Server；相對地，使用者也因此而能從 Microsoft Outlook、Outlook Web Access 及 Lync 2013 存取相同的連絡人集合 (除此之外，您也可繼續將連絡人存放在 Lync Server 2013 中，讓使用者可以分別維護兩組連絡人：一組供 Outlook 與 Outlook Web Access 使用，一組供 Lync 2013 使用)。

若要充分發揮統一連絡人存放區的功能，必須 (首要事項) 為使用者指派可以讓使用者使用統一連絡人存放區的 User Services 原則。User Services 原則 (可在全域、網站或個別使用者範圍設定) 只包含 UcsAllowed 一項屬性。若此屬性設為 True (並假設其他先決條件皆已符合)，當使用者下次登入 Lync Server 2013時，便會自動將其連絡人移轉到統一連絡人存放區。

若此屬性設為 False，將不會執行自動移轉。然而，單純設定 UcsAllowed 並不會將使用者的連絡人從統一連絡人存放區移回 Lync Server。為達成此目的，您必須先為使用者指派不允許使用統一連絡人存放區的 User Services 原則。然後必須使用 **Invoke-UcsRollback** Cmdlet 以「手動」方式將連絡人從統一連絡人存放區移轉回 Lync Server。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUserServicesPolicy"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsUserServicesPolicy** Cmdlet 所執行的功能。

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您在指定要擷取的一或多個原則時使用萬用字元。例如，下列語法會傳回在網站範圍設定的所有原則：</p>
<p>-Filter &quot;site:*&quot;</p>
<p>下列語法會傳回所有在個別使用者範圍設定的原則：</p>
<p>-Filter &quot;tag:*&quot;</p>
<p>您無法在同一個命令中同時使用 Filter 與 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之原則的唯一識別碼。若要傳回全域原則，請使用下列語法：</p>
<p>-Identity global</p>
<p>若要傳回在網站範圍設定的原則，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;</p>
<p>若要傳回在服務範圍設定的原則，請使用類似下列的語法：&quot;UserServer:atl-cs-001.litwareinc.com&quot;</p>
<p></p>
<p>請注意，UserServer 服務是唯一能主控 User Services 原則的服務。</p>
<p></p>
<p>原則也可以在個別使用者範圍設定。若要傳回其中一個原則，請使用類似下列的語法：</p>
<p>-Identity &quot;RedmondUserServicesPolicy&quot;</p>
<p>若未加入此參數，將會傳回設定供組織使用的所有 User Services 原則。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取 User Services 原則資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>使用此參數時，會針對指定的 商務用 Skype Online 租用戶擷取 User Services 原則。例如：</p>
<p>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>請勿在同一個命令中同時使用 Tenant 參數及 Identity 參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsUserServicesPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsUserServicesPolicy** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.UsersServices.UserServicesPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Grant-CsUserServicesPolicy](grant-csuserservicespolicy.md)  
[New-CsUserServicesPolicy](new-csuserservicespolicy.md)  
[Remove-CsUserServicesPolicy](remove-csuserservicespolicy.md)  
[Set-CsUserServicesPolicy](set-csuserservicespolicy.md)

