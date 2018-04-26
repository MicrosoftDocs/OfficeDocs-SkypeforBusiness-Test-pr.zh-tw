---
title: Remove-CsTrustedApplicationPool
TOCTitle: Remove-CsTrustedApplicationPool
ms:assetid: 93aa3381-e3fc-45df-840e-3d6d61a52fb3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398750(v=OCS.15)
ms:contentKeyID: 49291687
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTrustedApplicationPool

 

_**上次修改主題的時間：** 2015-03-09_

移除包含代管信任之應用程式的電腦的集區。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsTrustedApplicationPool -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除其 FQDN 為 TrustPool.litwareinc.com 的集區。我們會使用 Identity 參數指定要移除之集區的 FQDN。由於身分識別是唯一的，因此這個命令最多只會移除一個集區。

    Remove-CsTrustedApplicationPool -Identity TrustPool.litwareinc.com

## 範例 2

此範例會移除所有集區 FQDN 以 “trust” 字串開頭的受信任集區。命令的第一個部分是對 **Get-CsTrustedApplicationPool** Cmdlet 的呼叫，以擷取您 Lync Server 基礎結構中所有受信任應用程式集區的集合。將此集合管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會檢查集合中的每一個項目，查看 PoolFqdn 是否符合萬用字元 trust\* 字串。這會產生由所有其 PoolFqdn 以 trust 字串開頭、後接任何字元的受信任應用程式集區組成的集合。最後，將此集合管線傳送到 **Remove-CsTrustedApplicationPool** Cmdlet，以移除集合中的每一個項目。

    Get-CsTrustedApplicationPool | Where-Object {$_.PoolFqdn -match "trust*"} | Remove-CsTrustedApplicationPool

## 詳細描述

建議您應該將 Lync Server 部署內執行受信任應用程式的電腦，新增至受信任應用程式專用的集區。不過，您也可以將受信任應用程式電腦新增至用於其他用途的現有集區。此 Cmdlet 會移除現有的受信任應用程式集區。但是，您無法移除不具 Registrar 值的受信任應用程式集區。若受信任應用程式集區未被指派登錄器，您必須使用 **Set-CsTrustedApplicationPool** Cmdlet 新增登錄器值，然後移除該集區。

請記住，移除集區時也會移除所有與該集區相關聯的電腦、應用程式及應用程式端點。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsTrustedApplicationPool** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTrustedApplicationPool"}

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
<td><p>您要移除之集區的完整網域名稱 (FQDN) 或服務 ID。</p></td>
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

Microsoft.Rtc.Management.Xds.DisplayExternalServer 物件。接受管線傳送的受信任應用程式集區物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.Xds.DisplayExternalServer 類型的物件。

## 請參閱

#### 其他資源

[New-CsTrustedApplicationPool](new-cstrustedapplicationpool.md)  
[Set-CsTrustedApplicationPool](set-cstrustedapplicationpool.md)  
[Get-CsTrustedApplicationPool](get-cstrustedapplicationpool.md)

