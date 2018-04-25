---
title: Get-CsTestDevice
TOCTitle: Get-CsTestDevice
ms:assetid: 4c88d448-4130-40de-b7e9-7389922322f4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398304(v=OCS.15)
ms:contentKeyID: 49290846
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTestDevice

 

_**上次修改主題的時間：** 2015-03-09_

擷取設定供組織使用之裝置更新管理測試裝置的資訊。測試裝置可讓系統管理員先測試韌體更新，然後再將這些更新散發到組織中的所有裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsTestDevice [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsTestDevice [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回組織中的所有測試裝置。呼叫不含任何其他參數的 **Get-CsTestDevice** Cmdlet 會傳回目前所使用的所有測試裝置。

    Get-CsTestDevice

## 範例 2

此範例會傳回指派給 Redmond 網站且名稱為 UCPhone 的測試裝置。

    Get-CsTestDevice -Identity site:Redmond/UCPhone

## 範例 3

在範例 3 中，此命令會傳回針對 Redmond 網站設定的所有測試裝置。

``` 
Get-CsTestDevice -Identity site:Redmond  
```

## 範例 4

範例 4 會傳回已在網站範圍設定的所有測試裝置。為達此目的，命令會使用 Filter 參數 (篩選值 "site:\*" 可將傳回的資料限制為 Identity 開頭為字串值 "site:" 的測試裝置)。

    Get-CsTestDevice -Filter site:*

## 詳細描述

藉由將與 Lync Phone Edition 相容的特定電話或其他裝置識別為測試裝置，系統管理員可以在將韌體更新部署至組織中的所有相關裝置之前，驗證並核准這些更新。裝置更新規則在匯入至 Lync Server 後，會標記為「擱置」，表示受影響的裝置將不會自動下載並安裝這些規則的更新對應。

但是，任何相關的測試裝置將會下載並安裝這些擱置的規則。那就是測試裝置的目的，適用於：新的裝置更新規則會自動套用至測試裝置，讓系統管理員有機會確認韌體更新是否如預期般運作。若是如此，這些系統管理員就可以將規則標示為核准；之後，組織中所有相關的裝置就會下載並安裝核准的規則。

測試裝置可以指派給全域範圍或網站範圍。您可以使用 **Get-CsTestDevice** Cmdlet 擷取設定為目前要在組織內使用之測試裝置的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsTestDevice** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTestDevice"}

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
<td><p>可您在指定要傳回之測試裝置時使用萬用字元。例如，若要傳回已在網站範圍設定的所有測試裝置集合，請使用下列語法：-Filter &quot;site:*&quot;。若要傳回 Identity 中有 &quot;EMEA&quot; 一詞的所有裝置，請使用下列語法：-Filter &quot;*EMEA*&quot;。請注意，Filter 只能在測試裝置集合的 Identity 上有作用；您無法針對其他集合屬性進行篩選。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示要傳回之測試裝置的 Identity。若要參考名稱為 UCPhone 的個別裝置 (儲存於全域集合中)，請使用下列語法：-Identity global/UCPhone。若要參考在網站集合中找到的裝置，請使用類似下列的語法：-Identity site:Redmond/UCPhone。若要參考整個集合，請省略裝置名稱。例如，下列語法會傳回針對 Redmond 網站設定的所有測試裝置：-Identity site:Redmond。</p>
<p>請注意，如有指定 Identity，即無法使用萬用字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取測試裝置資料，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsTestDevice** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsTestDevice** Cmdlet 傳回 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.TestDevice 物件的一或多個執行個體。

## 請參閱

#### 其他資源

[New-CsTestDevice](new-cstestdevice.md)  
[Remove-CsTestDevice](remove-cstestdevice.md)  
[Set-CsTestDevice](set-cstestdevice.md)

