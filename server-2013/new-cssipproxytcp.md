---
title: New-CsSipProxyTCP
TOCTitle: New-CsSipProxyTCP
ms:assetid: 27600a10-cc00-4be0-ab47-0bb06e65e4cd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425745(v=OCS.15)
ms:contentKeyID: 49290412
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyTCP

 

_**上次修改主題的時間：** 2015-03-09_

建立新的 SipProxy.TCP 物件，可用於設定靜態路由，以使用傳輸控制通訊協定 (TCP) 做為傳輸通訊協定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsSipProxyTCP -IPAddress <String>

## 範例

## 範例 1

範例 1 所示的命令會建立使用 TCP 做為傳輸的新 SIP Proxy 傳輸物件。為達成此目的，範例中的第一個命令會使用 **New-CsSipProxyTCP** Cmdlet 建立新的 SipProxy.TCP 物件，並將其指向 IP 位址為 192.168.1.100 的下一個躍點伺服器；此 TCP 物件會儲存在名為 $tcp 的變數中。

建立 SipProxy.TCP 物件之後，**New-CsSipProxyTransport** Cmdlet 會建立 TCP 傳輸物件。

    $tcp = New-CsSipProxyTCP -IPAddress 192.168.1.100
    
    $transport = New-CsSipProxyTransport -TransportChoice $tcp -Port 7500

## 詳細描述

當您傳送 SIP 訊息給某人，該訊息可能需要在傳遞之前周遊多個子網路和網路；訊息所經歷的路徑通常稱為路由。網路中有兩種路由類型：動態和靜態。透過動態路由，伺服器使用演算法判斷訊息應轉送的下一個位置 (下一個躍點)。透過靜態路由，訊息路徑由系統管理員預先決定。當伺服器接收到訊息，伺服器會檢查訊息位址，然後將訊息轉送至已由管理員預先決定的下一個躍點伺服器。如果設定正確，靜態路由會協助確保及時並正確地傳遞訊息，且在伺服器上只要最小限度的監聽。靜態路由的缺點在於當網路失敗時，無法再次動態地傳送訊息。

Lync Server 可讓您設定 Proxy 伺服器的靜態路由。這些路由由兩個主要片段組成：Proxy 組態設定 (使用 **New-CsProxyConfiguration** Cmdlet 建立) 和 SIP Proxy 路由。SIP Proxy 路由含有數個屬性；例如，各個路由必須具備定義用於經路由傳送訊息之網路通訊協定的 Transport 屬性。

Lync Server 可讓您將傳輸控制通訊協定 (TCP) 或傳輸層安全性 (TLS) 指定為您的傳輸通訊協定。如果您決定使用 TCP 做為通訊協定，則必須先使用 **New-CsSipProxyTCP** Cmdlet 建立 TCP 物件。然後，您可以使用該物件指定 **New-CsSipProxyTransport** Cmdlet 所建立之 Transport 物件的通訊協定。

如果您使用 **New-CsStaticRoute** Cmdlet 建立靜態路由，則無需使用 **New-CsSipProxyTCP** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsSipProxyTCP** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyTCP"}

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
<td><p><em>IPAddress</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>下一個躍點路由器的 IP 位址。例如：-IPAddress 192.168.0.240。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsSipProxyTCP** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsSipProxyTCP** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.TCP 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsSipProxyTLS](new-cssipproxytls.md)  
[New-CsSipProxyTransport](new-cssipproxytransport.md)

