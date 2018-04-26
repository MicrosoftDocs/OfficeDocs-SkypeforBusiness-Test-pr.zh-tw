---
title: New-CsSipProxyUseDefaultCert
TOCTitle: New-CsSipProxyUseDefaultCert
ms:assetid: 387cf221-2607-4c46-abc3-f8db263a934f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425858(v=OCS.15)
ms:contentKeyID: 49290605
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyUseDefaultCert

 

_**上次修改主題的時間：** 2015-03-09_

建立對 Lync Server 所使用之預設憑證的物件參照。此物件參照可用於設定靜態路由，以使用傳輸層安全性 (TLS) 做為傳輸通訊協定。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsSipProxyUseDefaultCert

## 範例

## 範例 1

範例 1 所示的命令會建立使用 TLS 做為傳輸的新 SIP Proxy 傳輸物件。由於 TLS 需要憑證(以供驗證之用)，因此範例中的第一個命令會使用 **New-CsSipProxyUseDefaultCert** Cmdlet 設定新的 SipProxy.UseDefaultCert 物件。此物件儲存在名為 $cert 的變數中，並會指示 Lync Server 針對 TLS 傳輸使用預設憑證。在建立 UseDefaultCert 物件之後，可以呼叫 **New-CsSipProxyTLS** Cmdlet 建立新的 SipProxy.TLS 物件，此物件使用預設憑證並指向 atl-proxy-001.litwareinc.com 做為下一個躍點伺服器的完整網域名稱 (FQDN)。

只要 TLS 物件存在，該物件 (以及 TLS 通訊協定) 就可以新增至 Transport 物件 (透過呼叫 **New-CsSipProxyTransport** Cmdlet 所建立的物件)。

    $cert = New-CsSipProxyUseDefaultCert
    
    $tls = New-CsSipProxyTLS -Certificate $cert -Fqdn atl-proxy-001.litwareinc.com
    
    $transport = New-CsSipProxyTransport -TransportChoice $tls -Port 7500

## 詳細描述

當您傳送 SIP 訊息給某人，該訊息可能需要在傳遞之前周遊多個子網路和網路；訊息所經歷的路徑通常稱為路由。網路中有兩種路由類型：動態和靜態。透過動態路由，伺服器使用演算法判斷訊息應轉送的下一個位置 (下一個躍點)。透過靜態路由，訊息路徑由系統管理員預先決定。當伺服器接收到訊息，伺服器會檢查訊息位址，然後將訊息轉送至已由管理員預先決定的下一個躍點伺服器。如果設定正確，靜態路由會協助確保及時並正確地傳遞訊息，且在伺服器上只要最小限度的監聽。靜態路由的缺點是在網路故障時，無法動態地重新路由傳送訊息。

Lync Server 可讓您設定 Proxy 伺服器的靜態路由。如果您選擇使用 TLS (建議的傳輸選項)，也必須指定驗證用的憑證。您可以取得特別用在靜態路由上的憑證，或者設定 TLS 使用預設 Lync Server 憑證。如果您決定使用預設的憑證，則可執行 **New-CsSipProxyUseDefaultCert** Cmdlet 來建立該憑證的物件參照。接著 **New-CsSipProxyTLS** Cmdlet 可使用該憑證物件參照，將 TLS 設為傳輸通訊協定。

請注意，如果您使用 **New-CsStaticRoute** 建立靜態路由，則不需要 **New-CsSipProxcyUseDefaultCert** Cmdlet 。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsSipProxyUseDefaultCert** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyUseDefaultCert"}

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>此 Cmdlet 只提供一般的 Windows PowerShell 參數。</p>
<p></p></td>
<td><p></p></td>
<td> </td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **New-CsSipProxyUseDefaultCert** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsSipProxyUseDefaultCert** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.UseDefaultCert 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsSipProxyTLS](new-cssipproxytls.md)

