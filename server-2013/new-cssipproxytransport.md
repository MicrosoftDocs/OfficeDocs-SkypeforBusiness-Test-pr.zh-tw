---
title: New-CsSipProxyTransport
TOCTitle: New-CsSipProxyTransport
ms:assetid: 68587257-d666-429a-bf2d-f8a2b46f1f09
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398489(v=OCS.15)
ms:contentKeyID: 49291180
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyTransport

 

_**上次修改主題的時間：** 2015-03-09_

指定靜態路由所要使用的傳輸通訊協定。Lync Server 可讓您選擇使用傳輸控制通訊協定 (TCP) 或傳輸層安全性 (TLS) 做為路由的傳輸通訊協定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsSipProxyTransport -Port <UInt16> -TransportChoice <ITransportChoice>

## 範例

## 範例 1

範例 1 所示的命令會建立使用 TLS 做為傳輸的新 SIP Proxy 傳輸物件。由於 TLS 需要憑證(以供驗證之用)，因此範例中的第一個命令會使用 **New-CsSipProxyUseDefaultCert** Cmdlet 設定新的 SipProxy.UseDefaultCert 物件。此物件儲存在名為 $cert 的變數中，並會指示 Lync Server 針對 TLS 傳輸使用預設憑證。在建立 UseDefaultCert 物件之後，可以呼叫 **New-CsSipProxyTLS** Cmdlet 建立新的 SipProxy.TLS 物件，此物件使用預設憑證並指向 atl-proxy-001.litwareinc.com 做為下一個躍點伺服器的完整網域名稱 (FQDN)。

    $cert = New-CsSipProxyUseDefaultCert
    
    $tls = New-CsSipProxyTLS -Certificate $cert -Fqdn atl-proxy-001.litwareinc.com
    
    $transport = New-CsSipProxyTransport -TransportChoice $tls -Port 7500

## 範例 2

範例 2 所示的命令會建立使用 TCP 做為傳輸的新 SIP Proxy 傳輸物件。為達成此目的，範例中的第一個命令會使用 **New-CsSipProxyTCP** Cmdlet 建立新的 SipProxy.TCP 物件，並將其指向 IP 位址為 192.168.1.100 的下一個躍點伺服器；此 TCP 物件會儲存在名為 $tcp 的變數中。

建立 SipProxy.TCP 物件之後，**New-CsSipProxyTransport** Cmdlet 會建立 TCP 傳輸物件。

    $tcp = New-CsSipProxyTCP -IPAddress 192.168.1.100
    
    $transport = New-CsSipProxyTransport -TransportChoice $tcp -Port 7500

## 詳細描述

當您傳送 SIP 訊息給某人，該訊息可能需要在傳遞之前周遊多個子網路和網路；訊息所經歷的路徑通常稱為路由。網路中有兩種路由類型：動態和靜態。透過動態路由，伺服器使用演算法判斷訊息應轉送的下一個位置 (下一個躍點)。透過靜態路由，訊息路徑由系統管理員預先決定。當伺服器接收到訊息，伺服器會檢查訊息位址，然後將訊息轉送至已由管理員預先決定的下一個躍點伺服器。如果設定正確，靜態路由會協助確保及時並正確地傳遞訊息，且在伺服器上只要最小限度的監聽。靜態路由的缺點是在網路故障時，無法動態地重新路由傳送訊息。

Lync Server 可讓您設定 Proxy 伺服器的靜態路由。這些路由由兩個主要片段組成：Proxy 組態設定和 SIP Proxy 路由。因此，SIP Proxy 路由具有數個屬性；例如，每個路由都必須有一個 Transport，也就是定義沿路由傳輸訊息時使用之網路通訊協定的屬性。可使用 **New-CsSipProxyTransport** Cmdlet 來指定 Transport 屬性。

**New-CsSipProxyTransport** Cmdlet 有兩個必要參數：TransportChoice 和 Port。TransportChoice 參數是使用其他 Cmdlet 來設定︰**New-CsSipProxyTCP** Cmdlet (將傳輸控制通訊協定指派為路由傳輸) 或 **New-CsSipProxyTLS** Cmdlet (將 TLS 指派為路由傳輸)。任何使用 **New-CsSipProxyTransport** Cmdlet 所建立的傳輸物件都必須儲存至變數。該變數接著便會用於設定 SIP Proxy 路由的 Transport 屬性。

如果您使用 **New-CsStaticRoute** Cmdlet 建立靜態路由，則無需使用 **New-CsSipProxyTransport** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsSipProxyTransport** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyTransport"}

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
<td><p><em>Port</em></p></td>
<td><p>必要</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於 SIP 路由的連接埠號碼。例如：-Port 7742。</p></td>
</tr>
<tr class="even">
<td><p><em>TransportChoice</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ITransportChoice</p></td>
<td><p>指出要在靜態路由上使用的傳輸通訊協定 (TCP 或 TLS)。若要使用 TCP 通訊協定，請使用 <strong>New-CsSipProxyTCP</strong> Cmdlet 建立傳輸物件。若要使用 TLS 通訊協定，請使用 <strong>New-CsSipProxyTLS</strong> Cmdlet 建立傳輸物件。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsSipProxyTransport** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsSipProxyTransport** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.Transport 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsSipProxyTCP](new-cssipproxytcp.md)  
[New-CsSipProxyTLS](new-cssipproxytls.md)

