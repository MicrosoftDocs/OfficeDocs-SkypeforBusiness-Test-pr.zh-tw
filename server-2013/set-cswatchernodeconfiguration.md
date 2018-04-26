---
title: Set-CsWatcherNodeConfiguration
TOCTitle: Set-CsWatcherNodeConfiguration
ms:assetid: 001b49ab-de17-4161-9d0c-9d5d9626558f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204620(v=OCS.15)
ms:contentKeyID: 49289887
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsWatcherNodeConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有之監看員節點組態設定的集合。監看員節點是定期使用 Microsoft System Center Operations Manager 2007 R2 及 Lync Server 2013 綜合交易，以驗證 Lync Server 元件是否如預期運作的電腦。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsWatcherNodeConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsWatcherNodeConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-ExtendedTests <PSListModifier>] [-Force <SwitchParameter>] [-PortNumber <UInt16>] [-Tests <PSListModifier>] [-TestUsers <PSListModifier>] [-UseInternalWebUrls <$true | $false>] [-WhatIf [<SwitchParameter>]] [-XmppTestReceiverMailAddress <String>]

## 範例

## 範例 1

範例 1 所示的命令會在套用到 atl-cs-001.litwareinc.com 集區的監看員節點組態設定中，新增音訊會議提供者測試。為達成此目的，範例中的第一個命令會使用 **New-CsExtendedTest** Cmdlet 建立新測試；此測試只會在記憶體中執行，並儲存在 $x 變數中。在第二個命令中， **Set-CsWatcherNodeConfiguration** Cmdlet 會將測試新增到監看員節點組態設定；作法是使用 ExtendedTests 參數及 @{Add=$x} 語法。

    $x = New-CsExtendedTest -TestUsers "sip:kenmyer@litwareinc.com", "sip:pilar@litwareinc.com" -Name "Audio Conferencing Test" -TestType "AudioConferencingProvider"
    
    Set-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" -ExtendedTests @{Add=$x}

## 範例 2

範例 2 的命令說明如何從監看員節點組態設定集合中移除延伸測試。為了執行此工作，範例中的第一個命令會使用 **Get-CsWatcherNodeConfiguration** Cmdlet，將物件參照回傳給 atl-cs-001.litwareinc.com 集區的監看員節點設定；此物件參照會儲存在名為 $x 的變數中。

第二個命令會使用 RemoveAt() 方法移除 $x 物件參照中的第一個延伸測試。延伸測試會儲存為陣列中的項目；第一個項目的索引號碼為 0，第二個項目的索引號碼為 1，依此類推。RemoveAt(0) 語法會移除索引號碼為 0 的項目，亦即延伸測試集中的第一個項目。若要移除第二個延伸測試，請使用 RemoveAt(1) 語法。

物件參照更新之後，最後一個命令會使用 **Set-CsWatcherNodeConfiguration** Cmdlet 及 Instance 參數，將對物件參照的變更寫回 atl-cs-001.litwareinc.com 集區的實際監看員節點設定。

    $x = Get-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com"
    
    $x.ExtendedTests.RemoveAt(0)
    
    Set-CsWatcherNodeConfiguration -Instance $x

## 範例 3

範例 3 會移除針對 atl-cs-001.litwareinc.com 監看員節點所設定的全部延伸測試。此作業在執行時會加入 ExtendedTests 參數及 $Null 參數值。

    Set-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" -ExtendedTests $Null

## 詳細描述

您若是使用 Microsoft System Center Operations Manager 監視 Lync Server 2013，則可選擇是否要設定「監看員節點」(亦即定期自動執行綜合交易，以驗證 Lync Server 元件是否如預期運作的電腦)。監看員節點會指派給集區，且會使用 **CsWatcherNodeConfiguration** Cmdlet 來管理。請注意，您若是使用 System Center Operations Manager，即無須安裝監看員節點。您無須使用監看員節點，即可監視您的系統。唯一的差異在於必須手動叫用任何要執行的綜合交易，而無法由 Operations Manager 自動叫用。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsWatcherNodeConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Set-CsWatcherNodeConfiguration** Cmdlet 所執行的功能。

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
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>啟用或停用監看員節點。預設值為 True ($True)。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExtendedTests</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>對一或多個 ExtendedTest 物件執行個體的物件參照。這些物件必須使用 <strong>New-CsExtendedTest</strong> Cmdlet 建立。</p></td>
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
<td><p>監看員節點組態設定所關聯之集區的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>PortNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。</p></td>
</tr>
<tr class="even">
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
<p>若要啟用其他的監看員節點測試，請使用類似下列的語法：</p>
<p>-Tests @{Add=&quot;ExumConnectivity&quot;,&quot;JoinLauncher&quot;,&quot;UnifiedContactStore&quot;}</p>
<p>若要停用一或多個監看員節點測試，請使用類似下列的語法：</p>
<p>-Tests @{Remove=&quot;ABS&quot;,&quot;ABWQ&quot;}</p>
<p>若要停用所有監看員節點測試，請將 Tests 參數值設為 $Null：</p>
<p>-Tests $Null</p></td>
</tr>
<tr class="odd">
<td><p><em>TestUsers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>監看員節點所用之測試使用者的 SIP 位址。若要將其他測試使用者加入節點，請使用類似下列的語法：</p>
<p>-TestUsers @{Add=&quot;sip:aidan@litwareinc.com&quot;}</p>
<p>若要將測試使用者從監看員節點移除，請使用類似下列的語法：</p>
<p>-TestUsers @{Remove=&quot;sip:aidan@litwareinc.com&quot;</p>
<p>若以新使用者取代現有的使用者，請使用 Replace 方法。例如，下列語法會以新使用者 sip:aidan@litwareinc.com 取代使用者 sip:pilar@litwareinc.com：</p>
<p>-TestUsers @{Replace=&quot;sip:pilar@litwareinc.com&quot;,&quot;sip:aidan@litwareinc.com&quot;}</p>
<p>每個監看員節點至少須有兩位測試使用者。若只有兩位使用者，又嘗試移除其中一位使用者 (明顯造成節點只剩下一位測試使用者)，您的命令將會失敗。</p></td>
</tr>
<tr class="even">
<td><p><em>UseInternalWebUrls</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True ($True) 時，會指示監看員節點使用內部的 Web URL，而不使用外部 Web URL。此方法可驗證位於組織防火牆後方之使用者的 URL 有效性。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
<tr class="even">
<td><p><em>XmppTestReceiverMailAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>測試 XMPP 閘道時所使用的電子郵件地址。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Set-CsWatcherNodeConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TargetPool\#Decorated 物件執行個體。

## 傳回類型

無。反之， **Set-CsWatcherNodeConfiguration** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TargetPool\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsWatcherNodeConfiguration](get-cswatchernodeconfiguration.md)  
[New-CsWatcherNodeConfiguration](new-cswatchernodeconfiguration.md)  
[Remove-CsWatcherNodeConfiguration](remove-cswatchernodeconfiguration.md)  
[Test-CsWatcherNodeConfiguration](test-cswatchernodeconfiguration.md)

