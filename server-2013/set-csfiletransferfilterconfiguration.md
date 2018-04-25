---
title: Set-CsFileTransferFilterConfiguration
TOCTitle: Set-CsFileTransferFilterConfiguration
ms:assetid: 2697d3a0-d920-4a1d-9adc-7a8c754d8977
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425736(v=OCS.15)
ms:contentKeyID: 49290378
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsFileTransferFilterConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改檔案傳輸篩選組態設定的集合。檔案傳輸篩選設定可用於禁止使用者使用 Lync Server 用戶端傳輸某些檔案類型 (例如副檔名為 .vbs 或 .ps1 的檔案) 。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsFileTransferFilterConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsFileTransferFilterConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Action <BlockAll | Block>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Extensions <PSListModifier>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會停用 Redmond 網站 (亦即，Identity 為 site:Redmond 的檔案傳輸篩選組態) 的檔案傳輸篩選。為達此目的，命令會加入 Enabled 參數並設為 $False。

    Set-CsFileTransferFilterConfiguration -Identity site:Redmond -Enabled $False

## 範例 2

範例 2 所示的命令會將副檔名 (.ps1，Windows PowerShell 指令碼的副檔名) 新增至 Redmond 網站禁止的副檔名清單。若要新增副檔名，**Set-CsFileTransferFilterConfiguration** Cmdlet 會使用 Extensions 參數和 Add list 修改工具。修改工具將指定的副檔名 .ps1 新增至禁止的副檔名清單。若要使用單一命令新增多個副檔名，只要以逗號分隔副檔名即可：@{Add=".ps1",".ps2",".ps3"}。請注意，指定副檔名時必須包含逗點。

    Set-CsFileTransferFilterConfiguration -Identity site:Redmond -Extensions @{Add=".ps1"}

## 範例 3

範例 3 會將 .ps1 副檔名新增到組織目前所使用之所有檔案傳輸篩選組態的 Extensions 清單。為達成此目的，會先呼叫不含任何參數的 **Get-CsFileTransferFilterConfiguration** Cmdlet，以傳回目前所使用之所有檔案傳輸篩選組態的集合。然後，此集合會管線傳送到 **Set-CsFileTransferFilterConfiguration** Cmdlet，將 .ps1 副檔名加入集合中的每一個項目。

    Get-CsFileTransferFilterConfiguration | Set-CsFileTransferFilterConfiguration -Extensions @{Add=".ps1"}

## 範例 4

範例 4 會從 Redmond 網站之檔案傳輸篩選組態所封鎖的副檔名清單中，移除副檔名 .ps1。此範例和範例 3 唯一的不同之處，在於其不會呼叫 Add list 修改程式將副檔名加入清單，而會呼叫 Remove list 修改工具從該清單中移除副檔名。

    Set-CsFileTransferFilterConfiguration -Identity site:Redmond -Extensions @{Remove=".ps1"}

## 範例 5

範例 5 執行的動作和範例 4 相同：將副檔名 .ps1從 Redmond 網站的檔案傳輸篩選副檔名清單中移除。不過在此範例中，我們先擷取 site:Redmond 的檔案傳輸篩選組態，然後將輸出指派至變數 $a。$a 現在包含 Redmond 網站的組態。接下來，我們擷取 $a 的 Extensions 屬性，即 site:Redmond 的 Extensions 屬性 ($a.Extensions)。這個屬性包含副檔名清單。Extensions 屬性後面就是移除方法的呼叫 ($a.Extensions.Remove)。我們將值 .ps1 傳遞到 Remove 方法；這會從 Extension 屬性的清單中移除副檔名。但是，這只會從變數 $a 的記憶體所儲存的組態中移除副檔名。若要變更資料庫，必須呼叫 **Set-CsFileTransferFilterConfiguration** Cmdlet，將 $a 傳遞至 Instance 參數。

    $a = Get-CsFileTransferFilterConfiguration -Identity site:Redmond
    $a.Extensions.Remove(".ps1")
    Set-CsFileTransferFilterConfiguration -Instance $a

