---
title: Disable-CsPublicProvider
TOCTitle: Disable-CsPublicProvider
ms:assetid: df1338ea-fe6d-45da-a39c-86108bb54ef5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398984(v=OCS.15)
ms:contentKeyID: 49292549
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsPublicProvider

 

_**上次修改主題的時間：** 2015-03-09_

停用設定供組織使用的公用提供者。公用提供者是可以為大眾提供立即訊息、目前狀態及相關服務的組織。Lync Server 的出貨版本中設有 Yahoo、AIM (AOL) 及 Messenger (MSN) 三家公用提供者，但未加以啟用。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Disable-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Disable-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會停用 Identity 為 Messenger 的公用提供者。若已停用 MSN，則這個命令會傳回錯誤訊息。

    Disable-CsPublicProvider -Identity "Messenger"

## 範例 2

範例 2 會停用目前已啟用的所有公用提供者。為達成此目的，命令會先使用 **Get-CsPublicProvider** Cmdlet，以傳回組織目前使用之所有公用提供者的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Enabled 屬性等於 True 的提供者。接著將此篩選後的集合管線傳送到 **Disable-CsPublicProvider** Cmdlet，以停用集合中的每一位提供者。

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $True} | Disable-CsPublicProvider

## 範例 3

範例 3 所示的命令會停用目前已啟用且其驗證層級設為 AlwaysVerifiable 的所有公用提供者。為了完成此工作，命令會先呼叫 **Get-CsPublicProvider** Cmdlet，以傳回組織目前使用之所有公用提供者的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以選取符合下列兩項準則的提供者：1) VerificationLevel 屬性等於 AlwaysVerifiable；且，2) Enabled 屬性等於 True (-and 運算子會指示 **Where-Object** Cmdlet，只有當物件符合所有指定的準則時，才要選取物件)。接著將篩選後的集合管線傳送到 **Disable-CsPublicProvider** Cmdlet，以停用該集合中的每一位提供者。

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable" -and $_.Enabled -eq $True} | Disable-CsPublicProvider

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 2013 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與協力廠商主機服務提供者之間的同盟。

公用提供者是一家提供工作階段初始通訊協定 (SIP) 通訊服務給一般大眾的組織。當您與公用提供者建立同盟關係時，實際上就等於和任何具有該提供者所提供帳戶的使用者建立同盟。例如，如果您與 Messenger (MSN) 結盟，您的使用者便能夠與任何具有 Messenger 立即訊息帳戶的使用者交換立即訊息和目前狀態資訊。

若要與公用提供者結盟，您需要建立及啟用新的公用提供者 (此外，公用提供者也將需要與您建立同盟關係)。當您建立公用提供者時，您可以選擇啟用或停用該同盟關係。如果啟用了公用提供者，則您組織中的使用者將可與具有公用提供者帳戶的人員交換立即訊息與目前狀態資訊。如果停用公用提供者，則將會暫停您與具有公用提供者帳戶之人員通訊的能力，且直至重新啟用該提供者之前將會持續暫停。如果您需要暫時暫停提供者的關係，您可使用 **Disable-CsPublicProvider** Cmdlet 來達成。如果您想將該提供者一併刪除，請使用 **Remove-CsPublicProvider** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Disable-CsPublicProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Disable-CsPublicProvider"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要停用之公用提供者的唯一識別碼。Identity 通常是提供服務的網站名稱 (例如，Yahoo!、AOL、MSN 等)。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DisplayPublicProvider 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider 物件。**Disable-CsPublicProvider** Cmdlet 接受公用提供者物件的管線執行個體。

## 傳回類型

無。而 Cmdlet 會停用 Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

