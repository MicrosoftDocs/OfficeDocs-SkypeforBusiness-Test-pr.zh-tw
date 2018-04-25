---
title: Remove-CsPublicProvider
TOCTitle: Remove-CsPublicProvider
ms:assetid: b9eec2f4-cf36-41b7-8023-67790cc8d4cd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412906(v=OCS.15)
ms:contentKeyID: 49292136
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPublicProvider

 

_**上次修改主題的時間：** 2015-03-09_

移除設定供組織使用的公用提供者。公用提供者是可以為大眾提供立即訊息 (IM)、目前狀態及相關服務的組織。Lync Server 的出貨版本中設有 Yahoo、AIM (AOL) 及 Messenger (MSN) 三家公用提供者，但未加以啟用。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsPublicProvider -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會刪除 Identity 為 Messenger 的公用提供者。此命令完成後，設定好的公用提供者清單中不會再出現 Messenger；在這之後，要與 Messenger 重新建立同盟唯一的方法是重新建立此提供者。

    Remove-CsPublicProvider -Identity "Messenger"

## 範例 2

範例 2 會刪除設定供組織使用的所有公用提供者。為達成此目的，此命令會先使用 **Get-CsPublicProvider** Cmdlet，以傳回目前設定使用的所有公用提供者集合。然後，此集合會管線傳送到 **Remove-CsPublicProvider** Cmdlet，以刪除集合中的每一個提供者。

    Get-CsPublicProvider | Remove-CsPublicProvider

## 範例 3

範例 3 會從設定的公用提供者集合中移除所有目前停用的公用提供者。為了執行此工作，命令會先使用 **Get-CsPublicProvider** Cmdlet，以傳回目前設定使用的所有公用提供者集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 Enabled 屬性等於 False 的提供者。接著將該篩選後的集合管線傳送到 **Remove-CsPublicProvider** Cmdlet，以刪除集合中的所有項目。

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Remove-CsPublicProvider

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 2013 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與協力廠商主機供應商之間的同盟。

公用提供者是一家提供 SIP 通訊服務給一般大眾的組織。當您與公用提供者建立同盟關係時，實際上就等於和任何具有該提供者所提供帳戶的使用者建立同盟。例如，如果您與 Messenger (MSN) 結盟，您的使用者便能夠與任何具有 Messenger 立即訊息帳戶的使用者交換立即訊息和目前狀態資訊。

若要與公用提供者結盟，您需要建立及啟用新的公用提供者 (此外，公用提供者也將需要與您建立同盟關係)。如果您之後決定要終止此關係，可以用 **Remove-CsPublicProvider** Cmdlet 刪除此公用提供者。刪除公用提供者時，會從您的同盟協力廠商清單中移除提供者；在這之後，要重新建立關係的唯一方法是重新建立提供者。如果您想要暫停關係，可以改用 **Disable-CsPublicProvider** Cmdlet。停用公用提供者時，不會從同盟協力廠商清單中移除該提供者；而是將該提供者標示為已停用，而您的組織與該提供者之間的通訊也暫停。若要重新建立關係，只要使用 **Enable-CsPublicProvider** Cmdlet 重新啟用該提供者即可。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsPublicProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPublicProvider"}

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
<td><p>要移除的公用提供者的唯一識別碼。Identity 通常是提供服務的網站名稱 (例如，Yahoo!、AOL、MSN 等)。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider 物件。**Remove-CsPublicProvider** Cmdlet 會接受公用提供者物件管線傳送的執行個體。

## 傳回類型

無。反之，此 Cmdlet 會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

