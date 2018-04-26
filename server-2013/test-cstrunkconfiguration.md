---
title: Test-CsTrunkConfiguration
TOCTitle: Test-CsTrunkConfiguration
ms:assetid: 07f2ef04-49aa-4857-b213-fa98506c0427
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398137(v=OCS.15)
ms:contentKeyID: 49290001
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsTrunkConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

驗證主幹組態是否適用於電話號碼。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsTrunkConfiguration -TrunkConfiguration <TrunkConfiguration> [-CallingNumber <PhoneNumber>] [-DialedNumber <PhoneNumber>]

## 範例

## 範例 1

此範例會對針對 Redmond 網站定義的主幹組態執行測試。此範例中的第一行會呼叫 **Get-CsTrunkConfiguration** Cmdlet，以擷取 Redmond 網站的組態 (Identity 為 site:Redmond 的組態)。擷取的主幹組態物件會被指派給 $tc 變數。

在第 2 行中，我們會呼叫 **Test-CsTrunkConfiguration** Cmdlet，將要測試的電話號碼傳遞至 DialedNumber 參數，並將在第 1 行中擷取的主幹組態 (以 $tc 儲存) 傳遞至 TrunkConfiguration 參數。

    $tc = Get-CsTrunkConfiguration -Identity Site:Redmond
    Test-CsTrunkConfiguration -DialedNumber 4255551212 -TrunkConfiguration $tc

## 詳細描述

使用此 Cmdlet 針對撥打的電話號碼，驗證主幹組態是否如預期般運作。每個組態包含特定設定，定義中繼伺服器與服務提供者的公用交換電話網路 (PSTN) 閘道、IP 公用交換機 (PBX) 或工作階段界限控制器 (SBC) 之間的關係和功能。這些設定所設定的項目包括此主幹是否啟用媒體旁路、是否在特定情況下傳送即時傳輸控制通訊協定 (RTCP) 封包，以及是否需要安全即時通訊協定 (SRTP) 加密。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Test-CsTrunkConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsTrunkConfiguration"}

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
<td><p><em>TrunkConfiguration</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration</p></td>
<td><p>要針對其執行測試之主幹組態物件的參考。您可以呼叫 <strong>Get-CsTrunkConfiguration</strong> Cmdlet 來擷取主幹組態物件。</p></td>
</tr>
<tr class="even">
<td><p><em>CallingNumber</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
<td><p>指定此參數時，會針對所指定的電話號碼，傳回相符的外撥轉譯規則。例如：</p>
<p>-CallingNumber &quot;tel:+14255551219&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>DialedNumber</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
<td><p>要針對其測試組態的電話號碼。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration 物件。接受管線傳送的主幹組態物件輸入。

## 傳回類型

傳回 Microsoft.Rtc.Management.Voice.TrunkConfigurationTestResult 類型的值。

## 請參閱

#### 其他資源

[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Set-CsTrunkConfiguration](set-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)

