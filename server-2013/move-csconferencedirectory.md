---
title: Move-CsConferenceDirectory
TOCTitle: Move-CsConferenceDirectory
ms:assetid: c43207fa-06dd-4360-ae32-b2f17f7100d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412968(v=OCS.15)
ms:contentKeyID: 49292237
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsConferenceDirectory

 

_**上次修改主題的時間：** 2015-05-28_

在集區之間移動現有的會議目錄。會議目錄可用於協助電話撥入式會議使用者尋找會議資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Move-CsConferenceDirectory -Identity <XdsGlobalRelativeIdentity> -TargetPool <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令可將身分識別為 Identity 3 的會議目錄移至 atl-cs-002.litwareinc.com 集區。

    Move-CsConferenceDirectory -Identity 3 -TargetPool atl-cs-002.litwareinc.com

## 範例 2

雖然範例 2 所示的命令是範例 1 所示命令的變化，不過在這種情況下加入 Force 參數可確保在目標集區目前無法使用時，移動作業仍順利進行。

    Move-CsConferenceDirectory -Identity 3 -TargetPool atl-cs-002.litwareinc.com -Force

## 範例 3

範例 3 會將所有現有的會議目錄移至 atl-cs-002.litwareinc.com 目標集區。為了執行此工作，命令會先使用 **Get-CsConferenceDirectory** Cmdlet，以傳回組織目前使用的所有會議目錄集合。然後，此集合會管線傳送到 **Move-CsConferenceDirectory** Cmdlet，以將集合中的每一個目錄移至目標集區。

    Get-CsConferenceDirectory | Move-CsConferenceDirectory -TargetPool atl-cs-002.litwareinc.com 

## 詳細描述

建立電話撥入式會議統一資源識別元 (URI) 時，會指派唯一 SIP 位址給這些 URI。然而，對於無法識別 SIP 的裝置來說，SIP 位址是難以轉譯的位址；例如，公用交換電話網路 (PSTN) 電話無法轉譯 SIP 位址。有鑑於此，Lync Server 便會使用會議目錄來做為協助這些裝置尋找、連接及撥入會議的方法。這項作業的操作方法為建立和每個電話撥入式會議 URI 相關的 SIP 會議目錄，然後再利用整數值 (而非 SIP URI) 來加以識別。然後，當 PSTN 電話和其他裝置連線到會議時，可以使用這些號碼來取代 SIP URI；目錄號碼包含在使用者連線到電話撥入式會議時輸入的 PSTN 會議識別中。

您偶爾可能需要將某個集區中的現有會議目錄移至另一個集區；例如，由於淘汰某個集區，因此需要將現有的會議目錄移至新位置。**Move-CsConferenceDirectory** Cmdlet 可讓您將會議目錄移至其他集區。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Move-CsConferenceDirectory** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsConferenceDirectory"}

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
<td><p>要移動之會議目錄的數字身分識別。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPool</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要移動之會議目錄所在集區的完整網域名稱 (FQDN)。例如：-Identity atl-cs-002.litwareinc.com。</p></td>
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
<td><p>如果指定此參數，即便目前無法使用目標集區，也能移動會議目錄。根據預設，如果無法和目標集區連絡，<strong>Move-CsConferenceDirectory</strong> Cmdlet 將不會移動目錄。</p>
<p>執行 <strong>Move-CsConferenceDirectory</strong> Cmdlet 搭配 Force 參數之前，應先使用 Dbimpexp.exe 手動匯出舊資料，然後將此資料匯入目標登錄器集區。Dbimpexp.exe 可以在 Lync Server 安裝媒體的根資料夾中找到。</p></td>
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

無。**Move-CsConferenceDirectory** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

