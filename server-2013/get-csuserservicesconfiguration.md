---
title: Get-CsUserServicesConfiguration
TOCTitle: Get-CsUserServicesConfiguration
ms:assetid: 07884f7a-d9f7-4a3f-a5ef-7f4ba71c2769
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398133(v=OCS.15)
ms:contentKeyID: 49289990
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUserServicesConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之 User Services 組態設定的資訊。User Services 可用於維護目前狀態資訊及管理會議。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsUserServicesConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsUserServicesConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織目前所使用之所有 User Services 組態設定的集合。作法是呼叫不含任何參數的 **Get-CsUserServicesConfiguration** Cmdlet。

    Get-CsUserServicesConfiguration

## 範例 2

在範例 2 中只會傳回 User Services 組態設定的一個集合：Identity 為 site:Redmond 的集合。因為識別必須是唯一的，所以這個命令永遠不會傳回多個項目。

    Get-CsUserServicesConfiguration -Identity site:Redmond

## 範例 3

範例 3 會傳回已套用在服務範圍的所有 User Services 組態設定集合。作法是呼叫 **Get-CsUserServicesConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "service:\*" 可將傳回的資料限制在 Identity 開頭為 "service:" 字元的設定。根據定義，這些是在服務範圍設定的設定。

    Get-CsUserServicesConfiguration -Filter "service:*"

## 範例 4

範例 4 會傳回允許使用者能有超過 250 個連絡人的所有 User Services 組態設定。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsUserServicesConfiguration** Cmdlet，以傳回目前正在使用的所有 User Services 組態設定集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 MaxContacts 屬性大於 250 的設定。

    Get-CsUserServicesConfiguration | Where-Object {$_.MaxContacts -gt 250}

## 範例 5

範例 5 會回報匿名使用者寬限期間大於 10 分鐘的 User Services 組態設定。為了執行此工作，命令會呼叫不含任何參數的 **Get-CsUserServicesConfiguration** Cmdlet，以傳回組織目前使用之所有使用者負組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 AnonymousUserGracePeriod 屬性大於 10 分鐘的設定 (00 小時:10 分鐘：00 秒) 的 A/V Edge 組態設定。

    Get-CsUserServicesConfiguration | Where-Object {$_.AnonymousUserGracePeriod -gt "00:10:00"}

## 詳細描述

Lync Server 依賴 User Services 協助維護使用者的目前狀態資訊，以及管理會議。**CsUserServicesConfiguration** Cmdlet 依序用於管理全域、網站和服務範圍的 User Services 設定 (請注意，可主控 User Services 組態設定的唯一服務為 User Services 本身)。這些設定有助於決定使用者可擁有的連絡人數目、使用者可在任何一個時間中排程的會議數，以及所指定的會議可保持為作用中的時間長度等作業。

**Get-CsUserServicesConfiguration** Cmdlet 可讓系統管理員擷取目前正在使用的任何 (或所有) User Services 組態設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsUserServicesConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUserServicesConfiguration"}

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
<td><p>可讓您在擷取 User Services 組態設定的一或多個集合時使用萬用字元。例如，若要傳回在網站範圍所設定的所有設定，請使用下列語法：-Filter &quot;site:*&quot;。若要傳回在服務範圍所設定的所有設定，請使用下列語法：-Filter &quot;service:*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之 User Services 組態設定的唯一識別碼。若要傳回全域設定，請使用下列語法：-Identity global。若要傳回在此網站範圍設定的設定，請使用下列語法：-Identity site:Redmond。若要傳回該服務層級的設定，請使用如下所示的語法：-Identity service:UserServer:atl-cs-001.litwareinc.com。</p>
<p>如果省略此參數，則 <strong>Get-CsUserServicesConfiguration</strong> Cmdlet 會傳回組織目前所使用之所有 User Services 組態設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取 User Services 組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsUserServicesConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsUserServicesConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.UserServicesSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsUserServicesConfiguration](new-csuserservicesconfiguration.md)  
[Remove-CsUserServicesConfiguration](remove-csuserservicesconfiguration.md)  
[Set-CsUserServicesConfiguration](set-csuserservicesconfiguration.md)

