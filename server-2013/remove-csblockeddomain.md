---
title: Remove-CsBlockedDomain
TOCTitle: Remove-CsBlockedDomain
ms:assetid: 34485703-9e1d-47f9-9834-c2ba37249cd1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425832(v=OCS.15)
ms:contentKeyID: 49290542
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsBlockedDomain

 

_**上次修改主題的時間：** 2015-03-09_

從同盟的封鎖網域清單中移除網域。根據定義，您的使用者無法使用Lync Server 應用程式與封鎖網域的人員通訊；例如，使用者無法使用 Lync 與封鎖清單上之網域中使用 SIP 帳戶的人員交換立即訊息。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsBlockedDomain -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 fabrikam.com 網域從封鎖網域清單中移除。作法為呼叫 **Remove-CsBlockedDomain** Cmdlet，並指定 Identity 為 "fabrikam.com" 的網域。

    Remove-CsBlockedDomain -Identity fabrikam.com

## 範例 2

在範例 2 中，所有 Identity 包含字串值 "fabrikam" 的網域皆會自封鎖網域清單中移除。為達成此目的，命令會先使用 **Get-CsBlockedDomain** Cmdlet 搭配 Filter 參數，以傳回 Identity 包含 "fabrikam" 字串 (例如，fabrikam.com、fabrikam.org 或 us.fabrikam.net) 之所有封鎖網域的集合。然後再將集合管線傳送到 **Remove-CsBlockedDomain** Cmdlet，以從封鎖網域清單中刪除集合中的每個項目。

    Get-CsBlockedDomain -Filter *fabrikam* | Remove-CsBlockedDomain 

## 範例 3

範例 3 所示的命令會完全清除封鎖網域清單。作法是先呼叫不含任何參數的 **Get-CsBlockedDomain** Cmdlet，以傳回目前列名於封鎖網域清單中之所有網域的集合。然後，此集合會管線傳送到 **Remove-CsBlockedDomain** Cmdlet，以從封鎖網域清單中移除集合中的每個項目。整體效果：封鎖網域清單上不會留下任何的網域。

    Get-CsBlockedDomain | Remove-CsBlockedDomain 

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與第三方主機供應商之間的同盟。

設定與其他組織的直接同盟需要幾項工作。若要開始，必須啟用執行 Lync Server Access Edge 服務的伺服器以允許同盟。此外，另一個組織必須允許與您同盟；雙方必須皆同意同盟關係，才能建立同盟。

若要建立同盟關係，可能也需要管理兩個與同盟相關的清單：允許清單與封鎖清單。允許清單代表您選擇要建立同盟的組織；如果網域出現在允許清單上 (取決於您的組態設定)，您的使用者便能與在該同盟網域中有帳戶的使用者交換立即訊息與目前狀態資訊。相反地，封鎖清單代表明確禁止使用者進行同盟的網域；例如，Lync Server 會自動拒絕從封鎖網域傳送的訊息。

一旦網域出現在封鎖清單中，訊息必定會遭到拒絕。將網域從清單移除之後，您就可以和該網域建立同盟關係。若要能夠與先前禁止的網域同盟，您必須先使用 **Remove-CsBlockedDomain** Cmdlet 將該網域從封鎖網域清單中移除。一個網域無法同時出現在允許清單和封鎖清單中。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsBlockedDomain** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsBlockedDomain"}

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
<td><p>要從封鎖清單中移除之網域的完整網域名稱 (FQDN)，例如 fabrikam.com。請注意，在指定網域的 Identity 時，無法使用萬用字元。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.BlockedDomain 物件。**Remove-CsBlockedDomain** 接受封鎖網域物件的管線傳送執行個體。

## 傳回類型

刪除 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.BlockedDomain 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsBlockedDomain](get-csblockeddomain.md)  
[New-CsBlockedDomain](new-csblockeddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)  
[Set-CsBlockedDomain](set-csblockeddomain.md)

