---
title: Get-CsPresenceProvider
TOCTitle: Get-CsPresenceProvider
ms:assetid: 15f7a7d0-d6d6-491e-a2e3-04fd2d6528d5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204705(v=OCS.15)
ms:contentKeyID: 49290201
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPresenceProvider

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之目前狀態提供者的資訊。目前狀態提供者代表 User Services 組態設定集合的 PresenceProviders 屬性。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPresenceProvider [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPresenceProvider [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有目前狀態提供者的資訊。

    Get-CsPresenceProvider

## 範例 2

範例 2 會傳回下列單一目前狀態提供者的資訊：Identity 為 global/fabrikam.com 的提供者。

    Get-CsPresenceProvider -Identity "global/fabrikam.com"

## 範例 3

範例 3 會傳回網站範圍所設定之所有目前狀態提供者的資訊。為達此目的，命令會使用 Filter 參數搭配篩選值 "site:\*"。此篩選值可將傳回的資料限制在 Identity 開頭為 "site:" 字串值的目前狀態提供者。

    Get-CsPresenceProvider -Filter "site:*"

## 範例 4

範例 4 會傳回 Fqdn 屬性中某處有 "fabrikam.com" 字串值的所有目前狀態提供者。為了執行此工作，命令會先使用 **Get-CsPresenceProvider** Cmdlet 傳回設定供組織使用之所有目前狀態提供者的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Fqdn 屬性包含 (-match) "fabrikam.com" 字串值的提供者。

    Get-CsPresenceProvider | Where-Object {$_.Fqdn -match "fabrikam.com"}

## 詳細描述

**CsPresenceProvider** Cmdlet 可用於管理 User Services 組態設定中的 PresenceProviders 屬性。此外，這些設定會用於維護目前狀態資訊，包括授權之目前狀態提供者的集合。該集合會儲存在 PresenceProviders 屬性中。Get-CsPresenceProvider Cmdlet 可讓您傳回已獲授權可以在貴組織中使用之目前狀態提供者的資訊。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPresenceProvider"}

**Lync Server 控制台：** **Get-CsPresenceProvider** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>System.Strkng</p></td>
<td><p>可讓您在指定要傳回之目前狀態提供者的 Identity 時使用萬用字元。例如，若要傳回在服務範圍設定的所有目前狀態提供者，請使用下列篩選值：</p>
<p>-Filter &quot;service:*&quot;</p>
<p>請勿在同一個命令中同時使用 Filter 參數和 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>目前狀態提供者的唯一識別碼。目前狀態提供者的 Identity 包含兩個部分：已套用提供者的範圍 (Parent) (例如 service:UserServer:atl-cs-001.litwareinc.com)，以及提供者的完整網域名稱。例如，若要擷取單一目前狀態提供者，請使用類似下列的語法：</p>
<p>-Identity &quot;global/fabrikam.com&quot;</p>
<p>若要傳回特定父項的所有目前狀態提供者，直接指定範圍即可。例如，下列語法會傳回為全域範圍設定的所有目前狀態提供者：</p>
<p>-Identity &quot;global&quot;</p>
<p>如果 Identity 和 Filter 參數都未包含在內， <strong>Get-CsPresenceProvider</strong> Cmdlet 就會傳回所有提供者的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取允許的網域，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsPresenceProvider** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPresenceProvider** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PresenceProvider\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[New-CsPresenceProvider](new-cspresenceprovider.md)  
[Remove-CsPresenceProvider](remove-cspresenceprovider.md)  
[Set-CsPresenceProvider](set-cspresenceprovider.md)

