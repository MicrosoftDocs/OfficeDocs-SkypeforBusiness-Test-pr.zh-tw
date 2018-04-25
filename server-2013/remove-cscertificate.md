---
title: Remove-CsCertificate
TOCTitle: Remove-CsCertificate
ms:assetid: b7a83a58-9d3f-458a-867e-44466c9817dc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412895(v=OCS.15)
ms:contentKeyID: 49292104
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCertificate

 

_**上次修改主題的時間：** 2015-03-09_

移除先前標示為可供 Lync Server 使用的憑證。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsCertificate -Type <CertType[]> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Identity <XdsIdentity>] [-Previous <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除可供 Lync Server 使用的所有 WebServicesExternal 憑證。如果目前正在使用任何的這類憑證，**Remove-CsCertificate** Cmdlet 將詢問您是否確定要移除該憑證；您必須先回應該提示，命令才能完成。若要略過確認提示，請使用 Force 參數：

Remove-CsCertificate –Type WebServicesExternal -Force

    Remove-CsCertificate -Type WebServicesExternal

## 詳細描述

Lync Server 利用憑證讓伺服器與伺服器角色相互確認其身分；例如，Edge Server 會使用憑證確認與其通訊的電腦是否真的是 前端伺服器，反之亦然。若要完整實作 Lync Server，必須將適當的憑證指派給適當的伺服器角色。

**Remove-CsCertificate** Cmdlet 提供方法，讓您能夠移除 Lync Server 目前使用的憑證。**Remove-CsCertificate** Cmdlet 不會真的刪除憑證本身，而是將憑證標示為 Lync Server 無法再使用它、移除任何的憑證繫結，以及撤銷對憑證的存取權限 (假設沒有其他服務正在使用此憑證)。除此之外，這表示當您執行 **Get-CsCertificate** Cmdlet 時，此憑證將不再出現。

若要讓 Lync Server 再次使用憑證，必須使用 **Set-CsCertificate** Cmdlet，為 Lync Server 重新指派憑證。

如果您嘗試移除目前使用的憑證，**Remove-CsCertificate** Cmdlet 將詢問您是否確定要移除該憑證；在您回應該提示之前，將無法移除該憑證。若要略過此提示，且即使是目前正在使用的憑證也要以無訊息方式加以刪除，請在命令中加入 Force 參數：

Remove-CsCertificate –Type WebServicesExternal -Force

誰可以執行這個 Cmdlet：您必須是本機系統管理員和網域的成員，才能本機執行 **Remove-CsCertificate** Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCertificate"}

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
<td><p><em>Type</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>要刪除的憑證類型。憑證類型包括 (但不限於)：</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>PICWebService (僅限 Microsoft Lync Online 2010)</p>
<p>ProvisionService (僅限 Microsoft Lync Online 2010)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>例如，下列語法會刪除 Default 憑證：-Type Default。</p>
<p>您可以在單一命令中，利用逗號分隔憑證類型的方式來刪除多個類型：</p>
<p>-Type Internal,External,Default</p></td>
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
<td><p>如果您嘗試刪除目前所使用的憑證，通常會產生略過確認提示的情況。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>若設為 Global，將會從全域範圍移除憑證。若未指定，將會從本機電腦移除憑證。</p></td>
</tr>
<tr class="odd">
<td><p><em>Previous</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，將會移除先前所指派的憑證，而不會移除目前所指派的憑證。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>讓您可以記錄 <strong>Remove-CsCertificate</strong> Cmdlet 執行的程序的詳細資訊。參數值應該是要產生之 HTML 檔的完整路徑，例如：-Report C:\Logs\Certificates.html。如果指定的檔案已經存在，將使用新資訊自動覆寫該檔案。</p></td>
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

無。Remove-CsCertificate Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。反之，**Remove-CsCertificate** Cmdlet 會刪除 Microsoft.Rtc.Management.Deployment.CertificateReference 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

