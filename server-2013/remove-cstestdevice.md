---
title: Remove-CsTestDevice
TOCTitle: Remove-CsTestDevice
ms:assetid: 995111e0-2ab2-49a1-83f0-fc873f5b5426
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398790(v=OCS.15)
ms:contentKeyID: 49291758
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTestDevice

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的裝置更新管理測試裝置。測試裝置可讓系統管理員先測試韌體更新，然後再將這些更新散發到組織中的所有裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsTestDevice -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會從 Redmond 網站移除所有測試裝置。這將移除裝置集合以及個別測試裝置。

    Remove-CsTestDevice -Identity site:Redmond

## 範例 2

範例 2 所示的命令會移除所有設定供組織使用的測試裝置，作法為使用 **Get-CsTestDevice** Cmdlet 傳回所有的測試裝置集合，然後將這些項目全都管線傳送至 **Remove-CsTestDevice** Cmdlet。請注意，雖然無法移除全域測試裝置集合，但此命令會刪除所有在全域層級設定的個別測試裝置。

    Get-CsTestDevice | Remove-CsTestDevice

## 範例 3

範例 3 會移除所有在網站範圍設定的測試裝置。為了執行此工作，命令會使用 **Get-CsTestDevice** Cmdlet 並搭配 Filter 參數，以傳回 Identity 開頭為字串值 "site:" 的所有測試裝置。然後再將篩選後的集合管線傳送到 **Remove-CsTestDevice** Cmdlet，以刪除集合中的所有項目。

    Get-CsTestDevice -Filter "site:" | Remove-CsTestDevice

## 範例 4

範例 4 所示的命令會刪除所有 LG-Nortel 手機測試裝置。為達成此目的，命令會先呼叫 **Get-CsTestDevice** Cmdlet，以傳回所有設定供組織使用的測試裝置。然後再將該資訊管線傳送至 **Where-Object** Cmdlet，以使用 -match 運算子傳回 Name 屬性包含字串值 "LG-Nortel" 的裝置。接著使用 **Remove-CsTestDevice** Cmdlet 刪除所有符合該準則的測試裝置。

    Get-CsTestDevice | Where-Object {$_.Name -match "LG-Nortel Phone"} | Remove-CsTestDevice

## 詳細描述

系統管理員可以藉由指定特定 Lync Phone Edition 相容電話或其他裝置做為測試裝置，在韌體更新部署到組織中的所有相關裝置之前，先驗證並核准這些更新。裝置更新規則在匯入 Lync Server 後會標以「擱置」，表示受影響的裝置不會自動下載並安裝這些規則的對應更新。

但是相關的測試裝置將會下載並安裝這些擱置的規則。這就是測試裝置背後的概念：新的裝置更新規則會自動套用至測試裝置，讓系統管理員有機會確認韌體更新是否如預期般運作。如果韌體更新如預期般運作，系統管理員可以將規則標記為已核准；然後，組織中的所有相關裝置就會下載並安裝已核准的規則。

測試裝置是執行 Lync Server 的硬體裝置。這些裝置是使用 **New-CsTestDevice** Cmdlet 所建立。一旦建立之後，日後可藉由執行 **Remove-CsTestDevice** Cmdlet 來移除裝置。請注意，若將裝置移除為測試裝置，實際裝置本身並不會受到影響；例如，您的 Lync Phone Edition 手機仍可以用來存取 Lync Server。唯一的差別就是，因為裝置不再是測試裝置，所以它將不再下載處於擱置狀態的裝置更新規則，而是會等到規則獲准後，才下載並安裝這些規則。

**Remove-CsTestDevice** Cmdlet 可以用來移除在全域或網站範圍設定的個別測試裝置。您也可以使用此 Cmdlet 來移除所有針對特定範圍設定的測試裝置。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsTestDevice** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTestDevice"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示要移除之測試裝置的 Identity。若要移除特定裝置，請同時加上範圍 (例如 site:Redmond) 和裝置名稱，例如：-Identity &quot;site:Redmond/UCPhoneTest&quot;。若要從特定網站移除所有裝置，請使用下列語法：-Identity &quot;site:Redmond&quot;。</p>
<p>您也可以從全域範圍中移除測試裝置。無法移除全域測試裝置集合本身；但下列命令會刪除已儲存在全域集合中的所有裝置：</p>
<p>Remove-CsTestDevice –Identity global</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.TestDevice 物件。**Remove-CsTestDevice** Cmdlet 接受管線傳送的測試裝置物件輸入。

## 傳回類型

**Remove-CsTestDevice** Cmdlet 不會傳回值或物件，而會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.TestDevice 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsTestDevice](get-cstestdevice.md)  
[New-CsTestDevice](new-cstestdevice.md)  
[Set-CsTestDevice](set-cstestdevice.md)

