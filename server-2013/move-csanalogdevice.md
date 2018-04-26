---
title: Move-CsAnalogDevice
TOCTitle: Move-CsAnalogDevice
ms:assetid: c629c5f8-93e7-4fe4-ad51-52bc0ae99a46
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398816(v=OCS.15)
ms:contentKeyID: 49292261
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsAnalogDevice

 

_**上次修改主題的時間：** 2015-03-09_

將一或多個類比裝置移至新的登錄器集區。類比裝置是指連接到公用交換電話網路 (PSTN) 連接的電話或其他裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Move-CsAnalogDevice -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 Identity 為 CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com 的類比裝置移至登錄器集區 atl-cs-001.litwareinc.com。

    Move-CsAnalogDevice -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -Target atl-cs-001.litwareinc.com

## 範例 2

範例 2 會將 Active Directory 顯示名稱為 "Building 14, Room 142" 的類比裝置移至登錄器集區 atl-cs-001.litwareinc.com。為成達此目的，會先呼叫不含任何參數的 **Get-CsAnalogDevice** Cmdlet，以傳回組織目前使用之所有類比裝置的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出顯示名稱為 "Building 14, Room 142" 的所有裝置。接著將該篩選後的集合管線傳送到 **Move-CsAnalogDevice** Cmdlet，以將集合中的所有裝置移至登錄器集區 atl-cs-001.litwareinc.com。

    Get-CsAnalogDevice | Where-Object {$_.DisplayName -eq "Building 14, Room 142"} | Move-CsAnalogDevice -Target atl-cs-001.litwareinc.com

## 範例 3

範例 3 所示的命令會移動顯示名稱是以字串值 "Building 14" 開頭的所有類比裝置。為了執行此工作，命令會先呼叫 **Get-CsAnalogDevice** Cmdlet，以傳回組織目前使用之所有類比裝置的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以選取顯示名稱是以字串值 "Building 14" 開頭的所有裝置。接著將篩選後的集合管線傳送到 **Move-CsAnalogDevice** Cmdlet，以將集合中的每一個裝置移至登錄器集區 atl-cs-001.litwareinc.com。

    Get-CsAnalogDevice | Where-Object {$_.DisplayName -like "Building 14*"} | Move-CsAnalogDevice -Target atl-cs-001.litwareinc.com

## 詳細描述

類比裝置包含電話、傳真機、數據機，以及與公用交換電話網路 (PSTN) 連接的聽障人士電傳通訊裝置 (TTY/TDD)。與利用 Enterprise Voice (Microsoft 提供的 Voice over Internet Protocol (VoIP) 解決方案) 的裝置不同，類比裝置不會使用數位封包傳輸資訊；而是使用連續訊號來傳輸資訊。此訊號通常稱做類比訊號，因此這類裝置稱做「類比裝置」。

為了讓系統管理員能夠管理類比裝置，Lync Server 讓您能夠將類比裝置與 Active Directory 連絡人物件產生關聯。在裝置已與連絡人物件產生關聯後，您便可藉由指派原則與撥號對應表至該連絡人，以管理類比裝置。

**Move-CsAnalogDevice** Cmdlet 可讓您將現有類比裝置移至新的登錄器集區。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Move-CsAnalogDevice** Cmdlet：RTCUniversalUserAdmins。可以使用 **Grant-CsOUPermission** Cmdlet，為特定網站或特定 Active Directory 組織單位 (OU) 指派執行此 Cmdlet 的權限。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsAnalogDevice"}

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
<td><p>類比裝置的唯一識別碼。類比裝置使用關聯連絡人物件的 Active directory 辨別名稱來識別。根據預設，類比裝置使用 GUID (全域唯一識別碼) 做為一般名稱，這表示裝置的 Identity 通常會與此類似：CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com。</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>應移動其類比裝置之登錄器集區的完整網域名稱 (FQDN) (例如，atl-cs-001.litwareinc.com)。除了登錄器集區外，Target 也可以是主機供應商的 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>讓您連線至指定的網域控制站，以移動類比裝置。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-cs-001) 或其 FQDN (例如，atl-cs-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，則會移動類比裝置，但刪除任何關聯的資料 (例如已指派給裝置的原則)。如果不存在，則會連同任何關聯的資料一起移動裝置。</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會指示電腦忽略後端資料庫可能發生的任何錯誤，並嘗試移動公用區電話而不管這些錯誤。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>讓您透過管線傳遞使用者物件，代表被移動的使用者帳戶。根據預設，<strong>Move-CsAnalogDevice</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>此參數只能用於 Microsoft Lync Online 2010。請勿用於 Lync Server 的內部部署實作。</p></td>
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

字串。**Move-CsAnalogDevice** Cmdlet 接受代表類比裝置之 Identity 的管線傳送字串值。

## 傳回類型

根據預設，**Move-CsAnalogDevice** Cmdlet 不會傳回任何物件或值。但是，如果加入 PassThru 參數，Cmdlet 就會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAnalogDevice](get-csanalogdevice.md)  
[New-CsAnalogDevice](new-csanalogdevice.md)  
[Remove-CsAnalogDevice](remove-csanalogdevice.md)  
[Set-CsAnalogDevice](set-csanalogdevice.md)

