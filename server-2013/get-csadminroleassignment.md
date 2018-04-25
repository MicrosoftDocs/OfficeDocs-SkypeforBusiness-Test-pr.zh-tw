---
title: Get-CsAdminRoleAssignment
TOCTitle: Get-CsAdminRoleAssignment
ms:assetid: 61374f9b-e85a-4866-91f2-037a862ba0d6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398434(v=OCS.15)
ms:contentKeyID: 49291084
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdminRoleAssignment

 

_**上次修改主題的時間：** 2015-03-09_

傳回指派給使用者的角色型存取控制 (RBAC) 角色。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAdminRoleAssignment -Identity <String> [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回指派給使用者 kenmyer 的所有 RBAC 角色。

    Get-CsAdminRoleAssignment -Identity "kenmyer"

## 範例 2

範例 2 會傳回已針對 Lync Server 啟用之所有使用者的 RBAC 角色。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsUser** Cmdlet，以傳回組織中所有已針對 Lync Server 或 Office Communications Server 啟用之使用者的集合。然後再將該資料管線傳送到 **ForEach-Object** Cmdlet，以依序處理集合中的每個使用者帳戶來執行下列作業：1) 將使用者的顯示名稱回應到畫面上；且 2) 使用 **Get-CsAdminRoleAssignment** Cmdlet 傳回使用者的 RBAC 角色。因為 **Get-CsAdminRoleAssignment** Cmdlet 無法直接接受管線傳送的資料，所以使用者帳戶資訊必須管線傳送到 **ForEach-Object** Cmdlet。

    Get-CsUser | ForEach-Object {$_.DisplayName; Get-CsAdminRoleAssignment -Identity $_.SamAccountName}

## 詳細描述

角色型存取控制 (RBAC) 可讓系統管理員委派 Lync Server 之特定管理工作的控制權。例如，您可以不授予組織服務台完整的系統管理員權限，而是給予這些員工非常特定的權限：僅限管理使用者帳戶的權限、僅限管理 Enterprise Voice 元件的權限，以及僅限管理封存和封存伺服器的權限。此外，這些權利可限制在以下範圍：授予一位使用者管理 Enterprise Voice 的權利，但僅限於在 Redmond 網站，同時授予另一位使用者管理使用者帳戶的權利，但僅限於管理在財務組織單位 (OU) 中的帳戶。

**Get-CsAdminRoleAssignment** Cmdlet 可讓您擷取已指派給使用者的 RBAC 角色清單。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsAdminRoleAssignment** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdminRoleAssignment"}

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
<td><p>System.String</p></td>
<td><p>要傳回 RBAC 角色之使用者的 SamAccountName。您可以使用如下的命令擷取使用者的 SamAccountName：</p>
<p>Get-CsUser &quot;Ken Myer&quot; | Select-Object SamAccountName</p>
<p>請注意，當指定使用者 Identity 時，您必須使用 SamAccountName。其他在指定識別時常用到的值，例如 Active Directory 顯示名稱或使用者的 SIP 位址，將不會與 <strong>Get-CsAdminRoleAssignment</strong> 搭配使用。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取 RBAC 角色指派資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。**Get-CsAdminRoleAssignment** Cmdlet 接受管線傳送的字串值，此值代表使用者的 SamAccountName。

## 傳回類型

**Get-CsAdminRoleAssignment** Cmdlet 會傳回字串值，此值代表特定使用者所持有的 RBAC 角色。

## 請參閱

#### 其他資源

[Get-CsAdminRole](get-csadminrole.md)

