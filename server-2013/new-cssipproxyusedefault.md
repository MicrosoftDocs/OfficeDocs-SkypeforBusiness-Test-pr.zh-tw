---
title: New-CsSipProxyUseDefault
TOCTitle: New-CsSipProxyUseDefault
ms:assetid: 1e8bedca-8bd5-4559-b530-0f18ae23d6d3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398274(v=OCS.15)
ms:contentKeyID: 49290295
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyUseDefault

 

_**上次修改主題的時間：** 2015-03-09_

用於將預設領域 (SIP 通訊服務) 指派給 Proxy 組態設定的集合。領域 (又稱為保護網域) 可在登入期間用於驗證使用者憑證。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsSipProxyUseDefault

## 範例

## 範例 1

範例 1 所示的命令指派預設領域 (SIP Communications Service) 給名為 $x 的變數。

    $x = New-CsSipProxyUseDefault

## 詳細描述

Proxy 伺服器可讓內部網路以外的使用者存取內部網路上的資源。每個 Proxy 伺服器都必須與一個領域相關聯；領域 (也稱為保護網域) 表示處理使用者登入認證的位置。根據預設，Lync Server 使用 SIP Communications Service 做為其預設領域；但是可能會變更 Proxy 伺服器所採用的領域。如果您變更領域之後想要回復為使用預設領域，您可以建立一個 SipProxy.UseDefault 物件，然後將該物件指派給適當 Proxy 伺服器的 Realm 屬性。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsSipProxyUseDefault** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyUseDefault"}

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
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsSipProxyUseDefault** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsSipProxyUseDefault** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.UseDefault 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsSipProxyCustom](new-cssipproxycustom.md)  
[New-CsSipProxyRealm](new-cssipproxyrealm.md)

