---
title: Get-CsCertificate
TOCTitle: Get-CsCertificate
ms:assetid: 15b8f019-1d00-4389-9abe-18deb8cbf2ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398227(v=OCS.15)
ms:contentKeyID: 49290197
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCertificate

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定要使用 Lync Server 之本機電腦上憑證的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsCertificate [-Identity <XdsIdentity>] [-Report <String>] [-Type <CertType[]>]

## 範例

## 範例 1

範例 1 所示的命令會傳回關於目前指派給 Lync Server 元件之憑證的資訊。作法是呼叫不含任何參數的 **Get-CsCertificate** Cmdlet。

    Get-CsCertificate

## 範例 2

範例 2 會擷取用於內部 Web 服務的所有 Lync Server 憑證。為達此目的，會加入 Type 參數會與參數值 WebServicesInternal。

    Get-CsCertificate -Type WebServicesInternal

## 範例 3

範例 3 會傳回在 2012 年 9 月 1 日之前到期的所有 Lync Server 憑證。為了執行此工作，命令會先使用 **Get-CsCertificate** Cmdlet 傳回目前所使用之所有 Lync Server 憑證的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以選取在 2012 年 9 月 1 日之前到期的憑證。在此範例中，指定的日期 (9/1/2012) 是採用美國英文格式的日期時間值。請使用相容於您的 \[地區及語言選項\] 的格式指定日期。

    Get-CsCertificate | Where-Object {$_.NotAfter -lt "9/1/2012"}

## 範例 4

範例 4 會傳回有關憑證授權單位 (CA) MyCa 發行之所有 Lync Server 憑證的資訊。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsCertificate** Cmdlet，以傳回目前所使用之所有憑證的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 Issuer 屬性等於 (-eq) "Cn=MyCa" 的所有憑證。

    Get-CsCertificate | Where-Object {$_.Issuer -eq "Cn=MyCa"}

## 範例 5

範例 5 所示的命令會傳回 Subject 屬性已設為 CN=atl-cs-001.litwareinc.com 的所有 Lync Server 憑證。作法是使用 **Get-CsCertificate** Cmdlet 傳回所有 Lync Server 憑證的集合，然後，此集合會管線傳送到 **Where-Object** Cmdlet。接著 **Where-Object** Cmdlet 會只選取 Subject 屬性等於 "CN=atl-cs-001.litwareinc.com" 的憑證。

    Get-CsCertificate | Where-Object {$_.Subject -eq "CN=atl-cs-001.litwareinc.com"}

## 詳細描述

Lync Server 使用憑證做為一種讓伺服器和伺服器角色確認其身分的方法；例如，Edge Server 會使用憑證確認與其通訊的電腦是否真的是 前端伺服器，反之亦然。若要完整實作 Lync Server，您必須將適當的憑證指派給適當的伺服器角色。

**Get-CsCertificate** Cmdlet 可讓您擷取設定要搭配 Lync Server 使用之憑證的詳細資訊。請注意，此 Cmdlet 只會傳回有關 Lync Server 憑證的資訊。如果憑證未設定為用於 Lync Server (使用 **Set-CsCertificate** Cmdlet)，則當您執行 **Get-CsCertificate** Cmdlet 時，不會傳回該憑證。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsCertificate** Cmdlet：RTCUniversalServerAdmins。

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
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>可讓您擷取在全域範圍設定的憑證 (會複製全域憑證，並將其散發到相關的電腦)。若要傳回全域憑證的資訊，請使用下列語法：</p>
<p>Get-CsCertificate –Identity &quot;global&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您記錄由 <strong>Get-CsCertificate</strong> Cmdlet 執行之程序的詳細資訊。此參數值應該是將產生之 HTML 檔案的完整路徑；例如：-Report C:\Logs\Certificates.html。如果指定的檔案已經存在，將會自動以新資訊覆寫該檔案。</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>要求的憑證類型。憑證類型包含 (但不限於) 下列類型：</p>
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
<p>例如，此語法會傳回 Default 憑證的資訊：-Type Default。</p>
<p>您可以在單一命令中以逗號隔開憑證類型，以指定多種類型：</p>
<p>-Type Internal,External,Default</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsCertificate** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsCertificate** Cmdlet 會傳回 Microsoft.Rtc.Management.Deployment.CertificateReference 物件的執行個體。

## 請參閱

#### 其他資源

[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

