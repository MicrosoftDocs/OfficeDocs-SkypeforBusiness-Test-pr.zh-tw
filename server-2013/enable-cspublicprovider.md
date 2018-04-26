---
title: Enable-CsPublicProvider
TOCTitle: Enable-CsPublicProvider
ms:assetid: 98370dfd-9a53-41a8-a1f3-bb7a516c3c5e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398780(v=OCS.15)
ms:contentKeyID: 49291740
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsPublicProvider

 

_**上次修改主題的時間：** 2015-03-09_

啟用設定供組織使用的公用提供者。公用提供者是可以為大眾提供立即訊息、目前狀態及相關服務的組織。Lync Server 的出貨版本中設有 Yahoo、AIM (AOL) 及 Messenger (MSN) 三家公用提供者，但未加以啟用。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Enable-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Enable-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會啟用 Identity 為 Messenger 的公用提供者。若 Messenger 已啟用，此命令將傳回錯誤。

    Enable-CsPublicProvider -Identity "Messenger"

## 範例 2

範例 2 會啟用所有目前停用的公用提供者。為了執行此工作，命令會先使用 **Get-CsPublicProvider** Cmdlet 傳回設定供組織使用之所有公用提供者的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 Enabled 屬性等於 False 的提供者。接著將篩選後的集合管線傳送到 **Enable-CsPublicProvider** Cmdlet，以啟用集合中的每個提供者。

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Enable-CsPublicProvider

## 範例 3

範例 3 會啟用所有目前尚未啟用的公用提供者，只要這些提供者的驗證層級已設定為 AlwaysVerifiable。為達成此目的，此命令會先呼叫 **Get-CsPublicProvider** Cmdlet，以傳回組織目前所使用之所有公用提供者的集合。然後再將此集合管線傳送至 **Where-Object** Cmdlet，這會挑出同時符合以下兩個準則的提供者：1) VerificationLevel 屬性等於 AlwaysVerifiable；且 2) Enabled 屬性等於 False。(-and 運算子會指示 **Where-Object** Cmdlet 只選取符合所有指定準則的物件)。接著將篩選後的集合管線傳送至 **Enable-CsPublicProvider** Cmdlet，以啟用集合中的每個提供者。

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -eq "AlwaysVerifiable" -and $_.Enabled -eq $False} | Enable-CsPublicProvider

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 2013 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與第三方主機供應商之間的同盟。

公用提供者是為大眾提供 SIP 通訊服務的組織。當您與公用提供者建立同盟關係時，實際上是與擁有該提供者所提供帳戶的所有使用者建立同盟。例如，如果您與 Messenger (MSN) 結盟，您的使用者便能夠與任何具有 MSN Messenger 立即訊息帳戶的使用者交換立即訊息和目前狀態資訊。

若要與公用提供者結盟，您需要建立及啟用新的公用提供者 (此外，公用提供者也將需要與您建立同盟關係)。您可以在建立公用提供者時就啟用它們，也可以在建立它們之後，使用 **Enable-CsPublicProvider** Cmdlet 啟用它們。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Enable-CsPublicProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Enable-CsPublicProvider"}

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
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要啟用之公用提供者的唯一識別碼。Identity 通常是提供服務的網站名稱 (例如，Yahoo!、AOL 和 MSN)。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider 物件。**Enable-CsPublicProvider** Cmdlet 接受管線傳送的公用提供者物件執行個體。

## 傳回類型

無。反之，此 Cmdlet 會啟用 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

