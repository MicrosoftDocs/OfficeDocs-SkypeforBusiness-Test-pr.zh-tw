---
title: Revoke-CsOUPermission
TOCTitle: Revoke-CsOUPermission
ms:assetid: de0542c9-6d11-4038-9b4a-757338d61fae
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398977(v=OCS.15)
ms:contentKeyID: 49292552
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Revoke-CsOUPermission

 

_**上次修改主題的時間：** 2015-03-09_

撤銷授與 Active Directory 組織單位 (OU) 的 Lync Server 管理權限。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Revoke-CsOUPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <String> [-Confirm [<SwitchParameter>]] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會撤銷網域 litwareinc.com 中 Redmond OU 的使用者管理權限 (-ObjectType "user")。

    Revoke-CsOUPermission -OU "ou=Redmond,dc=litwareinc,dc=com" -ObjectType "user"

## 範例 2

在範例 2 中，這些不同的管理權限 (使用者、連絡人及 inetOrgPerson 物件) 會從網域 litwareinc.com 中的 Redmond OU 進行移除。

    Revoke-CsOUPermission -OU "ou=Redmond,dc=litwareinc,dc=com" -ObjectType "user","contact","inetOrgPerson"

## 詳細描述

如果您已鎖定 Active Directory 網域 (即您已停用權限繼承)，則在安裝 Lync Server 時執行的網域準備作業將無法新增管理使用者、電腦、連絡人、應用程式連絡人和 InetOrg 人員所需的權限 (企業系統管理員和網域系統管理員仍將能管理這些物件，但是包括 RTCUniversalServerAdmins 群組成員在內的其他人員都將不具管理權限)。在此情況下，您將需要使用 **Grant-CsOUPermission** Cmdlet，為所需的安全性群組授與必要的權限。這必須針對包含 Lync Server 使用者帳戶的每個 Active Directory 容器逐一完成。

使用 **Grant-CsOUPermission** Cmdlet 授與的權限日後可以用 **Revoke-CsOUPermission** 來移除。如果您針對 OU 執行 **Revoke-CsOUPermission** Cmdlet，則您必須是企業系統管理員或網域管理員，才能管理該 OU 中的 Lync Server 使用者。

誰可以執行這個 Cmdlet：您必須是網域系統管理員，才能本機執行 **Revoke-CsOUPermission** Cmdlet。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Revoke-CsOUPermission"}

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
<td><p><em>ObjectType</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.ObjectType</p></td>
<td><p>這些權限所涵蓋的物件類型。有效值為：</p>
<p>User</p>
<p>Computer</p>
<p>Contact</p>
<p>AppContact</p>
<p>InetOrgPerson</p>
<p>若要以同一個命令撤銷多個物件類型的權限，請使用逗號分隔物件類型：-ObjectType &quot;user&quot;,&quot;computer&quot;,&quot;contact&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要移除權限之 OU 的辨別名稱。例如：-OU &quot;ou=Redmond,dc=litwareinc,dc=com&quot;。您僅可從個別命令單一 OU 移除權限。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Domain</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>OU 所在網域的名稱。如果沒有加入此參數， <strong>Revoke-CsOUPermission</strong> Cmdlet 將在目前的網域尋找 OU。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓系統管理員指定執行 <strong>Revoke-CsOUPermission</strong> Cmdlet 時要使用之網域控制站的完整網域名稱 (FQDN)。若未指定，該 Cmdlet 會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的完整網域名稱。如果您執行 <strong>Revoke-CsOUPermission</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\OUPermissions.html&quot;</p></td>
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

無。 **Revoke-CsOUPermission** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Revoke-CsOUPermission** Cmdlet 不會傳回任何物件或值。

## 請參閱

#### 其他資源

[Grant-CsOUPermission](grant-csoupermission.md)  
[Test-CsOUPermission](test-csoupermission.md)

