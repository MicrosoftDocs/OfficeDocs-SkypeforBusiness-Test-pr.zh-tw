---
title: New-CsSipProxyCustom
TOCTitle: New-CsSipProxyCustom
ms:assetid: 3dc75cb0-c3d2-48bd-af32-2b2034b655dd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425904(v=OCS.15)
ms:contentKeyID: 49290681
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyCustom

 

_**上次修改主題的時間：** 2015-03-09_

用於將自訂領域 (SIP 通訊服務) 指派給 Proxy 組態設定的集合。領域 (又稱為保護網域) 可在登入期間用於驗證使用者憑證。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsSipProxyCustom -CustomValue <String>

## 範例

## 範例 1

範例 1 所示的命令會指派自訂領域 (Litwareinc Communications Service) 給名為 $x 的變數。

    $x = New-CsSipProxyCustom -CustomValue "Litwareinc Communications Service"

## 詳細描述

每個 Proxy 伺服器都必須與一個領域相關聯；領域 (也稱為保護網域) 表示處理使用者登入認證的位置。根據預設，Lync Server 使用 SIP 通訊服務做為其預設領域；但是可能會變更 Proxy 伺服器所使用的領域。作法是建立 SipProxy.Custom 物件，然後將該物件指派給適當 Proxy 伺服器的 Realm 屬性。您可以使用 **New-CsSipProxyCustom** Cmdlet 建立自訂領域。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsSipProxyCustom** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyCustom"}

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
<td><p><em>CustomValue</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要用於驗證用途之領域的名稱。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsSipProxyCustom** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsSipProxyCustom** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.Custom 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsSipProxyRealm](new-cssipproxyrealm.md)  
[New-CsSipProxyUseDefault](new-cssipproxyusedefault.md)

