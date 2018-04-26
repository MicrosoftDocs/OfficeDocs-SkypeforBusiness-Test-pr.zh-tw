---
title: Remove-CsAnalogDevice
TOCTitle: Remove-CsAnalogDevice
ms:assetid: 61250894-fde6-476d-aaa2-ec5692af02b3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398433(v=OCS.15)
ms:contentKeyID: 49291082
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAnalogDevice

 

_**上次修改主題的時間：** 2015-03-09_

從可以由 Lync Server 管理之類比裝置集合中移除現有的裝置。類比裝置是指連接到公用交換電話網路 (PSTN) 的電話或其他裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsAnalogDevice -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會刪除 Identity 為 CN={e5e7daba-394e-46ec-95a1-1f2a9947aad2},CN=Users,DC=litwareinc,DC=com 的類比裝置。

    Remove-CsAnalogDevice -Identity "CN={e5e7daba-394e-46ec-95a1-1f2a9947aad2},CN=Users,DC=litwareinc,DC=com"

## 範例 2

範例 2 所示的命令會刪除任何所指派之顯示名稱為 "Building 14 Receptionist" 的類比裝置。為了執行此工作，命令會先呼叫 **Get-CsAnalogDevice** Cmdlet 並搭配 Filter 參數；篩選值 {DisplayName -eq "Building 14 Receptionist"} 可將傳回的物件限制在 DisplayName 屬性等於 "Building 14 Receptionist" 的類比裝置。接著將傳回的項目管線傳送到 **Remove-CsAnalogDevice** Cmdlet，以移除傳回的項目。

    Get-CsAnalogDevice -Filter {DisplayName -eq "Building 14 Receptionist"} | Remove-CsAnalogDevice

## 範例 3

範例 3 會刪除所有已獲指派語音原則 RedmondVoicePolicy 的類比裝置。為達成此目的，命令會使用 **Get-CsAnalogDevice** Cmdlet 並搭配 Filter 參數，以擷取所有 VoicePolicy 屬性等於 RedmondVoicePolicy 的類比裝置。然後再將篩選後的集合管線傳送到 **Remove-CsAnalogDevice** Cmdlet，以刪除該集合中的每個項目。

    Get-CsAnalogDevice -Filter {VoicePolicy -eq "RedmondVoicePolicy"} | Remove-CsAnalogDevice

## 範例 4

範例 4 的命令會移除組織目前所使用的所有類比傳真機。為了執行此工作，命令會先呼叫 **Get-CsAnalogDevice** Cmdlet 並搭配 Filter 參數 (篩選值 {AnalogFax –eq $True} 會只挑選 AnalogFax 屬性等於 True 的裝置)。然後再將此篩選後的集合管線傳送到 **Remove-CsAnalogDevice** Cmdlet，以移除集合中的每個項目。

    Get-CsAnalogDevice -Filter {AnalogFax -eq $True} | Remove-CsAnalogDevice

## 詳細描述

類比裝置包括和公用交換電話網路 (PSTN) 連接的電話、傳真機、數據機，以及聽障人士電傳通訊裝置 (TTY/TDD)。與利用 Enterprise Voice (Microsoft 提供的 Voice over Internet Protocol (VoIP) 解決方案) 的裝置不同，類比裝置不會使用數位封包傳輸資訊；而是使用連續訊號來傳輸資訊。此訊號通常稱做類比訊號，也因此這類裝置稱做「類比裝置」。

為了讓系統管理員能夠管理組織的類比裝置，Lync Server 讓您能夠將類比裝置與 Active Directory 連絡人物件產生關聯。在裝置已與連絡人物件產生關聯後，您便可藉由指派原則與撥號對應表至該連絡人，以管理類比裝置。

經過一段時間後，您可能需要刪除與類比裝置相關聯的連絡人物件。例如，如果您淘汰所有的傳真機，便不再需要有與那些傳真機相關聯的類比裝置 (與連絡人物件)。**Remove-CsAnalogDevice** Cmdlet 能讓您刪除類比裝置。當您執行此 Cmdlet 時，會由 **Get-CsAnalogDevice** Cmdlet 傳回的類比裝置清單中刪除裝置。此外，與該裝置相關聯的連絡人物件也會從 Active Directory 網域服務中刪除。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsAnalogDevice** Cmdlet：RTCUniversalUserAdmins。可以使用 **Grant-CsOUPermission** Cmdlet，為特定網站或特定 Active Directory 組織單位 (OU) 指派執行此 Cmdlet 的權限。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsAnalogDevice"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>要移除之類比裝置的唯一識別碼。類比裝置是使用相關聯連絡人物件的 Active Directory 辨別名稱 (DN) 來識別。根據預設，這些裝置使用全域唯一識別碼 (GUID) 做為其一般名稱，這表示類比裝置通常具有類似如下的 Identity：CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com。因此，您可能會發現使用 <strong>Get-CsAnalogDevice</strong> Cmdlet 更容易擷取類比裝置，然後再將傳回的物件管線傳送到 <strong>Remove-CsAnalogDevice</strong> Cmdlet。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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

Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact 物件。**Remove-CsAnalogDevice** Cmdlet 接受管線傳送的類比裝置物件執行個體。

## 傳回類型

**Remove-CsAnalogDevice** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsAnalogDevice](get-csanalogdevice.md)  
[Move-CsAnalogDevice](move-csanalogdevice.md)  
[New-CsAnalogDevice](new-csanalogdevice.md)  
[Set-CsAnalogDevice](set-csanalogdevice.md)

