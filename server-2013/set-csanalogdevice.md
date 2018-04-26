---
title: Set-CsAnalogDevice
TOCTitle: Set-CsAnalogDevice
ms:assetid: b05e729e-cdef-4c78-8ce7-b183c3208a93
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412843(v=OCS.15)
ms:contentKeyID: 49292013
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAnalogDevice

 

_**上次修改主題的時間：** 2015-03-09_

修改類比裝置集合中可由 Lync Server 管理的現有裝置。類比裝置是指連接到公用交換電話網路 (PSTN) 的電話或其他裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsAnalogDevice -Identity <UserIdParameter> [-AnalogFax <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-Gateway <Fqdn>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會針對 Identity 為 CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com 的類比裝置變更 LineUri 屬性的值。

    Set-CsAnalogDevice -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -LineUri "TEL:+14255551298"

## 範例 2

範例 2 所示的命令會變更每個目前使用 192.168.0.240 閘道的類比裝置閘道。為達成此目的，會呼叫 **Get-CsAnalogDevice** Cmdlet 搭配 Filter 參數；篩選值 {Gateway -eq "192.168.0.240"} 可確保只傳回 Gateway 等於 (-eq) 192.168.0.240 的裝置。然後再將此篩選後的集合管線傳送到 **Set-CsAnalogDevice** Cmdlet，以取得集合中的每個項目，並將 Gateway 屬性的值變更為 192.168.1.100。

    Get-CsAnalogDevice -Filter {Gateway -eq "192.168.0.240"} | Set-CsAnalogDevice -Gateway "192.168.1.100"

## 詳細描述

類比裝置包含電話、傳真機、數據機，以及與公用交換電話網路 (PSTN) 連接的聽障人士電傳通訊裝置 (TTY/TDD)。與利用 Enterprise Voice (亦即由 Microsoft 提供的 Voice over Internet Protocol (VoIP) 解決方案) 的裝置不同，類比裝置不會使用數位封包傳輸資訊，而是使用連續訊號來傳輸資訊。此訊號通常稱做類比訊號，因此這類裝置稱做「類比裝置」。

為了讓系統管理員能夠管理類比裝置，Lync Server 讓您能夠將類比裝置與 Active Directory 連絡人物件產生關聯。在裝置已與連絡人物件產生關聯後，您便可藉由指派原則與撥號對應表至該連絡人，以管理類比裝置。

**Set-CsAnalogDevice** Cmdlet 讓您能夠修改與類比裝置相關聯連絡人物件的屬性。例如，您可以變更連絡人的 Active Directory 顯示名稱，或與裝置相關聯的線路統一資源識別元 (URI)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsAnalogDevice** Cmdlet：RTCUniversalUserAdmins。您可以使用 **Grant-CsOUPermission** Cmdlet，為特定的網站或特定的 Active Directory 組織單位 (OU) 指派執行此 Cmdlet 的權限。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAnalogDevice"}

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
<td><p>UserIdParameter</p></td>
<td><p>要修改之類比裝置的唯一識別碼。類比裝置是使用相關聯連絡人物件的 Active Directory 辨別名稱 (DN) 來識別。根據預設，類比裝置會使用 GUID (全域唯一識別碼) 做為一般名稱，這表示這些裝置通常具有如下的 Identity：CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com。這表示您可能發現使用 <strong>Get-CsAnalogDevice</strong> Cmdlet 傳回類比裝置物件後，再將這些物件管線傳送到 <strong>Set-CsAnalogDevice</strong> Cmdlet，會是修改類比裝置的較簡單方式。</p></td>
</tr>
<tr class="even">
<td><p><em>AnalogFax</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>如果類比裝置為傳真機則設為 True ($True)。如果裝置不是傳真機則設為 False ($False)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>設定類比裝置的 Active Directory 顯示名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>在 Lync 中顯示的電話號碼。DisplayNumber 屬性可設為任何您偏好的格式，例如 1-800-555-1234、1-(800)-555-1234、1.800.555.1234 等。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以修改連絡人資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-mcs-001) 或其完整網域名稱 (FQDN) (例如，atl-mcs-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True ($True) 時，類比裝置可以搭配 Lync 使用。</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出是否已針對 Enterprise Voice 啟用類比裝置的連絡人物件；Enterprise Voice 是由 Microsoft 所提供的 VoIP 解決方案。透過 Enterprise Voice，便可使用網際網路撥打電話，而非使用標準電話網路。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>表示連絡人之立即訊息工作階段的封存位置。允許的值為：</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>Gateway</em></p></td>
<td><p>選用</p></td>
<td><p>Fqdn</p></td>
<td><p>表示類比裝置使用之 PSTN 閘道的 IP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>類比裝置的電話號碼。指定線路 URI 時應該採用 E.164 格式，並在開頭加上 &quot;TEL:&quot;首碼。例如：TEL:+14255551297。任何分機號碼都應該新增至線路 URI 的尾端；例如：TEL:+14255551297; ext=51297。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>witchParameter</p></td>
<td><p>傳回代表一般區域電話的物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>允許類比裝置與 SIP 裝置 (例如 Lync 2013) 通訊的唯一識別碼。SIP 位址的開頭必須是首碼 &quot;sip:&quot;。例如：sip:bldg14lobby@litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact 物件。**Set-CsAnalogDevice** Cmdlet 接受類比裝置物件管線傳送的執行個體。

## 傳回類型

根據預設，**Set-CsAnalogDevice** Cmdlet 不會傳回任何物件或值。但是，如果加入 PassThru 參數，Cmdlet 就會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAnalogDevice](get-csanalogdevice.md)  
[Move-CsAnalogDevice](move-csanalogdevice.md)  
[New-CsAnalogDevice](new-csanalogdevice.md)  
[Remove-CsAnalogDevice](remove-csanalogdevice.md)

