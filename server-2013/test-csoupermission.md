---
title: Test-CsOUPermission
TOCTitle: Test-CsOUPermission
ms:assetid: 9908eac9-765e-4406-bb6b-0e4dd07f85f8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398787(v=OCS.15)
ms:contentKeyID: 49291772
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsOUPermission

 

_**上次修改主題的時間：** 2015-03-09_

確認是否已設定管理指定 Active Directory 容器上之使用者、電腦和其他物件所需的權限。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsOUPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <String> [-Domain <Fqdn>] [-DomainController <Fqdn>] [-GlobalCatalog <Fqdn>] [-Report <String>]

## 範例

## 範例 1

範例 1 所示的命令會確認已在 litwareinc.com 網域的 Redmond OU 上設定使用者權限。

    Test-CsOUPermission -OU "ou=Redmond,dc=litwareinc,dc=com" -ObjectType "user"

## 詳細描述

如果您已鎖定 Active Directory 網域 (即您已停用權限繼承)，則在安裝 Lync Server 時執行的網域準備作業將無法新增管理使用者、電腦、連絡人、應用程式連絡人和 InetOrg 人員所需的權限 (網域系統管理員仍將能夠管理這些物件，但是包括 RTCUniversalServerAdmins 群組成員在內的其他人員都將不具管理權限)。在此情況下，您將需要使用 [Grant-CsOUPermission](grant-csoupermission.md) Cmdet 授與 RTCUniversalServerAdmins 群組適當的權限。此外，您必須按容器逐一進行此作業。

**Test-CsOUPermission** Cmdlet 可讓您判斷是否已新增必要的權限至指定的 Active Directory 容器。如果已套用正確的權限，則 **Test-CsOUPermission** Cmdlet 會傳回 True；如果未套用正確的權限，則會傳回 False。如果 Cmdlet 傳回 False，則您將需要執行 [Grant-CsOUPermission](grant-csoupermission.md) Cmdlet 才能進行必要的變更。

誰可以執行這個 Cmdlet：若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsOUPermission"}

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
<td><p>要檢查的物件類型。有效值為：</p>
<p>User</p>
<p>Computer</p>
<p>Contact</p>
<p>AppContact</p>
<p>InetOrgPerson</p>
<p>若要檢查多個相同種類的物件，請使用逗號來分隔物件類型：-ObjectType &quot;user&quot;,&quot;computer&quot;,&quot;contact&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要檢查之組織單位 (OU) 的辨別名稱。例如：-OU &quot;ou=Redmond,dc=litwareinc,dc=com&quot;。</p>
<p>請注意，每個命令只能用來檢查一個 OU。</p></td>
</tr>
<tr class="odd">
<td><p><em>Domain</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要檢查之 OU 所在網域的名稱。如果未加入此參數，<strong>Test-CsOUPermission</strong> Cmdlet 將在目前的網域尋找 OU。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中網域控制站的完整網域名稱 (FQDN)。如果您執行 <strong>Test-CsOUPermission</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的 FQDN。如果您執行 <strong>Test-CsOUPermission</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\OUPermissions.html&quot;。執行此 Cmdlet 時，這個檔案若已存在，便會遭到覆寫。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsOUPermission** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsOUPermission** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Grant-CsOUPermission](grant-csoupermission.md)  
[Revoke-CsOUPermission](revoke-csoupermission.md)

