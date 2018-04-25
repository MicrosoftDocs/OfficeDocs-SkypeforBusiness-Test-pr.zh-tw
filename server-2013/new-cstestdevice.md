---
title: New-CsTestDevice
TOCTitle: New-CsTestDevice
ms:assetid: 3d223c5e-b987-4353-9bf7-b247a2bdfa25
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425899(v=OCS.15)
ms:contentKeyID: 49290667
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTestDevice

 

_**上次修改主題的時間：** 2015-03-09_

建立新的裝置更新管理測試裝置。測試裝置可讓系統管理員先測試韌體更新，然後再將這些更新散發到組織中的所有裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsTestDevice -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsTestDevice -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Identifier <String> -IdentifierType <MACAddress | SerialNumber> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會針對 Redmond 網站建立新的測試裝置 (名稱為 UCPhone)。請注意，用來指定裝置 Identity 的語法：裝置範圍 (site:Redmond) 後面加上 / 字元，再加上裝置名稱 (UCPhone)。此裝置會使用序號做為 IdentifierType，且其序號為 07823-A345。

    New-CsTestDevice -Identity site:Redmond/UCPhone -IdentifierType SerialNumber -Identifier "07823-A345"

## 範例 2

範例 2 所示的命令是範例 1 所示命令的變化。不過，在範例 2 中，不會使用 Identity 參數。但是，Parent 參數會用來指定新測試裝置的範圍 (site:Redmond)，而 Name 參數會用來表示新裝置的名稱 (UCPhone)。**New-CsTestDevice** Cmdlet 將會採用這兩個參數值，並為您建構測試裝置 Identity (site:Redmond/UCPhone)。

    New-CsTestDevice -Parent "site:Redmond" -Name UCPhone -IdentifierType SerialNumber -Identifier "07823-A345"

## 詳細描述

藉由將與 Lync Phone Edition 相容的特定電話或其他裝置識別為測試裝置，系統管理員可以在將韌體更新部署至組織中的相關裝置之前，驗證並核准這些更新。裝置更新規則在匯入至 Lync Server 後，會標記為「擱置」，表示受影響的裝置將不會自動下載並安裝這些規則的更新對應。

但是，任何相關的測試裝置將會下載並安裝這些擱置的規則。這就是測試裝置背後的概念：新的裝置更新規則會自動套用至測試裝置，讓系統管理員有機會確認韌體更新是否如預期般運作。若是如此，這些系統管理員就可以將規則標示為核准；之後，組織中所有相關的裝置就會下載並安裝核准的規則。

測試裝置是使用 **New-CsTestDevice** Cmdlet 所建立。您可以在全域範圍或網站範圍設定這些裝置。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsTestDevice** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTestDevice"}

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
<td><p><em>Identifier</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>根據 IdentifierType，表示新測試裝置的媒體存取控制 (MAC) 位址或序號。可以使用數字、字母、連字號和底線來指定序號；例如：</p>
<p>-Identifier &quot;AB37_679e&quot;</p>
<p>MAC 位址必須指定為六個或更多兩個字元一對的格式；視 MAC 位址而定，這些配對可以連結在單一字串中，或者以連字號或冒號分隔 (請注意，MAC 位址可以同時包含字母和/或數字)。下列全部都是有效的 MAC 位址：</p>
<p>010203040506</p>
<p>01-02-03-04-05-06</p>
<p>01:02:03:04:05:06</p>
<p>不接受 01-02-03-04-05 這種 MAC 位址，因為它未達到最少六組雙字元。</p></td>
</tr>
<tr class="even">
<td><p><em>IdentifierType</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.IdentifierType</p></td>
<td><p>表示測試裝置是由其 MAC 位址或其序列唯一識別。若要依裝置的 MAC 位址識別該裝置，將 IdentifierType 設為 MACAddress。若要依裝置的序號識別該裝置，將 IdentifierType 設為 SerialNumber。MACAddress 和 SerialNumber 是唯一允許的值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示新測試裝置的 Identity。Identity 是由要指派給測試裝置的範圍 (如 site:Redmond) 和新裝置的名稱 (例如 UCPhone) 所組成。若要將名稱為 UCPhone 的測試裝置指派給 Redmond 網站，您的 Identity 參數必須看起來如下：-Identity &quot;site:Redmond/UCPhone&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>新測試裝置的名稱 (名稱在指定的範圍中必須是唯一的)。只有在使用 Parent 參數時，才應使用 Name 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派給新測試裝置之範圍的名稱 (例如，site:Redmond)。如果您使用 Parent 參數，則也必須使用 Name 參數；例如：-Parent site:Redmond –Name UCPhone。如果您使用 Parent 參數，則不應該使用 Identity 參數，反之亦然。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsTestDevice** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.TestDevice 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsTestDevice](get-cstestdevice.md)  
[Remove-CsTestDevice](remove-cstestdevice.md)  
[Set-CsTestDevice](set-cstestdevice.md)

