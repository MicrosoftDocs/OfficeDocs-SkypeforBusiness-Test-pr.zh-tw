---
title: Test-CsInterTrunkRouting
TOCTitle: Test-CsInterTrunkRouting
ms:assetid: 2248d29a-8a2a-42b1-ab6b-a6c1d74b0455
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204741(v=OCS.15)
ms:contentKeyID: 49290331
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsInterTrunkRouting

 

_**上次修改主題的時間：** 2015-03-09_

檢查路由來自指定 SIP 主幹之電話時的路由與 PSTN 使用方式。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsInterTrunkRouting -TargetNumber <PhoneNumber> -TrunkConfiguration <TrunkConfiguration> [-Force <SwitchParameter>] [-RouteSettings <PstnRoutingSettings>]

## 範例

## 範例 1

範例 1 所示的命令會傳回相符的路由和相符的電話使用方式，讓使用者能夠使用 Redmond 網站的主幹組態設定來撥打電話號碼 1-206-555-1219。

    $trunk = Get-CsTrunkConfiguration -Identity "site:Redmond"
    
    Test-CsInterTrunkRouting -TargetNumber "tel:+12065551219" -TrunkConfiguration $trunk

## 詳細描述

Test-CsInterTrunkRouting 可驗證通設是否可以在 SIP 之間路由。為達此目的，會為此 Cmdlet 指定一組電話號碼與主幹設定。Test-CsInterTrunkRouting 會依據指定的號碼回報符合的路由與 PSTN 使用方式。請注意，主幹的號碼模式必須符合指定的電話號碼，而且至少要有一種 PSTN 使用方式相通，通話才可在主幹之間路由。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsInterTrunkRouting"}

**Lync Server 控制台：**Lync Server 控制台不提供 Test-CsInterTrunkRouting Cmdlet 所執行的功能。

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
<td><p><em>TargetNumber</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
<td><p>進行測試時所要撥打的 PSTN 電話號碼。目標電話號碼應以 E.164 格式來指定，這表示該號碼看起來會如下所示：</p>
<p>-TargetNumber &quot;tel:+12065551219&quot;</p>
<p>電話號碼應包含 &quot;tel:&quot; 首碼，後面接加號 (+)、國碼/地區碼 (1)、區碼 (206) 及電話號碼 (5551219)。指定電話號碼時，請勿使用虛線、括弧或其他任何字元。</p></td>
</tr>
<tr class="even">
<td><p><em>TrunkConfiguration</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration</p></td>
<td><p>所測試之主幹組態的物件參照。若要建立此物件參照，請使用類似下列的命令：</p>
<p>$trunk = Get-CsTrunkConfiguration –Identity &quot;site:Redmond&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>RouteSettings</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnRoutingSettings</p></td>
<td><p>物件參照，可讓您在呼叫 Test-CsInterTrunkRouting 時，指定語音路由組態設定的集合。若要建立此物件參照，請使用類似下列的命令：</p>
<p>$route = Get-CsRoutingConfiguration –Identity &quot;global&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。Test-CsInterTrunkRouting 不接受管線傳送的輸入。

## 傳回類型

Test-CsInterTrunkRouting 會傳回 Microsoft.Rtc.Management.Voice.InterTrunkRoutingTestResult 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsTrunk](get-cstrunk.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)

