---
title: Set-CsClsSecurityGroup
TOCTitle: Set-CsClsSecurityGroup
ms:assetid: 14e7d927-8d3e-4b36-867c-d4742101e751
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204700(v=OCS.15)
ms:contentKeyID: 49290179
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClsSecurityGroup

 

_**上次修改主題的時間：** 2015-03-09_

修改集中式記錄組態安全性群組。集中式記錄讓系統管理員可以同時啟用或停用多部電腦上事件追蹤。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsClsSecurityGroup [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClsSecurityGroup [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AccessLevel <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改 Identity 為 global/HelpDesk 的集中式記錄安全性群組。在此範例中，AccessLevel 屬性設為 Tier3。

    Set-CsClsSecurityGroup -Identity "global/HelpDesk" -AccessLevel "Tier3"

## 範例 2

範例 2 會修改所有在全域範圍中設定之集中式記錄安全性群組的存取層級。為達成此目的，命令會先呼叫 **Get-CsClsSecurityGroup** Cmdlet 搭配 Filter 參數；篩選值 "global/\*" 可將傳回的資料限制在全域範圍所設定的安全性群組。然後再將這些群組管線傳送到 **Set-CsClsSecurityGroup** Cmdlet，以將每個群組的 AccessLevel 屬性設為 Tier3。

    Get-CsClsSecurityGroup -Filter "global/*" | Set-CsClsSecurityGroup-AccessLevel "Tier3"

## 範例 3

範例 3 顯示如何針對共用現有存取層級的所有集中式記錄安全性群組，使用單一命令來變更存取層級。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsClsSecurityGroup** Cmdlet，以傳回所有集中式記錄安全性群組的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 AccessLevel 等於 (-eq) GlobalAccess 的群組。接著將這些群組管線傳送到 **Set-CsClsSecurityGroup** Cmdlet，以取得每個群組，並將 AccessLevel 變更為 Tier3。

    Get-CsClsSecurityGroup | Where-Object {$_.AccessLevel -eq "GlobalAccess"} | Set-CsClsSecurityGroup -AccessLevel "Tier3"

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

在 Office 365 版的 Lync Server 中，安全性群組可用於指定有權存取寫入記檔中之個人資訊的使用者。在使用 [New-CsClsSecurityGroup](new-csclssecuritygroup.md) Cmdlet 建立安全性群組後，會將其新增至集中式記錄組態設定集合。 您可以在群組建立之後，使用 **Set-CsClsSecurityGroup** Cmdlet 修改其屬性值。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClsSecurityGroup"}

**Lync Server 控制台：** **Set-CsClsSecurityGroup** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>AccessLevel</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>字串值，用來指定要指派給群組的存取層級。存取層級是由系統管理員指派，可用來分類安全性群組。例如：</p>
<p>-AccessLevel &quot;Tier3&quot;</p>
<p>同一存取層級可由多個群組共用。目前有意義的值只有 &quot;Tier3&quot;、&quot;Tier2&quot;、&quot;Product&quot;、&quot;Ops&quot; 及 &quot;Pii&quot;。</p></td>
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
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之集中式記錄安全性群組的唯一識別碼。安全性群組識別包含群組建立所在的範圍，後接群組名稱。例如，若要修改在全域範圍建立、名為 HelpDesk 的群組，請使用下列語法：</p>
<p>-Identity &quot;global/HelpDesk&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您傳遞物件參考，而不設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Set-CsClsSecurityGroup** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SecurityGroup\#Decorated 物件執行個體。

## 傳回類型

無。反之， **Set-CsClsSecurityGroup** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SecurityGroup\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsClsSecurityGroup](get-csclssecuritygroup.md)  
[New-CsClsSecurityGroup](new-csclssecuritygroup.md)  
[Remove-CsClsSecurityGroup](remove-csclssecuritygroup.md)

