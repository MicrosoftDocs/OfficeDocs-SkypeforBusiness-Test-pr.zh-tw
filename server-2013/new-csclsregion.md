---
title: New-CsClsRegion
TOCTitle: New-CsClsRegion
ms:assetid: 09396d6e-e7ec-43b8-9f5b-d9cac30348f6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204658(v=OCS.15)
ms:contentKeyID: 49290017
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClsRegion

 

_**上次修改主題的時間：** 2015-03-09_

建立新的集中式記錄組態區域。集中式記錄讓系統管理員可以同時啟用或停用多部電腦上的事件追蹤。集中式記錄區域適合搭配 商務用 Skype Online 使用。

Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsClsRegion -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsClsRegion -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -OtherRegionAccess <String> -SecurityGroupSuffix <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Sites <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立名為 Europe 的新全球區域。新區域會使用安全性群組尾碼 EMEA，也會允許 global/US 區域存取。

    New-CsClsRegion -Identity "global/Europe" -SecurityGroupSuffix "EMEA" -OtherRegionAccess "global/US"

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

在 Office 365 版的 Lync Server 中，區域可用於指定有權存取寫入記錄檔中之個人資訊的使用者。區域會在使用 [New-CsClsRegion](new-csclsregion.md) Cmdlet 建立後，才新增至集中式記錄組態設定的集合。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClsRegion"}

**Lync Server 控制台：** **New-CsClsRegion** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>新區域的唯一識別碼。區域識別包含集中式記錄組態範圍，其中建立區域時會加上唯一區域名稱。例如，若要建立名為 Redmond 的全球區域，請使用下列語法：</p>
<p>-Identity &quot;global/Redmond&quot;</p>
<p>如有使用 Identity 參數，即不可再使用 name 參數或 Parent 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>新區域的唯一名稱。例如：</p>
<p>-Name &quot;Redmond&quot;</p>
<p>如有使用 Name 參數，也必須使用 Parent 參數。但請勿在使用 Name 及 Parent 參數的命令中使用 Identity 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>OtherRegionAccess</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>獲授權存取此區域之使用者所能存取的其他區域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>新區域所在之集中式記錄組態設定的範圍。例如，若要將新區域加入全球設定，請使用下列語法：</p>
<p>-Parent &quot;global&quot;</p>
<p>您可以使用此命令傳回所有集中式記錄「父系」的識別：</p>
<p>Get-CsCentralizedLoggingConfiguration | Select-Object Identity</p>
<p>如有使用 Name 參數，也必須使用 Parent 參數。但請勿在使用 Name 及 Parent 參數的命令中使用 Identity 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>SecurityGroupSuffix</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要加入授權此區域存取之安全性群組的名稱結尾的尾碼。</p></td>
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
<td><p><em>Sites</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>此區域所含的網站。這些網站對應到拓撲文件中的 SideId 屬性值。</p></td>
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

無。New-CsClsRegion Cmdlet 不接受管線傳送的輸入。

## 傳回類型

New-CsClsRegion Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Region\#Decorated 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsClsRegion](get-csclsregion.md)  
[Remove-CsClsRegion](remove-csclsregion.md)  
[Set-CsClsRegion](set-csclsregion.md)

