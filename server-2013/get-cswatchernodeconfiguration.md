---
title: Get-CsWatcherNodeConfiguration
TOCTitle: Get-CsWatcherNodeConfiguration
ms:assetid: 20dae017-375c-4361-8d65-b56f4c09b375
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204739(v=OCS.15)
ms:contentKeyID: 49290313
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsWatcherNodeConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回有關組織使用之監看員節點組態設定的資訊。監看員節點是定期使用 Microsoft System Center Operations Manager 及 Lync Server 2013 綜合交易，以驗證 Lync Server 元件是否如預期運作的電腦。監看員節點組態設定可讓您知道監看員節點所關聯的集區。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsWatcherNodeConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsWatcherNodeConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回目前設定供組織使用之所有監看員節點的資訊。

    Get-CsWatcherNodeConfiguration

## 範例 2

範例 2 會傳回集區相關聯之監看員節點的資訊。

    Get-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com"

## 範例 3

範例 3 所示的命令會傳回測試使用者用來包含 SIP 位址為 sip:kenmyer@litwareinc.com 之使用者的所有監看員節點相關資訊。為達成此目的，命令會先使用 **Get-CsWatcherNodeConfiguration** Cmdlet 傳回組織中所有監看員節點的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 TestUsers 屬性中包含 SIP 位址 sip:kenmyer@litwareinc.com 的那些節點。

    Get-CsWatcherNodeConfiguration | Where-Object {$_.TestUsers -contains "sip:kenmyer@litwareinc.com"}

## 範例 4

範例 4 會傳回所有包含 PSTN 測試類型之監看員節點的資訊。為了執行此工作，命令會先呼叫 **Get-CsWatcherNodeConfiguration** Cmdlet 傳回組織中所有監看員節點的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 ExtendedTests 屬性中包含 (-matches) "TestType=PSTN" 字串值的監看員節點。

    Get-CsWatcherNodeConfiguration | Where-Object {$_.ExtendedTests -match "TestType=PSTN"}

## 詳細描述

您若是使用 Microsoft System Center Operations Manager 監視 Lync Server 2013，可以選擇是否要設定「監看員節點」(亦即定期自動執行綜合交易，以驗證 Lync Server 元件是否如預期運作的電腦)。監看員節點會受指派給集區，並須透過 **CsWatcherNodeConfiguration** Cmdlet 進行管理。請注意，您若是使用 System Center Operations Manager，則無須安裝監看員節點。無須使用監看員節點，即可監視您的系統。唯一不同在於必須手動叫用要執行的綜合交易，而無法由 Operations Manager 自動叫用執行。

**Get-CsWatcherNodeConfiguration** Cmdlet 會傳回設定供組織使用之所有監看員節點的資訊。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsWatcherNodeConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsWatcherNodeConfiguration** Cmdlet 所執行的功能。

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您使用萬用字元傳回一或多個監看員節點。例如，若要傳回 litwareinc.com 網域的所有監看員節點，請使用下列語法：</p>
<p>-Filter &quot;*.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>已被指派監看員節點之集區的完整網域名稱。例如：</p>
<p>-Identity &quot;atl-cs-001.litwareinc.com&quot;</p>
<p>若未指定此參數，<strong>Get-CsWatcherNodeConfiguration</strong> Cmdlet 將會傳回設定供組織使用之所有監看員節點的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取監看員節點組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsWatcherNodeConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsWatcherNodeConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TargetPool\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsWatcherNodeConfiguration](new-cswatchernodeconfiguration.md)  
[Remove-CsWatcherNodeConfiguration](remove-cswatchernodeconfiguration.md)  
[Set-CsWatcherNodeConfiguration](set-cswatchernodeconfiguration.md)  
[Test-CsWatcherNodeConfiguration](test-cswatchernodeconfiguration.md)

