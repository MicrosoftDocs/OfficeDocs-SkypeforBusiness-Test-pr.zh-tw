---
title: New-CsPresenceProvider
TOCTitle: New-CsPresenceProvider
ms:assetid: 55110f49-f8d5-4287-89d3-ae069d8090d3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204895(v=OCS.15)
ms:contentKeyID: 49290951
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPresenceProvider

 

_**上次修改主題的時間：** 2015-03-09_

授權新的目前狀態提供者供組織使用。目前狀態提供者代表 User Services 組態設定集合的 PresenceProviders 屬性。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsPresenceProvider -Fqdn <String> -Parent <String> <COMMON PARAMETERS>

    New-CsPresenceProvider -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立新的目前狀態提供者 (包含 "fabrikam.com" 完整網域名稱)，此目前狀態提供者將會新增至全域的 User Services 組態設定集合。

    New-CsPresenceProvider -Parent "global" -Fqdn "fabrikam.com"

## 範例 2

範例 2 會將 FQDN 為 "fabrikam.com" 的目前狀態提供者新增至組織中的所有 User Services 組態集合。為達成此目的，命令會先使用 **Get-CsUserServicesConfiguration** Cmdlet 傳回所有 User Services 設定的集合。然後再將這些設定管線傳送到 ForEach-Object，取得集合中的每個項目，並為該集合建立新的目前狀態提供者 (以 "fabrikam.com" 做為目前狀態提供者 FQDN，以 User Services 集合的 Identity 做為目前狀態提供者 Parent)。

    Get-CsUserServicesConfiguration | ForEach-Object {New-CsPresenceProvider -Parent $_.Identity -Fqdn "fabrikam.com"}

## 詳細描述

**CsPresenceProvider** Cmdlet 可用於管理 User Services 組態設定中的 PresenceProviders 屬性。此外，這些設定會用於維護目前狀態資訊，包括授權之目前狀態提供者的集合。該集合會儲存在 PresenceProviders 屬性中。您可以使用 **New-CsPresenceProvider** Cmdlet 新增授權的目前狀態提供者到 User Services 組態設定集合中。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPresenceProvider"}

**Lync Server 控制台：** **New-CsPresenceProvider** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>Fqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>目前狀態提供者的完整網域名稱。例如：</p>
<p>-Fqdn &quot;fabrikam.com&quot;</p>
<p>如有使用 Fqdn 參數，也必須使用 Parent 參數。但不可在同一個命令中同時使用 Fqdn 參數與 Identity 參數。</p>
<p>請注意，FQDN 在給定的範圍內必須是唯一的。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>新目前狀態提供者的唯一識別碼。目前狀態提供者的 Identity 包含兩個部分：已套用使用者的範圍 (Parent) (例如 service:UserServer:atl-cs-001.litwareinc.com)，以及提供者的完整網域名稱。若要在全域範圍建立新的提供者，請使用類似下列的語法：</p>
<p>-Identity &quot;global/fabrikam.com&quot;</p>
<p>若要在網站範圍建立提供者，請使用如下語法：</p>
<p>-Identity &quot;site:Redmond/fabrikam.com&quot;</p>
<p>若要在服務範圍 (僅限 UserServer 服務) 建立提供者，請使用類似下列的語法：</p>
<p>-Parent &quot;UserServer:atl-cs-001.litwareinc.com&quot;</p>
<p>您不可在使用 Fqdn 及 Parent 參數的命令中使用 Identity 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要建立新目前狀態提供者的範圍。若要在全域範圍建立新的目前狀態提供者，請使用類似下列的語法：</p>
<p>-Parent &quot;global&quot;</p>
<p>若要在網站範圍建立新的提供者，請使用類似下列的語法：</p>
<p>-Parent &quot;site:Redmond&quot;</p>
<p>若要在服務範圍 (僅限 UserServer 服務) 建立提供者，請使用類似下列的語法：</p>
<p>-Parent &quot;UserServer:atl-cs-001.litwareinc.com&quot;</p>
<p>如果您使用 Parent 參數，也必須包含 Fqdn 參數。不過，Parent 參數不能與 Identity 參數一起使用。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **New-CsPresenceProvider** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsPresenceProvider** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PresenceProvider\#Decorated 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsPresenceProvider](get-cspresenceprovider.md)  
[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[Remove-CsPresenceProvider](remove-cspresenceprovider.md)  
[Set-CsPresenceProvider](set-cspresenceprovider.md)

