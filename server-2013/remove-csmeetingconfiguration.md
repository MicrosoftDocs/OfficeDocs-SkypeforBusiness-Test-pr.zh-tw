---
title: Remove-CsMeetingConfiguration
TOCTitle: Remove-CsMeetingConfiguration
ms:assetid: a5d4c758-25f6-4cdb-a5b7-dbb0fb1d8488
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412775(v=OCS.15)
ms:contentKeyID: 49291902
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsMeetingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

**Remove-CsMeetingConfiguration** Cmdlet 可讓您刪除現有的會議組態設定集合。會議組態設定有助於規定使用者所能建立的會議類型，以及控制匿名使用者和電話撥入式會議使用者如何 (或能否) 加入這些會議。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsMeetingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，將 Identity 為 site:Redmond 的會議組態設定移除。從 Redmond 網站移除這些設定時，網站中的使用者會自動繼承全域會議組態設定。

    Remove-CsMeetingConfiguration -Identity site:Redmond

## 範例 2

範例 2 所示的命令會移除所有在網站範圍設定的會議設定。為達成此目的，命令會先呼叫 **Get-CsMeetingConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "site:\*" 可確保只會選取 Identity 開頭為字元 "site:" 的設定。然後再將此篩選後的集合管線傳送到 **Remove-CsMeetingConfiguration** Cmdlet，以刪除集合中的每一個項目。

    Get-CsMeetingConfiguration -Filter "site:*" | Remove-CsMeetingConfiguration

## 範例 3

範例 3 會刪除 AdmitAnonymousUsersbyDefault 屬性為 True 的會議組態設定的每一個集合。為達此目的，命令會先呼叫 **Get-CsMeetingConfiguration** Cmdlet 以傳回目前所使用之所有會議組態設定的集合。然後再將此集合以管線傳送到 **Where-Object** Cmdlet，以挑出 AdmitAnonymousUsersByDefault property 屬性等於 True 的設定。接著將篩選後的集合以管線傳送到 **Remove-CsMeetingConfiguration** Cmdlet，以繼續移除該集合中的每一個項目。

    Get-CsMeetingConfiguration | Where-Object {$_.AdmitAnonymousUsersByDefault -eq $True} | Remove-CsMeetingConfiguration

## 詳細描述

線上會議是 Lync Server 的一部分。 **CsMeetingConfiguration** Cmdlet 可讓系統管理員控制使用者所能建立的會議類型，以及指定會議處理匿名使用者與電話撥入式會議使用者的方式。例如，您可以設定會議自動允許透過公用交換電話網路 (PSTN) 撥入的人員加入會議，也可設定會議，不讓電話撥入式使用者自動加入會議，而將其路由到會議大廳。這些電話撥入式使用者會一直保留在大廳，直到簡報者允許其加入會議為止。

會議組態設定可以指派到全域、網站或服務範圍。如果您在網站或服務範圍建立新設定，之後可以用 **Remove-CsMeetingConfiguration** Cmdlet 移除這些設定。 **Remove-CsMeetingConfiguration** Cmdlet 也可以用於通用會議設定。但在此情況下，不會移除設定；因為全域設定是不能移除的。而是會將全域集合內的所有屬性都重設為預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsMeetingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsMeetingConfiguration"}

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
<td><p>要移除的會議組態設定的唯一識別碼。若要「移除」全域設定，請使用下列語法：-Identity global。(如前所述，您無法真正移除全域設定，您所能做的只有將屬性重設回預設值)。若要將設定從網站範圍移除，請使用如下語法：-Identity site:Redmond。移除服務設定可以使用下列語法：-Identity service:UserServer:atl-cs-001.litwareinc.com。</p>
<p>請注意，如有指定 Identity，即無法使用萬用字元。</p></td>
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
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>所刪除的會議組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.MeetingConfiguration 物件。 **Remove-CsMeetingConfiguration** Cmdlet 接受會議組態物件管線傳送的執行個體。

## 傳回類型

無。反之， **Remove-CsMeetingConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.MeetingConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsMeetingConfiguration](get-csmeetingconfiguration.md)  
[New-CsMeetingConfiguration](new-csmeetingconfiguration.md)  
[Set-CsMeetingConfiguration](set-csmeetingconfiguration.md)

