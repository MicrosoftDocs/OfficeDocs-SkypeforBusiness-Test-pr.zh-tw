---
title: New-CsWatcherNodeConfiguration
TOCTitle: New-CsWatcherNodeConfiguration
ms:assetid: c7f78c92-7965-4879-9efa-1b5adcd1881b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205254(v=OCS.15)
ms:contentKeyID: 49292275
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsWatcherNodeConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

將新的監看員節點組態設定集合指派給集區。監看員節點是定期使用 Microsoft System Center Operations Manager 及 Lync Server 2013 綜合交易，以驗證 Lync Server 元件是否如預期運作的電腦。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsWatcherNodeConfiguration -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    New-CsWatcherNodeConfiguration -TargetFqdn <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -PortNumber <UInt16> [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-ExtendedTests <PSListModifier>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Tests <PSListModifier>] [-TestUsers <PSListModifier>] [-UseInternalWebUrls <$true | $false>] [-WhatIf [<SwitchParameter>]] [-XmppTestReceiverMailAddress <String>]

## 範例

## 範例 1

範例 1 所示的命令會建立集區 atl-cs-001.litwareinc.com 之監看員節點組態設定的新集合。為達此目的，範例中的前兩個命令會建立一對監看員節點測試使用者 (sip:kenmyer@litwareinc.com 和 sip:pilar@litwareinc.com)。建立測試使用者之後，範例中的第三個命令會使用新建立的使用者建立新的擴充 PSTN 測試。此新測試 (此時只存在於記憶體中) 會儲存於名為 $x 的變數中。

最後，範例中的第四個命令會建立 atl-cs-001.litwareinc.com 的監看員節點組態設定。這些新設定使用連接埠 5061、兩位新測試使用者及儲存於變數 $x 中的延伸測試。

    Set-CsTestUserCredential -SipAddress "sip:kenmyer@litwareinc.com" -UserName "litwareinc\kenmyer" -Password "07Apples"
    
    Set-CsTestUserCredential -SipAddress "sip:pilar@litwareinc.com" -UserName "litwareinc\pilar" -Password "07Apples"
    
    $x = New-CsExtendedTest -TestUsers "sip:kenmyer@litwareinc.com", "sip:pilar@litwareinc.com" -Name "PSTN Test" -TestType "PSTN"
    
    New-CsWatcherNodeConfiguration -TargetFqdn "atl-cs-001.litwareinc.com" -PortNumber 5061 -TestUsers "sip:kenmyer@litwareinc.com","sip:pilar@litwareinc.com"} -ExtendedTests @{Add=$x}

## 詳細描述

您若是使用 Microsoft System Center Operations Manager 監視 Lync Server 2013，則可選擇是否要設定「監看員節點」(亦即定期自動執行綜合交易，以驗證 Lync Server 元件是否如預期運作的電腦)。監看員節點會指派給集區，且會使用 **CsWatcherNodeConfiguration** Cmdlet 來管理。請注意，您若是使用 System Center Operations Manager，即無須安裝監看員節點。您無須使用監看員節點，即可監視您的系統。唯一的差異在於必須手動叫用任何要執行的綜合交易，而無法由 Operations Manager 自動叫用。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsWatcherNodeConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **New-CsWatcherNodeConfiguration** Cmdlet 所執行的功能。

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
<td><p>要與監看員節點組態設定相關聯的完整網域名稱。您可以使用 Identity 參數或 TargetFqdn 參數指定集區，但是無法在相同命令中使用這些參數。</p></td>
</tr>
<tr class="even">
<td><p><em>PortNumber</em></p></td>
<td><p>必要</p></td>
<td><p>System.UInt16</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要與監看員節點組態設定相關聯的完整網域名稱。您可以使用 TargetFqdn 參數或 Identity 參數指定集區，但是無法在相同命令中使用這些參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>啟用或停用監看員節點。預設值為 True ($True)。</p></td>
</tr>
<tr class="even">
<td><p><em>ExtendedTests</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>可指派給監看員節點組態的 PSTN 或音訊會議提供者測試。這些測試必須使用 <strong>New-CsExtendedTest</strong> Cmdlet 來建立，並儲存於變數中 (例如 $x)。然後使用類似下列的語法，將測試指派給監看員節點：</p>
<p>–ExtendedTests @{Add=$x}</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tests</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>監看員節點要執行的綜合交易。允許的值為：</p>
<p>* Registration</p>
<p>* IM</p>
<p>* GroupIM</p>
<p>* P2PAV</p>
<p>* AvConference</p>
<p>* Presence</p>
<p>* ABS</p>
<p>* ABWQ</p>
<p>* MCXP2PIM</p>
<p>* ExumConnectivity</p>
<p>* JoinLauncher</p>
<p>* PersistentChatMessage</p>
<p>* DataConference</p>
<p>* XmppIM</p>
<p>* UnifiedContactStore</p>
<p>* AVEdgeConnectivity</p>
<p>若要在建立新的監看員節點時設定測試，請使用下列語法，並使用逗號分隔每個測試：</p>
<p>-Tests &quot;ABS&quot;,&quot;ABWQ&quot;,&quot;IM&quot;,&quot;GroupIM&quot;,&quot;XmppIM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>TestUsers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>要指派給監看員節點之測試使用者的 SIP 位址；之前必須先使用 <strong>Set-CsTestUserCredential</strong> Cmdlet 來設定這些使用者帳戶。若要新增測試使用者，請使用類似下列的語法，並使用逗號來分隔使用者位址：</p>
<p>–TestUsers &quot;sip:kenmyer@litwareinc.com&quot;,&quot;sip:pilar@litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>UseInternalWebUrls</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True ($True) 時，會指示監看員節點使用內部的 Web URL，而不使用外部 Web URL。此方法可驗證位於組織防火牆後方之使用者的 URL 有效性。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
<tr class="odd">
<td><p><em>XmppTestReceiverMailAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>測試 XMPP 閘道時所使用的電子郵件地址。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsWatcherNodeConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsWatcherNodeConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TargetPool\#Decorated 物件的新執行個體。

