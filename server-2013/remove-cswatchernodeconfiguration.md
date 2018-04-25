---
title: Remove-CsWatcherNodeConfiguration
TOCTitle: Remove-CsWatcherNodeConfiguration
ms:assetid: 599c6d58-da3d-4f0b-bc1f-22ac3e33ec7f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204926(v=OCS.15)
ms:contentKeyID: 49291008
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsWatcherNodeConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的監看員節點組態設定集合。監看員節點是定期使用 System Center Operations Manager 和 Lync Server 2013 綜合交易來驗證 Lync Server 元件是否如預期運作的電腦。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsWatcherNodeConfiguration -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除套用至 atl-cs-001.litwareinc.com 集區的監看員節點組態設定。

    Remove-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com"

## 範例 2

範例 2 會移除設定供組織使用的所有監看員節點。為達成此目的，命令會先使用 **Get-CsWatcherNodeConfiguration** Cmdlet 傳回所有監看員節點的集合。然後，此集合會管線傳送到 **Remove-CsWatcherNodeConfiguration** Cmdlet，以移除集合中的每一個監看員節點。如此將實際上移除組織中的每個監看員節點。

    Get-CsWatcherNodeConfiguration | Remove-CsWatcherNodeConfiguration

## 範例 3

範例 3 會移除所有以 sip:kenmyer@litwareinc.com 使用者為測試使用者的監看員節點。為了執行此工作，命令會先呼叫 **Get-CsWatcherNodeConfiguration** Cmdlet，以傳回目前所使用之所有監看員節點的集合。然後，此集合會管線傳送到 Where-Object Cmdlet，這會只挑出 TestUsers 屬性包含 (-contains) sip:kenmyer@litwareinc.com 使用者的設定。接著將篩選後的集合管線傳送到 **Remove-CsWatcherNodeConfiguration** Cmdlet，以移除經過篩選之集合中的每一個項目。

    Get-CsWatcherNodeConfiguration | Where-Object {$_.TestUsers -contains "sip:kenmyer@litwareinc.com"} | Remove-CsWatcherNodeConfiguration

## 詳細描述

您若是使用 Microsoft System Center Operations Manager 監視 Lync Server 2013，可以選擇是否要設定「監看員節點」(亦即定期自動執行綜合交易，以確認 Lync Server 元件是否如預期運作的電腦)。監看員節點會指派給集區，並使用 **CsWatcherNodeConfiguration** Cmdlet 進行管理。請注意，您若是使用 System Center Operations Manager，則無需安裝監看員節點。您無需使用監看員節點，即可監視您的系統。唯一不同在於必須手動叫用執行綜合交易，而無法由 Operations Manager 自動叫用執行。

之後若您決定要解除委任監看員節點，可以使用 **Remove-CsWatcherNodeConfiguration** Cmdlet。除此之外也可使用 [Set-CsWatcherNodeConfiguration](set-cswatchernodeconfiguration.md) Cmdlet 暫時停用 (並之後重新啟用) 監看員節點。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsWatcherNodeConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Remove-CsWatcherNodeConfiguration** Cmdlet 所執行的功能。

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
<td><p>獲指派要刪除之監看員節點的集區的完整網域名稱。例如：</p>
<p>-Identity &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
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
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Remove-CsWatcherNodeConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TargetPool\#Decorated 物件執行個體。

## 傳回類型

無。反之，Remove-CsWatcherNodeConfiguration Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TargetPool\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsWatcherNodeConfiguration](get-cswatchernodeconfiguration.md)  
[New-CsWatcherNodeConfiguration](new-cswatchernodeconfiguration.md)  
[Set-CsWatcherNodeConfiguration](set-cswatchernodeconfiguration.md)  
[Test-CsWatcherNodeConfiguration](test-cswatchernodeconfiguration.md)

