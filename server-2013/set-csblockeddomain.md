---
title: Set-CsBlockedDomain
TOCTitle: Set-CsBlockedDomain
ms:assetid: 03f9443c-4c99-4338-bbf0-7b2f40a30ea5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398090(v=OCS.15)
ms:contentKeyID: 49289932
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsBlockedDomain

 

_**上次修改主題的時間：** 2015-03-09_

修改同盟之封鎖網域清單中之一或多個網域的 Comment 屬性。根據定義，您的使用者無法使用 Lync Server 應用程式與封鎖網域的人員通訊；例如，使用者無法使用 Lync 與封鎖清單上之網域中使用 SIP 帳戶的人員交換立即訊息。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsBlockedDomain [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsBlockedDomain [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Comment <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改 Identity 為 "fabrikam.com" 之封鎖網域的 Comment。在此範例中，Comment 參數會與參數值 "Block this domain pending legal review" 一起加入。

    Set-CsBlockedDomain -Identity fabrikam.com -Comment "Block this domain pending legal review."

## 範例 2

範例 2 會更新封鎖網域清單中包含之所有網域的 Comment 屬性。為達成此目的，命令會先呼叫 **Get-CsBlockedDomain** Cmdlet 傳回目前在封鎖網域清單上所有網域的集合。然後，此集合會管線傳送到 **Set-CsBlockedDomain** Cmdlet，這會繼續修改集合中每個網域的 Comment 屬性。

    Get-CsBlockedDomain | Set-CsBlockedDomain -Comment "Block this domain pending legal review."

## 範例 3

範例 3 會為封鎖清單中還沒有設定 Comment 屬性值的每個網域新增一個註解 ("Block this domain pending legal review.")。為了執行此工作，命令會先使用 **Get-CsBlockedDomain** Cmdlet 傳回目前在封鎖清單上所有網域的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Comment 屬性等於 Null 值的網域。接著將篩選後的集合管線傳送到 **Set-CsBlockedDomain** Cmdlet，以將相同的註解指派給此篩選過的集合中每個網域的 Comment 屬性。

    Get-CsBlockedDomain | Where-Object {$_.Comment -eq $Null} | Set-CsBlockedDomain -Comment "Block this domain pending legal review."

## 詳細描述

「同盟」是兩個組織可建立信任關係的一種方法，此信任關係會簡化兩個團體之間的通訊。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync Server 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您的組織與其他組織之間的直接同盟；2) 您的組織與公用提供者之間的同盟；以及 3) 您的組織與第三方主機供應商之間的同盟。

設定與其他組織間的直接同盟包含幾個工作。首先，您必須啟用 Access Edge Server 以允許同盟。此外，另一個組織必須允許與您同盟；除非雙方都同意該關係，否則無法建立同盟。

若要設定同盟關係，您也可能需要管理兩個同盟相關清單：允許清單和封鎖清單。允許清單表示您已選擇與其同盟的組織；如果某個網域顯示在允許清單中，則 (根據您的組態設定而定) 您的使用者就可以與在該同盟網域中具有帳戶的使用者交換立即訊息及目前狀態資訊。相反地，封鎖清單代表明確禁止使用者進行同盟的網域；例如，Lync Server 會自動拒絕從封鎖網域傳送的訊息。

Comment 內容 (封鎖網域中唯一可修改的內容) 用來儲存封鎖清單上的網域其他資訊 (例如，為何封鎖網域、何時可從封鎖清單中移除網域，或當您想要從封鎖清單中移除網域時應該連絡何人)。如果需要變更封鎖網域清單上任何網域的 Comment 屬性，請使用 **Set-CsBlockedDomain** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsBlockedDomain** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsBlockedDomain"}

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
<td><p><em>Comment</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您提供要修改之網域的其他資訊。例如，您可能會新增 Comment，其中指出網域放置在封鎖清單中的原因。</p></td>
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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改 Comment 內容之封鎖清單的完整網域名稱 (FQDN)。例如：fabrikam.com</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>BlockedDomain 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.BlockedDomain 物件。**Set-CsBlockedDomain** Cmdlet 接受管線傳送的封鎖網域物件執行個體。

## 傳回類型

**Set-CsBlockedDomain** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.BlockedDomain 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsBlockedDomain](get-csblockeddomain.md)  
[New-CsBlockedDomain](new-csblockeddomain.md)  
[Remove-CsBlockedDomain](remove-csblockeddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

