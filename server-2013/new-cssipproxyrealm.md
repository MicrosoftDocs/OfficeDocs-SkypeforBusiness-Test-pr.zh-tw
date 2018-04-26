---
title: New-CsSipProxyRealm
TOCTitle: New-CsSipProxyRealm
ms:assetid: fedf9c71-5a23-4818-9f98-db5008a2ba74
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413084(v=OCS.15)
ms:contentKeyID: 49292925
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyRealm

 

_**上次修改主題的時間：** 2015-03-09_

用於將預設領域 (SIP 通訊服務) 指派給 Proxy 組態設定的集合。領域 (又稱為保護網域) 可在登入期間用於驗證使用者憑證。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsSipProxyRealm -RealmChoice <IRealmChoice>

## 範例

## 範例 1

範例 1 所示的命令會將預設領域 (SIP Communications Service) 指派給變數 $y。為達成此目的，第一個命令會呼叫 **New-CsSipProxyUseDefault** Cmdlet 建立 SipProxy.UseDefault 物件；此物件會儲存在名為 $x 的變數中。

在第二個命令中，$x 會用來做為 **New-CsSipProxyRealm** Cmdlet 和 RealmChoice 參數的參數值。而如此一來會建立新的 Proxy 領域物件，此物件會儲存在名稱為 $y 的變數中。

    $x = New-CsSipProxyUseDefault
    $y = New-CsSipProxyRealm -RealmChoice $x

## 範例 2

範例 2 所示的命令會將自訂領域 (Litwareinc Communications Service) 指派給變數 $y。為達成此目的，第一個命令會呼叫 **New-CsSipProxyCustom** Cmdlet 建立 SipProxy.Custom 物件；此物件 (使用 CustomValue Litwareinc Communications Service) 會儲存在名為 $x 的變數中。

在第二個命令中，會將 $x 與 **New-CsSipProxyRealm** Cmdlet 和 RealmChoice 參數搭配使用，來建立新的自訂領域物件。

    $x = New-CsSipProxyCustom -CustomValue "Litwareinc Communications Service"
    $y = New-CsSipProxyRealm -RealmChoice $x

## 詳細描述

Proxy 伺服器可讓內部網路的外部使用者存取內部網路的資源。每台 Proxy 伺服器都必須關聯至一個領域；領域 (亦稱為保護網域) 會指出應繼續處理使用者登入憑證的位置。根據預設，Lync Server 使用 SIP Communications Service 做為其預設領域；但是可能會變更 Proxy 伺服器所使用的領域。**New-CsSipProxyUseDefault** Cmdlet 和 **New-CsSipProxyCustom** Cmdlet 可用於變更 Proxy 伺服器所使用的領域。您也可以使用 **New-CsSipProxyRealm** Cmdlet 進行這些變更。由於此 Cmdlet 需要其他步驟，因此，每當您需要變更 Proxy 伺服器所使用的領域時，可能會需要使用另外兩個 Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsSipProxyRealm** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyRealm"}

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
<td><p><em>RealmChoice</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.IRealmChoice</p></td>
<td><p>代表 Proxy 伺服器所使用之領域的物件。您必須使用 <strong>New-CsSipProxyUseDefault</strong> 或 <strong>New-CsSipProxyCustom</strong> Cmdlet 來建立 RealmChoice。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsSipProxyRealm** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsSipProxyRealm** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.Realm 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsSipProxyCustom](new-cssipproxycustom.md)  
[New-CsSipProxyUseDefault](new-cssipproxyusedefault.md)

