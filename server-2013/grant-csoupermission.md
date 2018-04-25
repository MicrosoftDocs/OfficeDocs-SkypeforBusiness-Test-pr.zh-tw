---
title: Grant-CsOUPermission
TOCTitle: Grant-CsOUPermission
ms:assetid: 26d8bdbf-abf0-4ca3-b9ab-fbb355fbcca1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425739(v=OCS.15)
ms:contentKeyID: 49290383
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsOUPermission

 

_**上次修改主題的時間：** 2015-03-09_

授與 Active Directory 組織單位 (OU) 的 Lync Server 管理權限。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsOUPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <String> [-Confirm [<SwitchParameter>]] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會授與使用者管理權限 (-ObjectType "user") 給網域 litwareinc.com 中的 Redmond OU。

    Grant-CsOUPermission -OU "ou=Redmond,dc=litwareinc,dc=com" -ObjectType "user"

## 範例 2

範例 2 會授與網域 litwareinc.com 中 Redmond OU 三種不同物件 (user、contact 以及 inetOrgPerson) 的管理權限。

    Grant-CsOUPermission -OU "ou=Redmond,dc=litwareinc,dc=com" -ObjectType "user","contact","inetOrgPerson"

## 範例 3

在範例 3 中，使用者管理權限會同時授與三個不同的 OU：Redmond、Dublin 以及 Tokyo。為達此目的，範例中的第一個命令會建立名為 $x 的陣列變數，以保存要授與權限之三個 Active Directory OU 的辨別名稱。第二個命令會建立 foreach 迴圈，從陣列中取用所儲存的每個 OU，並對組織單位執行 **Grant-CsOUPermission** Cmdlet。然後，該命令會為陣列中的每個 OU 授與使用者管理權限。

    $x = "ou=Redmond,dc=litwareinc,dc=com", "ou=Dublin,dc=litwareinc,dc=com", "ou=Tokyo,dc=litwareinc,dc=com"
    
    foreach ($i in $x) {Grant-CsOUPermission -OU $i -ObjectType "user"}

## 詳細描述

如果您已鎖定 Active Directory 網域 (即您已停用權限繼承)，則在安裝 Lync Server 時執行的網域準備作業將無法新增管理使用者、電腦、連絡人、應用程式連絡人和 InetOrg 人員所需的權限 (網域管理員仍然可以管理這些物件，但其他人都沒有管理權限，包括 RTCUniversalUserAdmins 群組的成員)。在此情況下，您需要使用 **Grant-CsOUPermission** Cmdlet，提供必要權限給需要的安全性群組。作法是必須根據個別容器。

請注意，此 Cmdlet 只會將權限授與一組預先定義的安全性群組；此 Cmdlet 無法用來授與權限給任意安全性群組或個別使用者。

使用 **Grant-CsOUPermission** Cmdlet 所授與的權限可於稍後使用 **Revoke-CsOUPermission** 進行移除。如果您執行該 Cmdlet，則最初授與 OU 權限的群組在指定的 Active Directory 容器上，將不再具有這些 Lync Server 管理權限。在此狀況下，您將需要一個企業系統管理員或網域系統管理員，來管理 Lync Server 或其元件的其中一項。

誰可以執行這個 Cmdlet：您必須是網域管理員，才能在本機執行 **Grant-CsOUPermission** Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsOUPermission"}

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
<td><p>這些權限涵蓋的物件類型。有效值為：</p>
<p>User</p>
<p>Computer</p>
<p>Contact</p>
<p>AppContact</p>
<p>InetOrgPerson</p>
<p>Device (建立公共區域電話所需)</p>
<p>若要在同一個的命令中指派多個物件類型，請使用逗號分隔物件類型：-ObjectType &quot;user&quot;,&quot;computer&quot;,&quot;contact&quot;。但請注意，每個命令最多只能指定三個物件類型。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要授與權限之 OU 的辨別名稱。例如：-OU &quot;ou=Redmond,dc=litwareinc,dc=com&quot;。請注意，在每個命令中只可授與權限給單一 OU。</p></td>
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
<td><p>OU 所在網域的名稱。如果未加上此參數，則 <strong>Grant-CsOUPermission</strong> Cmdlet 會在目前的網域中尋找 OU。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓系統管理員指定執行 <strong>Grant-CsOUPermission</strong> Cmdlet 時要使用之網域控制站的完整網域名稱。若未指定，該 Cmdlet 會使用第一個可用的網域控制站。</p></td>
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
<td><p>網域中通用類別目錄伺服器的 FQDN。如果您要在電腦上使用網域中的帳戶執行 <strong>Grant-CsOUPermission</strong> Cmdlet，則不需要此參數。</p></td>
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

無。**Grant-CsOUPermission** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Grant-CsOUPermission** Cmdlet 不會傳回任何物件或值。

## 請參閱

#### 其他資源

[Revoke-CsOUPermission](revoke-csoupermission.md)  
[Test-CsOUPermission](test-csoupermission.md)

