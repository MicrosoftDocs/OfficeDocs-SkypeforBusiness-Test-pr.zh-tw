---
title: Set-CsTestDevice
TOCTitle: Set-CsTestDevice
ms:assetid: 0a9fabfc-b0d3-4c94-ae04-0a87f0886db8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398156(v=OCS.15)
ms:contentKeyID: 49290038
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTestDevice

 

_**上次修改主題的時間：** 2015-03-09_

修改一或多個設定供組織使用的裝置更新管理測試裝置。測試裝置可讓系統管理員先測試韌體更新，然後再將這些更新散發到組織中的所有裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsTestDevice [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsTestDevice [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Identifier <String>] [-IdentifierType <MACAddress | SerialNumber>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會修改指派給 Redmond 網站，且名稱為 UCPhone 之測試裝置的 Identifier 屬性。

    Set-CsTestDevice -Identity site:Redmond/UCPhone -Identifier "09768-ABDR-83295"

## 範例 2

範例 2 所示的命令也會修改指派給 Redmond 網站，且名稱為 UCPhone 的測試裝置。但在此範例中，此命令不僅會指定一個新的 Identifier，也會指派一個新的 IdentifierType：SerialNumber。

    Set-CsTestDevice -Identity site:Redmond/UCPhone -IdentifierType SerialNumber -Identifier "09768-ABDR-83295"

## 詳細描述

藉由識別執行 Lync Phone Edition 之特定手機或其他裝置做為測試裝置，系統管理員可以在將韌體更新部署至組織中的所有相關裝置之前，驗證並核准這些更新。裝置更新規則在匯入至 Lync Server 後，會被標記為「擱置」，表示受影響的裝置將不會自動安裝並安裝這些規則的對應更新。

但是，任何相關的測試裝置將會下載並安裝這些擱置的規則。這就是測試裝置背後的概念：新的裝置更新規則會自動套用至測試裝置，讓系統管理員有機會確認韌體更新是否如預期般運作。若是如此，這些系統管理員就可以將規則標示為核准；之後，組織中所有相關的裝置就會下載並安裝核准的規則。

測試裝置是使用 **New-CsTestDevice** Cmdlet 所建立。建立測試裝置之後，您便可以使用 **Set-CsTestDevice** Cmdlet 來變更該裝置或其他任何測試裝置的 Identifier 和 IdentifierType。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsTestDevice** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTestDevice"}

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
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identifier</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>根據 IdentifierType，表示新測試裝置的媒體存取控制 (MAC) 位址或序號。可以使用數字、字母、連字號和底線來指定序號；例如：</p>
<p>-Identifier &quot;AB37_679e&quot;</p>
<p>MAC 位址必須指定為六個或更多兩個字元一對的格式；視 MAC 位址而定，這些配對可以是單一字串值，或者以連字號或冒號分隔 (請注意，MAC 位址可以同時包含字母和/或數字)。下列全部都是有效的 MAC 位址：</p>
<p>010203040506</p>
<p>01-02-03-04-05-06</p>
<p>01:02:03:04:05:06</p>
<p>不接受 01-02-03-04-05 這種 MAC 位址，因為它未達到最少六組雙字元。</p></td>
</tr>
<tr class="even">
<td><p><em>IdentifierType</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.IdentifierType</p></td>
<td><p>表示測試裝置是由其 MAC 位址或其序列唯一識別。若要依裝置的 MAC 位址識別該裝置，將 IdentifierType 設為 MACAddress。若要依裝置的序號識別該裝置，將 IdentifierType 設為 SerialNumber。MACAddress 和 SerialNumber 是唯一允許的值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示要修改之測試裝置的 Identity。例如：-Identity site:Redmond/UCPhoneTestDevice。請注意，如有指定 Identity，即無法使用萬用字元。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>測試裝置物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.TestDevice 物件。**Set-CsTestDevice** Cmdlet 接受管線傳送的測試裝置物件輸入。

## 傳回類型

**Set-CsTestDevice** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.TestDevice 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsTestDevice](get-cstestdevice.md)  
[New-CsTestDevice](new-cstestdevice.md)  
[Remove-CsTestDevice](remove-cstestdevice.md)

