---
title: Set-CsClsRegion
TOCTitle: Set-CsClsRegion
ms:assetid: 2599cae9-edef-408f-8987-313c67bfe763
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204746(v=OCS.15)
ms:contentKeyID: 49290368
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClsRegion

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的集中式記錄組態區域。集中式記錄讓系統管理員可以同時啟用或停用多部電腦上事件追蹤。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsClsRegion [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClsRegion [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-OtherRegionAccess <String>] [-SecurityGroupSuffix <String>] [-Sites <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 global/US 區域的安全性群組尾碼變更為 USSupport。

    Set-CsClsRegion -Identity "global/US" -SecurityGroupSuffix "USSupport"

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

透過 商務用 Skype Online，區域可用於指定有權存取寫入記檔中之個人資訊的使用者。區域會在使用 [New-CsClsRegion](new-csclsregion.md) Cmdlet 建立後，才新增至集中式記錄組態設定的集合。 您可以在區域建立之後，使用 **Set-CsClsRegion** Cmdlet 修改其屬性值。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClsRegion"}

**Lync Server 控制台：** **Set-CsClsRegion** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>區域的唯一識別碼。區域的 Identity 由建立區域所在的集中式記錄組態範圍加上唯一的區域名稱所組成。例如，若要參照全域區域 Redmond，請使用下列語法：</p>
<p>-Identity &quot;global/Redmond&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您傳遞物件參考，而不設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>OtherRegionAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>獲授權存取此區域之使用者所能存取的其他區域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>SecurityGroupSuffix</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要加入授權此區域存取之安全性群組的名稱結尾的尾碼。</p></td>
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

**Set-CsClsRegion** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Region\#Decorated 物件執行個體。

## 傳回類型

無。反之，**Set-CsClsRegion** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Region\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsClsRegion](get-csclsregion.md)  
[New-CsClsRegion](new-csclsregion.md)  
[Remove-CsClsRegion](remove-csclsregion.md)

