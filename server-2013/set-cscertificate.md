---
title: Set-CsCertificate
TOCTitle: Set-CsCertificate
ms:assetid: 6da0be05-b257-4258-9d6d-7ddf283f1038
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398518(v=OCS.15)
ms:contentKeyID: 49291254
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCertificate

 

_**上次修改主題的時間：** 2015-03-09_

可讓您指派憑證給 Lync Server 伺服器或伺服器角色。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsCertificate -Reference <CertificateReference> -Type <CertType[]> [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCertificate -Identity <XdsIdentity> -Path <String> -Type <CertType[]> [-Password <String>] <COMMON PARAMETERS>

    Set-CsCertificate -Thumbprint <String> -Type <CertType[]> [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EffectiveDate <DateTime>] [-Force <SwitchParameter>] [-Report <String>] [-Roll <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 Thumbprint 為 B142918E463981A76503828BB1278391B716280987B 的憑證指派給本機電腦上的 WebServicesExternal 角色。

    Set-CsCertificate -Type WebServicesExternal -Thumbprint "B142918E463981A76503828BB1278391B716280987B"

## 範例 2

範例 2 會將 Thumbprint 為 B142918E463981A76503828BB1278391B716280987B 的憑證指派給本機電腦上三個不同的角色：Default、WebServicesInternal 以及 WebServicesExternal。

    Set-CsCertificate -Type Default, WebServicesInternal, WebServicesExternal -Thumbprint "B142918E463981A76503828BB1278391B716280987B"

## 詳細描述

Lync Server 利用憑證讓伺服器與伺服器角色相互確認其身分；例如，Edge Server 會使用憑證確認與其通訊的電腦是否真的是 前端伺服器，反之亦然。若要完整實作 Lync Server，必須將適當的憑證指派給適當的伺服器角色。

**Set-CsCertificate** Cmdlet 可讓系統管理員將憑證指派給伺服器或伺服器角色。請注意，您只能指派已設定為搭配 Lync Server 使用的憑證。若要識別可用於指派的憑證，請使用 **Get-CsCertificate** Cmdlet。

誰可以執行這個 Cmdlet：您必須是本機系統管理員，才能在本機執行 **Set-CsCertificate** Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCertificate"}

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
<td><p>此參數設為 Global 時，可讓憑證在全域範圍作用。Global 憑證會自動複製並散佈至適當的電腦。</p></td>
</tr>
<tr class="even">
<td><p><em>Path</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>.PFX 憑證檔案的完整路徑。</p></td>
</tr>
<tr class="odd">
<td><p><em>Reference</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertificateReference</p></td>
<td><p>設定為搭配 Lync Server 使用之憑證的物件參考。下列命令會傳回代表指紋為 B142918E463981A76503828BB1278391B716280987B 之憑證的物件參照 (變數 $x)：</p>
<p>$x = Get-CsCertificate | Where-Object {$_.Thumbprint –eq &quot;B142918E463981A76503828BB1278391B716280987B&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Thumbprint</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>憑證的唯一識別碼。憑證指紋外觀類似如下：B142918E463981A76503828BB1278391B716280987B。</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>指派的憑證類型。憑證類型包含 (但不限於) 下列類型：</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>iPhoneAPNService</p>
<p>iPadAPNService</p>
<p>MPNService</p>
<p>PICWebService (僅限 Microsoft Lync Online 2010)</p>
<p>ProvisionService (僅限 Microsoft Lync Online 2010)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>例如，此語法會指派 Default 認證：-Type Default。</p>
<p>您可以在單一命令中以逗號隔開憑證類型，以指定多種類型：</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EffectiveDate</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>憑證可供第一次使用的日期和時間。例如，若要將憑證設為在 2012 年 7 月 31 日早上 8:00 第一次使用，請在以美國英文 [地區及語言] 設定執行的伺服器上，使用下列語法：</p>
<p>-EffectiveTime &quot;7/31/2012 8:00 AM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>抑制顯示執行命令時可能引起的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Password</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>憑證的密碼。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您記錄關於由 <strong>Set-CsCertificate</strong> Cmdlet 執行之程序的詳細資訊。此參數值應該是要產生之 HTML 檔案的完整路徑；例如：-Report C:\Logs\Certificates.html。如果指定的檔案已經存在，將會自動以新資訊覆寫該檔案。</p></td>
</tr>
<tr class="odd">
<td><p><em>Roll</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您在 EffectiveDate 參數指定的日期和時間，更新指定的憑證；這可讓您指定新憑證成為主要憑證的日期和時間。請注意，如果指定 Roll 參數時，未包含 EffectiveDate 參數，命令將會失敗。</p></td>
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

Microsoft.Rtc.Management.Deployment.CertificateReference。

## 傳回類型

**Set-CsCertificate** Cmdlet 不會傳回任何值或物件，

## 請參閱

#### 其他資源

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)

