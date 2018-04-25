---
title: New-CsConferenceDirectory
TOCTitle: New-CsConferenceDirectory
ms:assetid: fd5a4369-10cd-4337-94df-51bcaee4fde9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413080(v=OCS.15)
ms:contentKeyID: 49292913
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsConferenceDirectory

 

_**上次修改主題的時間：** 2015-03-09_

建立新的會議目錄供組織使用。會議目錄可用於協助電話撥入式會議使用者尋找會議資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsConferenceDirectory -HomePool <String> -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

建立新的會議目錄 (Identity 為 42)。此目錄將裝載於集區 atl-cs-001.litwareinc.com 上。

    New-CsConferenceDirectory -Identity 42 -HomePool "atl-cs-001.litwareinc.com"

## 詳細描述

建立電話撥入式會議統一資源識別元 (URI) 時，會為這些 URI 指派唯一的 SIP 位址。但對於無法識別 SIP 的裝置而言，將 SIP 位址轉譯成裝置並非易事。例如公用交換電話網路 (PSTN) 電話便無法轉譯 SIP 位址。有鑑於此，Lync Server 會使用會議目錄協助這些裝置尋找、連線及撥入會議。作法是建立 SIP 會議目錄，並將其關聯到每個電話撥入會議 URI，然後為其指定整數值 (而非 SIP URI) 做為識別，讓 PSTN 電話和其他裝置連線到會議時，可以使用這些號碼 (非 SIP URI)。目錄號碼包含在使用者連線到電話撥入式會議時所輸入的 PSTN 會議識別中。

您可以呼叫 **New-CsConferenceDirectory** Cmdlet 來建立新的會議目錄。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsConferenceDirectory** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsConferenceDirectory"}

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
<td><p><em>HomePool</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要主控新會議目錄之登錄器集區的完整網域名稱 (FQDN)。例如：-Identity atl-cs-001.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>新會議目錄的唯一數字識別碼。識別碼可以是任何介於 0 和 9999 (含) 之間的整數值；但是，Identity 必須是唯一的 (例如，您不能擁有兩個 Identity 為 575 的目錄)。當您建立新目錄時，不需要依照任何數字順序。例如，您可以建立 Identity 為 999 的目錄，再來建立 Identity 為 2 的目錄，之後則是 Identity 為 438 的目錄，依此類推。</p></td>
</tr>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsConferenceDirectory** Cmdlet 不會接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

