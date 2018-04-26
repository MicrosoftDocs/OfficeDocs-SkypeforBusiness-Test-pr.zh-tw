---
title: New-CsExtendedTest
TOCTitle: New-CsExtendedTest
ms:assetid: d4756daa-a4ce-4d74-926b-89754cf7e0b2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205275(v=OCS.15)
ms:contentKeyID: 49292440
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsExtendedTest

 

_**上次修改主題的時間：** 2015-03-09_

建立稍後可以指派給監看員節點組態的 PSTN 或音訊會議提供者測試。監看員節點是定期使用 Microsoft System Center Operations Manager 及 Lync Server 2013 綜合交易，以驗證 Lync Server 元件如預期運作的電腦。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsExtendedTest -Name <String> -TestType <AudioConferencingProvider | PSTN> [-TestUsers <PSListModifier>]

## 範例

## 範例 1

範例 1 所示的命令會建立新的延伸測試 (TestType 為 PSTN)，然後將此延伸測試新增至集區 atl-cs-001.litwareinc.com 的新監看員節點。範例中的第一個命令會使用 **New-CsExtendedTest** Cmdlet，來建立名為 PSTN Test 的延伸測試；此測試包含測試使用者 sip:kenmyer@litwareinc.com 和 sip:pilar@litwareinc.com (請注意，您必須先使用 **Set-CsTestUserCredential** Cmdlet，來設定這兩位測試使用者)。然後將產生的延伸測試物件儲存於名為 $cred1 的變數中。

第二個命令會將延伸測試新增到針對 atl-cs-001.litwareinc.com 所建立的新監看員節點。作法是使用 ExtendedTests 參數和語法 @{Add=$x}。

    $x = New-CsExtendedTest -TestUsers "sip:kenmyer@litwareinc.com", "sip:pilar@litwareinc.com" -Name "PSTN Test" -TestType "PSTN"
    
    New-CsWatcherNodeConfiguration -TargetFqdn "atl-cs-001.litwareinc.com" -PortNumber 5061 -TestUsers "sip:kenmyer@litwareinc.com","sip:pilar@litwareinc.com" -ExtendedTests @{Add=$x}

## 詳細描述

您若是使用 Microsoft System Center Operations Manager 監視 Lync Server 2013，可以選擇是否要選定「監看員節點」(亦即定期自動執行綜合交易，以驗證 Lync Server 元件是否如預期運作的電腦)。監看員節點會指派給集，並須透過 CsWatcherNodeConfiguration Cmdlet 進行管理。請注意，您若是使用 System Center Operations Manager，即無須安裝監看員節點。您無須使用監看員節點，即可監視您的系統。唯一不同在於必須手動叫用執行綜合交易，而無法由 Operations Manager 自動叫用執行。

當您設定監看員節點時，可以選擇新增 PSTN 或音訊會議提供者測試以做為「延伸測試」。這些延伸測試可以用來取代監看員節點電腦所執行的標準測試集，或是標準測試集以外的測試。延伸測試必須使用 **New-CsExtendedTest** Cmdlet 來建立，然後新增適當的監看員節點。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsExtendedTest"}

**Lync Server 控制台：**Lync Server 控制台不提供 **New-CsExtendedTest** Cmdlet 所執行的功能。

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
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>指定給延伸測試的易記名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>TestType</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TestType</p></td>
<td><p>延伸測試所執行的測試類型。允許的值為：</p>
<p>* PSTN</p>
<p>* AudioConferencingProvider</p>
<p>每個延伸測試只能指定一種 TestType。</p></td>
</tr>
<tr class="odd">
<td><p><em>TestUsers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>要擔任測試使用者之使用者帳戶的 SIP 位址。您可以使用逗號分隔帳戶來指定多個帳戶，例如：</p>
<p>–TestUsers &quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;</p>
<p>使用 PSTN TestType 時，至少必須指定兩位測試使用者。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsExtendedTest** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsExtendedTest** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.ExtendedTest 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsWatcherNodeConfiguration](new-cswatchernodeconfiguration.md)  
[Set-CsWatcherNodeConfiguration](set-cswatchernodeconfiguration.md)

