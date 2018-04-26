---
title: New-CsTrustedApplicationComputer
TOCTitle: New-CsTrustedApplicationComputer
ms:assetid: 5c44a596-7fca-49d3-a7cf-e22656698a28
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398405(v=OCS.15)
ms:contentKeyID: 49291042
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrustedApplicationComputer

 

_**上次修改主題的時間：** 2015-03-09_

將代管信任之應用程式的電腦新增至現有的集區。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsTrustedApplicationComputer -Identity <XdsGlobalRelativeIdentity> -Pool <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會將 FQDN 為 Trust1.litwareinc.com 的新電腦新增至集區 TrustPool.litwareinc.com。我們使用 Identity 參數來指定新電腦的 FQDN，並使用 Pool 參數來指定集區的 FQDN。該集區必須存在，且必須是信任的應用程式集區 (注意：若要建立信任的應用程式集區，請呼叫 **New-CsTrustedApplicationPool** Cmdlet)。

    New-CsTrustedApplicationComputer -Identity Trust1.litwareinc.com -Pool TrustPool.litwareinc.com

## 詳細描述

我們建議您應該將 Lync Server 部署內執行信任的應用程式的電腦，新增至信任的應用程式專用的集區。不過，您也可以將信任的應用程式電腦新增至用於其他用途的現有集區。根據預設，當您建立集區時，也會建立完整網域名稱 (FQDN) 與集區相同的電腦。使用此 Cmdlet 建立新電腦，並將其新增至集區。

信任的應用程式集區必須已經存在，此 Cmdlet 才會成功。此外，如果集區包含 ExternalServer 角色之外的服務角色，您也無法將其他信任的應用程式電腦新增至該集區。例如，如果此集區也支援 Registrar 或 CentralMgmt 角色，則該集區只能包含一部信任的應用程式電腦。此外，如果您在建立集區 (透過呼叫 **New-CsTrustedApplicationPool** Cmdlet) 時未指定預設電腦的 FQDN，則該電腦的 FQDN 會與集區的 FQDN 相同，而您也無法新增另一部電腦。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsTrustedApplicationComputer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrustedApplicationComputer"}

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
<td><p>主控信任應用程式之電腦的 FQDN。</p></td>
</tr>
<tr class="even">
<td><p><em>Pool</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>主控信任應用程式電腦之集區的 FQDN。您可以執行 <strong>Get-CsTrustedApplicationPool</strong> Cmdlet 來尋找可用的集區。</p></td>
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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
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

無。

## 傳回類型

建立 Microsoft.Rtc.Management.Xds.DisplayComputer 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsTrustedApplicationComputer](remove-cstrustedapplicationcomputer.md)  
[Get-CsTrustedApplicationComputer](get-cstrustedapplicationcomputer.md)  
[New-CsTrustedApplicationPool](new-cstrustedapplicationpool.md)  
[Get-CsTrustedApplicationPool](get-cstrustedapplicationpool.md)

