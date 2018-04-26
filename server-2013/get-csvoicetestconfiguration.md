---
title: Get-CsVoiceTestConfiguration
TOCTitle: Get-CsVoiceTestConfiguration
ms:assetid: c23235db-500c-4303-8c75-b4ae341b3807
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412957(v=OCS.15)
ms:contentKeyID: 49292221
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceTestConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取用以測試電話號碼是否符合指定路由與規則的測試案例。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsVoiceTestConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceTestConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

擷取所有的語音測試組態設定。

    Get-CsVoiceTestConfiguration

## 範例 2

這個範例會擷取所有的語音測試組態設定，只顯示每一個設定的 Identity、DialedNumber 和 ExpectedTranslatedNumber 參數。**Get-CsVoiceTestConfiguration** Cmdlet 傳回的設定會管線傳送到 **Select-Object** Cmdlet，它會將輸出範圍縮小到 Identity、DialedNumber 和 ExpectedTranslatedNumber 屬性。

    Get-CsVoiceTestConfiguration | Select-Object Identity, DialedNumber, ExpectedTranslatedNumber

## 範例 3

這個範例使用 Filter 參數擷取識別身分中包含字串 "test" 的所有語音測試組態設定。篩選值開頭和結尾的萬用字元 (\*) 表示字串 "test" 可位於 Identity 中的任何位置，該字串的前面或後面可以是任何字元。例如，這個命令會傳回名稱為 TestConfig、VoiceNumberTest 和 VoiceTest1 的語音測試設定。

    Get-CsVoiceTestConfiguration -Filter *test*

## 詳細描述

這個 Cmdlet 會擷取語音路由、使用方式、撥號對應表和據以測試指定之電話號碼的語音原則。在實作語音路由和語音原則之前，最好先以不同的電話號碼來測試，以確保結果符合您的預期。可以使用這個 Cmdlet 擷取測試設定，然後使用 **Test-CsVoiceConfiguration** Cmdlet 執行該案例，以執行此測試。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsVoiceTestConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceTestConfiguration"}

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
<td><p>此參數提供以萬用字元搜尋定義的語音測試設定的方式 (如需詳細資訊，請參閱本主題中的範例)。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>唯一識別您要擷取之測試設定的字串。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取語音測試組態，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration 類型的一個或多個物件。

## 請參閱

#### 其他資源

[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)

