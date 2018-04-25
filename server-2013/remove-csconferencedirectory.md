---
title: Remove-CsConferenceDirectory
TOCTitle: Remove-CsConferenceDirectory
ms:assetid: c2c62a14-f3f3-472f-bf91-1fcea9e45425
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412961(v=OCS.15)
ms:contentKeyID: 49292222
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferenceDirectory

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的會議目錄。會議目錄可用於協助電話撥入式會議使用者尋找會議資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsConferenceDirectory -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除具有 Identity 2 的會議目錄。

    Remove-CsConferenceDirectory -Identity 2

## 範例 2

範例 2 會刪除在 UserServer:atl-cs-001.litwareinc.com 服務上找到的所有會議目錄。為達成此目的，命令會先不呼叫含任何參數的 **Get-CsConferenceDirectory** Cmdlet，以傳回組織目前使用之所有會議目錄的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出位於 UserServer:atl-cs-001.litwareinc.com 服務上的目錄。接著將該篩選後的集合管線傳送到 **Remove-CsConferenceDirectory** Cmdlet 加以刪除。

    Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "UserServer:atl-cs-001.litwareinc.com"} | Remove-CsConferenceDirectory

## 詳細描述

建立電話撥入式會議統一資源識別元 (URI) 時，會為這些 URI 指派唯一的 SIP 位址。但對於無法識別 SIP 的裝置而言，將 SIP 位址轉譯成裝置並非易事。例如公用交換電話網路 (PSTN) 電話便無法轉譯 SIP 位址。有鑑於此，Lync Server 會使用會議目錄協助這些裝置尋找、連線及撥入會議。作法是建立 SIP 會議目錄，並將其關聯到每個電話撥入會議 URI，然後為其指定整數值 (而非 SIP URI) 做為識別，讓 PSTN 電話和其他裝置連線到會議時，可以使用這些號碼 (非 SIP URI)。目錄號碼包含在使用者連線到電話撥入式會議時所輸入的 PSTN 會議識別中。

您可以使用 **New-CsConferenceDirectory** Cmdlet 來建立會議目錄。您偶爾可能需要刪除一或多個這類目錄。例如，可能需要淘汰主控這些目錄的集區。您可以使用 **Remove-CsConferenceDirectory** Cmdlet 來移除會議目錄。請注意，如果您必須將某個集區中的目錄移動到另一個集區，則只要呼叫 **Move-CsConferenceDirectory** Cmdlet 即可。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsConferenceDirectory** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferenceDirectory"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要移除之會議目錄的數字身分識別。</p></td>
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
<td><p>如果指定此參數，即便目前無法使用主控會議目錄的集區，也能移除該目錄。根據預設，如果無法和對應的集區連絡，<strong>Remove-CsConferenceDirectory</strong> Cmdlet 將不會移除目錄。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories 物件。**Remove-CsConferenceDirectory** Cmdlet 接受會議目錄物件管線傳送的輸入。

## 傳回類型

無。反之，**Removes-CsConferenceDirectory** Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)

