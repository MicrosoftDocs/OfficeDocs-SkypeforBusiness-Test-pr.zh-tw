---
title: Remove-CsTrustedApplicationComputer
TOCTitle: Remove-CsTrustedApplicationComputer
ms:assetid: c9c0604b-a94e-42b9-9db3-bc3dbe686e41
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398838(v=OCS.15)
ms:contentKeyID: 49292313
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTrustedApplicationComputer

 

_**上次修改主題的時間：** 2015-03-09_

移除信任的應用程式電腦。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsTrustedApplicationComputer -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除 FQDN 為 Trust1.litwareinc.com 的電腦。

    Remove-CsTrustedApplicationComputer -Identity Trust1.litwareinc.com

## 範例 2

此範例會移除所有 FQDN 開頭為 Trust 字串的受信任電腦。此範例會先呼叫 **Get-CsTrustedApplicationComputer** Cmdlet，並將 Trust\* 值傳遞給 Filter 參數。如此可擷取所有 FQDN 開頭為 Trust 且結尾為任意字元集的受信任應用程式電腦。然後將該電腦集合傳送到 **Remove-CsTrustedApplicationComputer** Cmdlet，由其移除集合中的每個項目 (每部電腦)。請記住，如果移除集區中的電腦會使集區成為空白的集區，此命令將不會移除這些電腦。

    Get-CsTrustedApplicationComputer -Filter Trust* | Remove-CsTrustedApplicationComputer

## 詳細描述

建議您應該將 Lync Server 部署內執行信任的應用程式的電腦，新增至信任的應用程式專用的集區。不過，您也可以將信任的應用程式電腦新增至用於其他用途的現有集區。使用此 Cmdlet 移除受信任的應用程式電腦。

使用此 Cmdlet 移除信任的應用程式電腦時，系統不僅會將該電腦從信任的應用程式電腦清單中移除，也會從 Lync Server 的可用電腦清單中移除。換句話說，如果您呼叫 **Get-CsTrustedApplicationComputer** Cmdlet 或 **Get-CsComputer** Cmdlet，電腦將不再出現於清單中。如果信任的應用程式電腦是集區中唯一的電腦，您便無法移除該電腦。如果您想要移除集區中唯一的電腦，必須移除整個集區 (作法是呼叫 **Remove-CsTrustedApplicationPool** Cmdlet)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsTrustedApplicationComputer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTrustedApplicationComputer"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要移除之電腦的完整網域名稱 (FQDN)。</p></td>
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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
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

Microsoft.Rtc.Management.Xds.DisplayComputer 物件。接受信任之應用程式電腦物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.Xds.DisplayComputer 類型的物件。

## 請參閱

#### 其他資源

[New-CsTrustedApplicationComputer](new-cstrustedapplicationcomputer.md)  
[Get-CsTrustedApplicationComputer](get-cstrustedapplicationcomputer.md)  
[Remove-CsTrustedApplicationPool](remove-cstrustedapplicationpool.md)  
[Get-CsTrustedApplicationPool](get-cstrustedapplicationpool.md)

