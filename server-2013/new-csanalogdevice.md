---
title: New-CsAnalogDevice
TOCTitle: New-CsAnalogDevice
ms:assetid: c02755d6-b651-4385-91a0-5b594dc67751
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412937(v=OCS.15)
ms:contentKeyID: 49292190
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAnalogDevice

 

_**上次修改主題的時間：** 2015-03-09_

建立可由 Lync Server 管理的裝置。類比裝置是指連接到公用交換電話網路 (PSTN) 的電話或其他裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsAnalogDevice -DN <ADObjectId> <COMMON PARAMETERS>

    New-CsAnalogDevice -OU <OUIdParameter> <COMMON PARAMETERS>

    COMMON PARAMETERS: -AnalogFax <$true | $false> -Gateway <Fqdn> -LineUri <String> -RegistrarPool <Fqdn> [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會利用電話號碼 (LineUri) 1-425-555-6001 來建立新的類比裝置 (請注意，電話號碼必須使用 E.164 格式來指定)。除了 LineUri 參數之外，此命令中使用的其他參數如下：DisplayName (可設定裝置的 Active Directory 顯示名稱)；RegistrarPool (可指定登錄器集區)；AnalogFax (設定為 $False，表示這是電話而非傳真機)；Gateway (設定為閘道的 IP 位址)；以及 OU (應在其中建立裝置連絡人物件之 Active Directory OU 的辨別名稱)。

    New-CsAnalogDevice -LineUri tel:+14255556001 -DisplayName "Building 14 Receptionist" -RegistrarPool redmond-Cs-001.litwareinc.com -AnalogFax $False -Gateway 192.168.0.240 -OU "ou=Telecommunications,dc=litwareinc,dc=com"

## 詳細描述

類比裝置包含電話、傳真機、數據機，以及與公用交換電話網路 (PSTN) 連接的聽障人士電傳通訊裝置 (TTY/TDD)。與利用 Enterprise Voice (Microsoft 提供的 Voice over Internet Protocol (VoIP) 解決方案) 的裝置不同，類比裝置不會使用數位封包傳輸資訊；而是使用連續訊號來傳輸資訊。此訊號通常稱做類比訊號，因此這類裝置稱做「類比裝置」。

為了讓系統管理員能夠管理類比裝置，Lync Server 讓您能夠將類比裝置與 Active Directory 連絡人物件產生關聯。在裝置已與連絡人物件產生關聯後，您便可藉由指派原則與撥號對應表至該連絡人，以管理類比裝置。

您可以使用 **New-CsAnalogDevice** Cmdlet 來建立新的類比裝置。此 Cmdlet 可以建立新的連絡人物件以便與類比裝置搭配使用，或者可將現有的連絡人物件關聯至新裝置。如需詳細資訊，請參閱本主題的 OU 和 DN 參數描述。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsAnalogDevice** Cmdlet：RTCUniversalUserAdmins。可以使用 **Grant-CsOUPermission** Cmdlet，為特定網站或特定 Active Directory 組織單位 (OU) 指派執行此 Cmdlet 的權限。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsAnalogDevice"}

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
<td><p><em>AnalogFax</em></p></td>
<td><p>必要</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果類比裝置為傳真機則設為 True ($True)。如果裝置不是傳真機則設為 False ($False)。</p></td>
</tr>
<tr class="even">
<td><p><em>DN</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.ADObjectId</p></td>
<td><p>讓您能夠將現有的 Active Directory 連絡人物件關聯至類比裝置。如果您想要將連絡人物件關聯至類比裝置，請使用 DN 參數，後面加上該連絡人的辨別名稱。例如：-DN &quot;cn=Building 14 Lobby,dc=litwareinc,dc=com&quot;。請注意，如果指定的連絡人不存在，命令將會失敗。</p>
<p>您無法在同一個命令中使用 OU 和 DN 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Gateway</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>表示類比裝置使用之 PSTN 閘道的 IP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>LineUri</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>類比裝置的電話號碼。指定線路統一資源識別元 (URI) 時應該採用 E.164 格式，並在開頭加上 &quot;TEL:&quot;首碼。例如：TEL:+14255551297。任何分機號碼都應該新增至線路 URI 的尾端，例如：&quot;TEL:+14255551297;ext=51297&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>OU</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>連絡人物件應位於其中之 Active Directory 組織單位 (OU) 的辨別名稱。例如：-OU &quot;ou=Redmond,dc=litwareinc,dc=com”。</p>
<p>如果您加入 OU 參數，會在指定的 OU 中建立一個新連絡人，而且該連絡人會自動被指派一個 GUID (全域唯一識別碼) 做為其一般名稱。因此，連絡人物件將具備類似下列的名稱：{ce84964a-c4da-4622-ad34-c54ff3ed361f}。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPool</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>連絡人物件應隸屬之登錄器集區的完整網域名稱 (FQDN)。例如：-RegistrarPool &quot;atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>設定類比裝置的 Active Directory 顯示名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>在 Lync 中顯示的電話號碼。DisplayNumber 屬性可設為任何您偏好的格式，例如 1-800-555-1234、1-(800)-555-1234、1.800.555.1234 等。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回代表一般區域電話的物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓類比裝置與諸如 Lync 的 SIP 裝置進行通訊的唯一識別碼 (類似電子郵件地址)。SIP 位址的開頭必須是首碼 &quot;sip:&quot;。例如：sip:bldg14lobby@litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsAnalogDevice** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsAnalogDevice** Cmdlet 會建立 Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsAnalogDevice](get-csanalogdevice.md)  
[Move-CsAnalogDevice](move-csanalogdevice.md)  
[Remove-CsAnalogDevice](remove-csanalogdevice.md)  
[Set-CsAnalogDevice](set-csanalogdevice.md)

