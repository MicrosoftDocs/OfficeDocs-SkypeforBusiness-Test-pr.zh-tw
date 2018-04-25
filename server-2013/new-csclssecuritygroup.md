---
title: New-CsClsSecurityGroup
TOCTitle: New-CsClsSecurityGroup
ms:assetid: e42f2d5f-7720-4b69-8563-48172120d8d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205359(v=OCS.15)
ms:contentKeyID: 49292607
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClsSecurityGroup

 

_**上次修改主題的時間：** 2015-03-09_

建立新的集中式記錄組態安全性群組。集中式記錄讓系統管理員可以同時啟用或停用多部電腦上事件追蹤。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsClsSecurityGroup -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsClsSecurityGroup -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -AccessLevel <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立 Identity 為 global/HelpDesk 的新集中式記錄安全性群組。在此範例中，AccessLevel 屬性設為 Tier3。

    New-CsClsSecurityGroup -Identity "global/HelpDesk" -AccessLevel "Tier3"

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

在 商務用 Skype Online 中，安全性群組可用於判斷有權存取要寫入記錄檔之個人識別資訊的使用者。使用 New-CsClsSecurityGroup Cmdlet 建立安全性群組之後，會將其新增至集中式記錄組態設定的集合中。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClsSecurityGroup"}

**Lync Server 控制台：** **New-CsClsSecurityGroup** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>指定指派給群組之存取層級的字串值。存取層級是由系統管理員指派的任意字串值，可用來分類安全性群組。例如：</p>
<p>-AccessLevel &quot;Tier3&quot;</p>
<p>同一存取層級可由多個群組共用。目前有意義的值只有 &quot;Tier3&quot;、&quot;Tier2&quot;、&quot;Product&quot;、&quot;Ops&quot; 及 &quot;Pii&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>新安全性群組的唯一識別碼。安全性群組的 Identity 包含集中式記錄組態範圍 (建立群組的位置) 及唯一的安全性群組名稱。例如，若要建立名為 HelpDesk 的全域安全性群組，請使用下列語法：</p>
<p>-Identity &quot;global/HelpDesk&quot;</p>
<p>如有使用 Identity 參數，即不可再使用 name 參數或 Parent 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>新安全性群組的唯一名稱。例如：</p>
<p>-Name &quot;HelpDesk&quot;</p>
<p>如有使用 Name 參數，也必須使用 Parent 參數。但請勿在使用 Name 及 Parent 參數的命令中使用 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>集中式記錄組態設定的範圍，亦即新安全性群組的所在位置。例如，若要新增安全性群組至全域設定，請使用下列語法：</p>
<p>-Parent &quot;global&quot;</p>
<p>您可以使用此命令傳回所有集中式記錄「父系」的識別：</p>
<p>Get-CsCentralizedLoggingConfiguration | Select-Object Identity</p>
<p>如有使用 Name 參數，也必須使用 Parent 參數。但請勿在使用 Name 及 Parent 參數的命令中使用 Identity 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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

無。 **New-CsClsSecurityGroup** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsClsSecurityGroup** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SecurityGroup\#Decorated 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsClsSecurityGroup](get-csclssecuritygroup.md)  
[Remove-CsClsSecurityGroup](remove-csclssecuritygroup.md)  
[Set-CsClsSecurityGroup](set-csclssecuritygroup.md)

