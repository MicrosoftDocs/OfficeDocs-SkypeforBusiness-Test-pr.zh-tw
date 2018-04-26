---
title: New-CsSipProxyTLS
TOCTitle: New-CsSipProxyTLS
ms:assetid: 7e04f7bb-c33f-49b4-9306-082b14d2a854
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398629(v=OCS.15)
ms:contentKeyID: 49291446
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyTLS

 

_**上次修改主題的時間：** 2015-03-09_

建立新的 SipProxy.TLS 物件。此物件可設定靜態路由使用傳輸層安全性 (TLS) 做為其傳輸通訊協定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsSipProxyTLS -Certificate <ITLSTLSChoice> -Fqdn <String>

## 範例

## 範例 1

範例 1 所示的命令會建立使用 TLS 做為其傳輸的新 SIP Proxy 傳輸物件。由於 TLS 需要憑證以供驗證之用，因此範例中的第一個命令會使用 **New-CsSipProxyUseDefaultCert** Cmdlet 設定新的 SipProxy.UseDefaultCert。此儲存在名為 $cert 變數的物件會指示 Lync Server 針對 TLS 傳輸使用預設憑證。在建立 UseDefaultCert 物件之後，可以呼叫 **New-CsSipProxyTLS** Cmdlet 以建立新的 SipProxy.TLS 物件；此物件使用預設憑證並指向 atl-proxy-001.litwareinc.com 做為下一個躍點伺服器的 FQDN。

只要 TLS 物件存在，該物件 (以及 TLS 通訊協定) 就可以新增至 Transport 物件 (透過呼叫 **New-CsSipProxyTransport** Cmdlet 所建立的物件)。

    $cert = New-CsSipProxyUseDefaultCert
    
    $tls = New-CsSipProxyTLS -Certificate $cert -Fqdn atl-proxy-001.litwareinc.com
    
    $transport = New-CsSipProxyTransport -TransportChoice $tls -Port 7500

## 詳細描述

當您傳送 SIP 訊息給某人，該訊息可能需要在傳遞之前周遊多個子網路和網路；訊息所經歷的路徑通常稱為路由。在網路中，有兩種路由類型：動態及靜態。使用動態路由時，伺服器會使用演算法來決定應該將訊息轉送到的下一個位置 (下一個躍點)。使用靜態路由時，訊息路徑是由系統管理員預先決定的。當伺服器收到訊息時，該伺服器會檢查訊息位址，然後將該訊息轉送到系統管理員預先設定的下一個躍點伺服器。如果設定正確，靜態路由有助於確保訊息即時且準確送達，而且可將伺服器竊聽減到最少。靜態路由的缺點是在網路故障時，無法動態地重新路由傳送訊息。

Lync Server 可讓您設定 Proxy 伺服器的靜態路由。這些路由包含兩個主要部分：Proxy 組態設定和 SIP Proxy 路由。因此，SIP Proxy 路由具有數個屬性；例如，每個路由都必須有一個 Transport，也就是定義沿路由傳輸訊息時使用之網路通訊協定的屬性。

Lync Server 可讓您將傳輸控制通訊協定 (TCP) 或傳輸層安全性 (TLS) 指定為您的傳輸通訊協定。如果您決定使用 TLS 做為通訊協定，則必須先使用 **New-CsSipProxyTLS** Cmdlet 建立 TLS 物件。然後，您可以使用該物件指定 **New-CsSipProxyTransport** Cmdlet 所建立之 Transport 物件的通訊協定。

請注意，如果您選擇使用 TLS 做為傳輸通訊協定，也必須指定憑證 (供驗證之用)。

如果使用 **New-CsStaticRoute** Cmdlet 建立靜態路由，則不需要 **New-CsSipProxyTLS** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsSipProxyTLS** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSimpleUrlEntry"}

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
<td><p><em>Certificate</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ITLSTLSChoice</p></td>
<td><p>TLS 驗證所使用的憑證。</p></td>
</tr>
<tr class="even">
<td><p><em>Fqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>下一個躍點伺服器的完整網域名稱 (FQDN)。例如：-Fqdn atl-proxy-001.litwareinc.com。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsSipProxyTLS** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsSipProxyTLS** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.TLS 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsSipProxyTCP](new-cssipproxytcp.md)  
[New-CsSipProxyTransport](new-cssipproxytransport.md)  
[New-CsSipProxyUseDefaultCert](new-cssipproxyusedefaultcert.md)

