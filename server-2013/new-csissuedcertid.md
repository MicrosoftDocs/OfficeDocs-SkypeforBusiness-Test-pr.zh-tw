---
title: New-CsIssuedCertId
TOCTitle: New-CsIssuedCertId
ms:assetid: 3158e26e-3fda-488b-a08d-5481e1abfc1d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425814(v=OCS.15)
ms:contentKeyID: 49290506
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsIssuedCertId

 

_**上次修改主題的時間：** 2015-03-09_

可讓您指派現有的憑證給 SipProxy.TLS 物件。該物件可用於設定靜態路由，以使用傳輸層安全性 (TLS) 做為傳輸通訊協定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsIssuedCertId -Issuer <String> -SerialNumber <Byte[]>

## 範例

## 範例 1

範例 1 所示的命令會建立新的憑證 ID 物件，並將該憑證指派給 SipProxy.TLS 物件。於是該物件便可用來設定靜態路由，使其使用 TLS 傳輸通訊協定。為達此目的，範例中的第一個命令使用 **New-CsIssuedCertId** 來為 Fabrikam 發行的憑證 (序號為 10143A1A) 建立憑證 ID 物件 (請注意，序號已指定為一排雙字元值的字串)。產生的物件會儲存在名為 $cert 的變數中。

在第二個命令中會使用 New-CsSipProxyTLS 建立 SIPProxy.TLS 物件。為確保此物件會使用 Fabrikam 發行的憑證進行驗證，命令中使用變數 $cert 做為 Certificate 參數的參數值。

    $cert = New-CsIssuedCertId -Issuer "Fabrikam" -SerialNumber 0x10,0x14,0x3A,0x1A
    
    $tls = New-CsSipProxyTLS -Certificate $cert -Fqdn atl-proxy-001.litwareinc.com

## 詳細描述

當您傳送工作階段初始通訊協定 (SIP) 訊息給某人時，該訊息可能需要在傳遞之前周遊多個子網路和網路。訊息所經歷的路徑通常稱為路由。網路中有兩種路由類型：動態和靜態。透過動態路由，伺服器使用演算法判斷訊息應轉送的下一個位置 (下一個躍點)。透過靜態路由，訊息路徑由系統管理員預先決定。當伺服器接收到訊息，伺服器會檢查訊息位址，然後將訊息轉送至已由管理員預先決定的下一個躍點伺服器。如果設定正確，靜態路由會協助確保及時並正確地傳遞訊息，且在伺服器上只要最小限度的監聽。靜態路由的缺點在於當網路失敗時，無法再次動態地傳送訊息。

設定靜態路由時，Lync Server 可讓您指定傳輸控制通訊協定 (TCP) 或傳輸層安全性 (TLS) 做為傳輸通訊協定。如果您決定使用 TLS 做為您的通訊協定，必須先指派用於驗證的憑證。在此狀況下，您可以使用為 Lync Server 設定的預設憑證。或者，可透過呼叫 **New-CsIssuedCertID** 來指派 TLS 憑證以建立憑證物件，再將該物件指派給 SipProxy。TLS 物件是使用 **New-CsSipProxyTLS** Cmdlet 所建立。

當您執行 **New-CsIssuedCertID** 時，必須提供該 Cmdlet 和現有憑證的發行者名稱與序號。如需該資訊，可執行此命令取得：

Get-CsCertificate | Select-Object Issuer, SerialNumber

請注意，序號必須以位元組陣列的方式傳遞。也就是說，您必須以一排雙字元值的形式來傳遞序號。此外，每個雙字元值的開頭必須為 0x。例如，假設您的憑證序號為 1E225D3ZF66。該資料必須使用下列語法來加以傳遞：

\-SerialNumber 0x1E,0x22,0x5D,0x3F,0x66

如果您使用 **New-CsStaticRoute** Cmdlet 建立靜態路由，則不必使用 **New-CsIssuedCertId** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsIssuedCertId** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsIssuedCertId"}

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
<td><p><em>Issuer</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>發行靜態路由中使用之憑證的憑證授權單位 (CA) 名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>SerialNumber</em></p></td>
<td><p>必要</p></td>
<td><p>System.Byte[]</p></td>
<td><p>靜態路由所用憑證的序號。序號必須以位元組陣列的方式傳遞。也就是說，您必須以一排雙字元值的形式來傳遞序號，且每個雙字元值的開頭必須為 0x。例如：-SerialNumber 0x01, 0x23, 0x45, 0x67, 0x89。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsIssuedCertId** 不接受管線傳送的輸入。

## 傳回類型

**New-CsIssuedCertId** 會建立 Microsoft.Rtc.Management.WritableConfig.BaseTypes.IssuedCertId 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsSipProxyTLS](new-cssipproxytls.md)

