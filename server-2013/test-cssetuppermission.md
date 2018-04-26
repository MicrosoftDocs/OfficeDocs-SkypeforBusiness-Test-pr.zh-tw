---
title: Test-CsSetupPermission
TOCTitle: Test-CsSetupPermission
ms:assetid: 604ccb97-278a-4588-9ab8-991aaabae275
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398428(v=OCS.15)
ms:contentKeyID: 49291078
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsSetupPermission

 

_**上次修改主題的時間：** 2015-03-09_

確認安裝 Lync Server 所需的權限，或指定的 Active Directory 容器上是否已有設定其元件。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsSetupPermission -ComputerOU <String> [-Domain <Fqdn>] [-DomainController <Fqdn>] [-GlobalCatalog <Fqdn>] [-Report <String>]

## 範例

## 範例 1

範例 1 所示的命令會先檢查必要的安裝權限是否已套用到 litwareinc.com 網域中的 CsServers OU。

    Test-CsSetupPermission -ComputerOU "ou=CsServers,dc=litwareinc,dc=com"

## 詳細描述

安裝 Lync Server 時會進行的網域準備無法自動新增權限，該權限可讓 RTCUniversalServerAdmins 群組成員執行 **Enable-CsTopology** Cmdlet。這代表根據預設，您必須為網域系統管理員才能啟用拓樸。您必須執行 **Grant-CsSetupPermissions** Cmdlet，才能給予 RTCUniversalServerAdmins 群組成員權限以啟用拓樸。此外，您必須針對每個裝載執行 Lync Server 之電腦的 Active Directory 容器，執行此 Cmdlet。

**Test-CsSetupPermission** Cmdlet 可讓您判定必要的權限是否已新增到指定的 Active Directory 容器 (亦即裝載執行 Lync Server 之電腦的容器)。如果已套用正確的權限，**Test-CsSetupPermission** Cmdlet 會傳回 True，如果尚未套用正確的權限，則會傳回 False。如果 Cmdlet 傳回 False，則您必須執行 **Grant-CsSetupPermission** Cmdlet 才能對 Active Directory 容器進行必要的變更。

誰可以執行這個 Cmdlet：執行 Windows PowerShell 提示字元提供的下列命令，即可傳回指派給此 Cmdlet (包括您自行建立的任何自訂 RBAC 角色) 的所有角色型存取控制 (RBAC) 角色清單：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsSetupPermission"}

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
<td><p><em>ComputerOU</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>組織單位 (OU) 的辨別名稱，包含執行 Lync Server 之電腦的帳戶。例如：&quot;ou=CsServers,dc=litwareinc,dc=com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Domain</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要檢查之 OU 所在網域的名稱。如果未包含此參數，<strong>Test-CsSetupPermission</strong> Cmdlet 將在目前的網域尋找 OU。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中網域控制站的完整網域名稱 (FQDN)。如果您執行 <strong>Test-CsSetupPermission</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的 FQDN。如果您執行 <strong>Test-CsSetupPermission</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>Cmdlet 執行時，在畫面上的詳細活動報告。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsSetupPermission** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsSetupPermission** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Grant-CsSetupPermission](grant-cssetuppermission.md)  
[Revoke-CsSetupPermission](revoke-cssetuppermission.md)