## 詳細描述

傳送立即訊息時，使用者可以附加並傳送檔案給交談中的其他參與者。可設定 Lync Server，含有某些副檔名的檔案便不允許從用戶端傳送，通常是證實可能有害的副檔名類型。

使用者使用 Lync Server 用戶端傳輸檔案的能力，是由在全域範圍或 (選用) 網站範圍套用的檔案傳輸篩選組態設定所決定。**Set-CsFileTransferFilterConfiguration** Cmdlet 允許您修改現有的檔案傳輸篩選組態。您可以利用新增或移除副檔名或是建立新的清單，來修改副檔名清單。您也可以使用此 Cmdlet 變更是否要啟用檔案傳輸篩選及其層級 (只封鎖副檔名符合 Extensions 清單的檔案，或是封鎖全部檔案)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsFileTransferFilterConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsFileTransferFilterConfiguration"}

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
<td><p><em>Action</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileFilterAction</p></td>
<td><p>決定啟用這個檔案傳輸篩選組態時要採取的動作。如果設為 BlockAll，則不論副檔名為何，都會禁止所有檔案傳輸。如果設為 Block (預設值)，則允許檔案傳輸，除非副檔名是 Extensions 屬性所列出之禁止的檔案類型之一。</p>
<p>若要允許無限制的檔案傳輸 (也就是，允許使用者交換任何類型檔案 (不論副檔名為何)，請將此原則的 Enabled 屬性設為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>啟用或停用檔案傳輸篩選。如果此參數設為 True，則無法從用戶端傳輸含有指定副檔名的檔案 (或全部檔案，視 Action 屬性值而定)。如果此參數設為 False，則可傳輸任何檔案。</p>
<p>預設值：True。</p></td>
</tr>
<tr class="even">
<td><p><em>Extensions</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>要封鎖的副檔名清單。如果嘗試使用 Lync Server 用戶端來傳輸具有符合此清單中其中一個副檔名的檔案，則會封鎖該傳輸，而且不會傳輸該檔案。如果 Action 設為 BlockAll (封鎖所有檔案傳輸) 或 Enabled 設為 False (不封鎖任何檔案傳輸)，則會略過此清單。</p>
<p>根據預設，下列副檔名包含在 Extensions 屬性的 Default 中：.ade, .adp, .app, .asp, .bas, .bat, .cer, .chm, .cmd, .com, .cpl, .crt, .csh, .exe, .fxp, .grp, .hlp, .hta, .inf, .ins, .isp, .its, .js, .jse, .ksh, .lnk, .mad, .maf, .mag, .mam, .maq, .mar, .mas, .mat, .mau, .mav, .maw, .mda, .mdb。.mde, .mdt, .mdw, .mdz, .msc, .msi, .msp, .mst, .ocx, .ops, .pcd, .pif, .pl, .pnp, .prf, .prg, .pst, .reg, .scf, .scr, .sct, .shb, .shs, .tmp, .url, .vb, .vbe, .vbs, .vsd, .vsmacros, .vss, .vst, .vsw, .ws, .wsc。.wsf, .wsh</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要修改之檔案傳輸組態的唯一識別碼。這個值可以是 global 或 site:&lt;網站名稱&gt;，&lt;網站名稱&gt; 是要套用設定的網站之名稱，例如 site:Redmond。</p>
<p>若未指定此參數，根據預設，<strong>Set-CsFileTransferFilterConfiguration</strong> Cmdlet 會更新全域設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>FileTransferFilterConfiguration</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。此物件的類型必須是 FileTransferFilterConfiguration，並可由呼叫 <strong>Get-CsFileTransferFilterConfiguration</strong> Cmdlet 擷取。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration 物件。接受檔案傳輸篩選組態物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsFileTransferFilterConfiguration](new-csfiletransferfilterconfiguration.md)  
[Remove-CsFileTransferFilterConfiguration](remove-csfiletransferfilterconfiguration.md)  
[Get-CsFileTransferFilterConfiguration](get-csfiletransferfilterconfiguration.md)

