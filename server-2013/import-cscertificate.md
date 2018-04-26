---
title: Import-CsCertificate
TOCTitle: Import-CsCertificate
ms:assetid: 87bdafce-f4b9-4c44-ad8f-86c2deb680a4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398688(v=OCS.15)
ms:contentKeyID: 49291568
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsCertificate

 

_**上次修改主題的時間：** 2015-03-09_

匯入要在 Lync Server 中使用的憑證。若未使用 **Request-CsCertificate** Cmdlet 取得憑證，必須先匯入該憑證，才可將其指派給 Lync Server 伺服器角色。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Import-CsCertificate -Identity <XdsIdentity> -Type <CertType[]> <COMMON PARAMETERS>

    Import-CsCertificate [-PrivateKeyExportable <$true | $false>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Path <String> [-Confirm [<SwitchParameter>]] [-EffectiveDate <DateTime>] [-Force <SwitchParameter>] [-Password <String>] [-Report <String>] [-Roll <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會匯入憑證 C:\\Certificates\\WebServer.pfx。命令完成後，該憑證便可供指派給伺服器角色。

    Import-CsCertificate -Path "C:\Certificates\WebServer.pfx" -PrivateKeyExportable $True

## 詳細描述

Lync Server 使用憑證做為一種讓伺服器和伺服器角色確認其身分的方法；例如，Edge Server 會使用憑證確認與其通訊的電腦是否真的是前端伺服器，反之亦然。為了完整實作 Lync Server，您需要對適當的伺服器角色指派適當的憑證。

若要將憑證指派給 Lync Server 角色，必須先讓 Lync Server 知道有這些憑證。**Request-CsCertificate** Cmdlet 可讓您提出線上和離線的新憑證要求。如果提出線上要求，系統會自動下載憑證，並將其儲存在本機憑證存放區中；同樣重要的還有，Lync Server 立即就能使用該憑證。如果提出離線要求，系統會將憑證傳送給您。此時，您可以使用 **Import-CsCertificate** Cmdlet 匯入憑證，這是一個讓憑證可供指派給 Lync Server 伺服器角色的程序。

誰可以執行這個 Cmdlet：您必須是本機系統管理員才能在本機執行 **Import-CsCertificate** Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsCertificate"}

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
<td><p>要匯入之憑證檔案的完整路徑。例如：–Path &quot;C:\Certificates\WebServer.cer&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>要求的憑證類型。憑證類型包含 (但不限於) 下列類型：</p>
<p>* AccessEdgeExternal</p>
<p>* AudioVideoAuthentication</p>
<p>* DataEdgeExternal</p>
<p>* Default</p>
<p>* External</p>
<p>* Internal</p>
<p>* iPadAPNService</p>
<p></p>
<p>* iPhoneAPNService</p>
<p>* LogRetentionService</p>
<p>* MPNService</p>
<p>* OAuthTokenIssuer</p>
<p>* PICWebService</p>
<p>* ProvisionService</p>
<p>* SMPDNSWebService</p>
<p>* TenantAdmin</p>
<p>* UpgradeEngineService</p>
<p>* WebServicesExternal</p>
<p>* WebServicesInternal</p>
<p>* WsFedTokenTransfer</p>
<p>* XMPPServer</p></td>
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
<td><p>憑證開放使用的日期與時間。例如，若要將憑證設定在 2012 年 7 月 31 日上午 8:00 開放使用，請在區域及語言設定為美國英文的伺服器上使用下列語法：</p>
<p>-EffectiveTime &quot;7/31/2012 8:00 AM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Password</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>與憑證檔案相關聯的密碼。</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateKeyExportable</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，請確認網路服務帳戶可以讀取憑證的私密金鑰部分。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\Certificates.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Roll</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您在 EffectiveDate 參數所指定的日期與時間更新指定的憑證。這可讓您指定新憑證轉變為主要憑證的日期與時間。請注意，若只指定 Roll 參數而未加入 EffectiveDate 參數，此命令將會失敗。</p></td>
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

無。**Import-CsCertificate** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Get-CsCertificate](get-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

