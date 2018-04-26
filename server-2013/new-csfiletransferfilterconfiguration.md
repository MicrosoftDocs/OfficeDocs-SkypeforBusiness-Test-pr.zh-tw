---
title: New-CsFileTransferFilterConfiguration
TOCTitle: New-CsFileTransferFilterConfiguration
ms:assetid: 3d1050fb-5df9-4186-94b9-8ef8a9103958
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425897(v=OCS.15)
ms:contentKeyID: 49290668
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsFileTransferFilterConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的檔案傳輸篩選組態。檔案傳輸篩選設定可用於禁止使用者使用 Lync Server 用戶端傳輸某些檔案類型 (例如副檔名為 .vbs 或 .ps1 的檔案)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsFileTransferFilterConfiguration -Identity <XdsIdentity> [-Action <BlockAll | Block>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Extensions <PSListModifier>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會使用 **New-CsFileTransferFilterConfiguration** Cmdlet 建立 Identity 為 site:Redmond 的新立即訊息檔案傳輸篩選組態。由於未指定其他參數，因此會使用預設值建立組態。

    New-CsFileTransferFilterConfiguration -Identity site:Redmond

## 範例 2

在此命令中，**New-CsFileTransferFilterConfiguration** Cmdlet 用來建立 Identity 為 site:Redmond 的新檔案傳輸篩選組態。由於已指定 Extensions 參數，因此新的組態將會包含所有預設值，並加上額外的副檔名：.ps1。這個新副檔名是使用 Extensions 參數新增的，而清單修飾詞 Add 會緊接在要新增的副檔名之後 (請注意，您必須加入句號做為副檔名的一部分)。若要新增多個副檔名，只要使用逗號分隔副檔名即可：@{Add=".ps1",".ps2",".ps3"}

    New-CsFileTransferFilterConfiguration -Identity site:Redmond -Extensions @{Add=".ps1"}

## 範例 3

在範例 3 中，**New-CsFileTransferFilterConfiguration** Cmdlet 用來建立 Identity 為 site:Redmond 的新檔案傳輸篩選組態。此範例類似於範例 2，但是使用的是 Replace 清單修飾詞，而非 Add 修飾詞。這表示完整的副檔名集將會以兩個指定的副檔名取代：.vbs 與 .ps1。在此例中，在 Redmond 網站封鎖的唯一檔案將是 .vbs 與 .ps1。

    New-CsFileTransferFilterConfiguration -Identity site:Redmond -Extensions @{Replace=".vbs",".ps1"}

## 範例 4

範例 4 會示範如何使用 InMemory 參數建立最初僅位於記憶體中的檔案傳輸篩選組態。為此，範例中的第一個命令會使用 **New-CsFileTransferFilterConfiguration** Cmdlet 搭配 InMemory 參數，以建立 Identity 為 site:Redmond 的新檔案傳輸篩選組態。此時，新設定僅存在於記憶體中；Redmond 網站中的使用者仍將由全域檔案傳輸篩選設定來管理。

在第二個命令中，此記憶體中執行個體的 Action 屬性值會設為 BlockAll。最後，範例中的第三個命令會使用 **Set-CsFileTransferFilterConfiguration** Cmdlet 建立新設定集合，並將它們套用至 Redmond 網站。

請注意，採用下列命令可以在單一步驟完成相同的工作：

    New-CsFileTransferFilterConfiguration -Identity site:Redmond -Action "BlockAll"
    $x = New-CsFileTransferFilterConfiguration -Identity site:Redmond -InMemory 
    $x.Action = "BlockAll"
    Set-CsFileTransferFilterConfiguration -Instance $x

## 詳細描述

傳送立即訊息時，使用者可以在交談中附加及傳送檔案給其他參與者。Lync Server 可加以設定，如此便不允許使用 Lync Server 用戶端來傳送含特定副檔名的檔案 (特別是可能證明有害之檔案類型的副檔名)。

安裝 Lync Server 時，系統會為您建立單一檔案傳輸篩選組態 (在全域範圍內設定)。根據預設，全域設定會套用至組織中的所有使用者。此外，您可以使用 **New-CsFileTransferFilterConfiguration** Cmdlet，為個別網站建立自訂的檔案傳輸篩選組態。如果指定的網站已有組態，則那些檔案傳輸設定將會套用至該網站中的所有使用者。如果網站不存在這類集合，則會改為套用全域設定。

請注意，您無法在全域範圍建立新的檔案傳輸篩選組態；不過，可以使用 **Set-CsFileTransferFilterConfiguration** Cmdlet 修改全域設定。同樣地，您無法為已經定義組態的網站建立新的組態；如果嘗試這麼做，則命令會失敗。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsFileTransferFilterConfiguration** Cmdlet：RTCUniversalServerAdministrator。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsFileTransferFilterConfiguration"}

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
<td><p>要提供給檔案傳輸篩選組態的唯一識別碼。新組態的 Identity 即為首碼 &quot;site:&quot;後面緊接著網站名稱。例如，若要建立 Redmond 網站的新組態，應該使用下列語法：-Identity site:Redmond。</p></td>
</tr>
<tr class="even">
<td><p><em>Action</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileFilterAction</p></td>
<td><p>決定已啟用檔案傳輸篩選時所要採取的動作。如果設為 BlockAll，則不論副檔名為何，都會禁止所有檔案傳輸。如果設為 Block (預設值)，除非副檔名顯示為在 Extensions 屬性中所列的其中一個禁止檔案類型，否則會允許檔案傳輸。</p>
<p>若要允許無限制的檔案傳輸 (也就是，允許使用者交換任何類型檔案 (不論副檔名為何)，請將此原則的 Enabled 屬性設為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>啟用或停用檔案傳輸篩選。如果此參數設為 True，則無法使用 Lync Server 用戶端傳輸具有指定副檔名的檔案 (或所有檔案，視 Action 屬性的值而定)。如果此參數設為 False，則可以傳輸任何檔案。</p>
<p>預設值：True。</p></td>
</tr>
<tr class="odd">
<td><p><em>Extensions</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>將會封鎖的副檔名清單。如果嘗試使用 Lync Server 用戶端來傳輸具有符合此清單中其中一個副檔名的檔案，則會封鎖該傳輸，而且不會傳輸該檔案。如果 Action 設為 BlockAll (封鎖所有檔案傳輸)，或者 Enabled 設為 False (不封鎖任何檔案傳輸)，則會忽略此清單。</p>
<p>根據預設，下列副檔名會包含在 Extensions 屬性中：.ade, .adp, .app, .asp, .bas, .bat, .cer, .chm, .cmd, .com, .cpl, .crt, .csh, .exe, .fxp, .grp, .hlp, .hta, .inf, .ins, .isp, .its, .js, .jse, .ksh, .lnk, .mad, .maf, .mag, .mam, .maq, .mar.、mas., .mat, .mau, .mav, .maw, .mda, .mdb。.mde, .mdt, .mdw, .mdz, .msc, .msi, .msp, .mst, .ocx, .ops, .pcd, .pif, .pl, .pnp, .prf, .prg, .pst, .reg, .scf, .scr, .sct, .shb, .shs, .tmp, .url, .vb, .vbe, .vbs, .vsd, .vsmacros, .vss, .vst, .vsw, .ws, .wsc。.wsf, .wsh</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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

無。

## 傳回類型

**New-CsFileTransferFilterConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration 物件的新執行個體。

## 請參閱

#### 其他資源

[Remove-CsFileTransferFilterConfiguration](remove-csfiletransferfilterconfiguration.md)  
[Set-CsFileTransferFilterConfiguration](set-csfiletransferfilterconfiguration.md)  
[Get-CsFileTransferFilterConfiguration](get-csfiletransferfilterconfiguration.md)

