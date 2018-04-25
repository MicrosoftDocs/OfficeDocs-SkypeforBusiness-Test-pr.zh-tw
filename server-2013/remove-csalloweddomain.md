---
title: Remove-CsAllowedDomain
TOCTitle: Remove-CsAllowedDomain
ms:assetid: d38afb34-627e-4772-990c-4f6676c54000
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398913(v=OCS.15)
ms:contentKeyID: 49292408
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAllowedDomain

 

_**上次修改主題的時間：** 2015-03-09_

從同盟的核准網域清單中移除網域。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsAllowedDomain -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 fabrikam.com 網域從允許的網域清單移除。

    Remove-CsAllowedDomain -Identity fabrikam.com

## 範例 2

範例 2 會將 Identity 之任何部分含字串值 "fabrikam" 的網域從允許的網域清單移除。為達成此目的，命令會先使用 **Get-CsAllowedDomain** Cmdlet 搭配 Filter 參數，以傳回 Identity (唯一能篩選的屬性) 包含字串值 "fabrikam" 之網域的集合。然後將該篩選後的集合管線傳送到 **Remove-CsAllowedDomain** Cmdlet，以從允許的網域清單中移除篩選後之集合中的所有項目。

    Get-CsAllowedDomain -Filter *fabrikam* | Remove-CsAllowedDomain

## 範例 3

範例 3 會將所有不具有已識別 Proxy 伺服器的網域從允許的網域清單中移除。為了執行此工作，會呼叫 **Get-CsAllowedDomain** Cmdlet，以傳回目前在允許清單中的所有網域集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet；這會只挑出 ProxyFqdn 屬性等於 Null 值的網域。接著將篩選後的集合管線傳送到 **Remove-CsAllowedDomain** Cmdlet，以從允許的清單中移除集合中的每一個網域。

    Get-CsAllowedDomain | Where-Object {$_.ProxyFqdn -eq $Null} | Remove-CsAllowedDomain 

## 範例 4

範例 4 會從允許的網域清單移除所有 Comment 欄位含字串值 "Ken Myer" 的網域。為達成此目的，命令會先使用 **Get-CsAllowedDomain** Cmdlet，以擷取目前列在允許之網域清單中的所有網域集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 Comment 屬性包含字串值 "Ken Myer" 的網域。接著將此篩選後的集合管線傳送到 **Remove-CsAllowedDomain** Cmdlet，以從允許的網域清單中移除集合中的每一個項目。

    Get-CsAllowedDomain | Where-Object {$_.Comment -match "Ken Myer"} | Remove-CsAllowedDomain 

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與第三方主機供應商之間的同盟。

設定與其他組織的直接同盟需要幾項工作。若要開始，必須啟用執行 Lync Server Access Edge 服務的伺服器以允許同盟。此外，另一個組織必須允許與您同盟；雙方必須皆同意同盟關係，才能建立同盟。

若要設定同盟關係，您也可能需要管理兩個同盟相關清單：允許清單與封鎖清單。允許清單代表您選擇要建立同盟的組織。如果網域出現在允許清單上 (視組態設定而定)，則使用者能夠與在該同盟網域中具有帳戶的使用者交換立即訊息和目前狀態資訊。相反地，封鎖清單代表明確禁止使用者進行同盟的網域；例如，Lync Server 會自動拒絕從封鎖網域傳送的訊息。

如果您想要中斷同盟關係，請使用 **Remove-CsAllowedDomain** Cmdlet 從允許的網域清單移除適當網域，然後，如果適當，請使用 **New-CsBlockedDomain** Cmdlet，將該網域新增至封鎖的網域清單。請注意，一個網域無法同時出現在允許清單和封鎖清單上。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsAllowedDomain** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsAllowedDomain"}

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
<td><p>要從允許清單移除之網域的完整網域名稱 (FQDN)；例如 fabrikam.com。您無法在指定網域 Identity 時使用萬用字元。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowedDomain 物件。**Remove-CsAllowedDomain** Cmdlet 接受允許之網域物件管線傳送的執行個體。

## 傳回類型

刪除 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowedDomain 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAllowedDomain](get-csalloweddomain.md)  
[New-CsAllowedDomain](new-csalloweddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)  
[Set-CsAllowedDomain](set-csalloweddomain.md)

