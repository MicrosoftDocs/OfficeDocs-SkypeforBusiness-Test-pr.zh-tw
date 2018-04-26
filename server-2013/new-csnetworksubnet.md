---
title: New-CsNetworkSubnet
TOCTitle: New-CsNetworkSubnet
ms:assetid: 15af44bd-d798-435c-9c27-df47ab475023
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398226(v=OCS.15)
ms:contentKeyID: 49290193
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkSubnet

 

_**上次修改主題的時間：** 2015-03-09_

建立新的網路子網路。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsNetworkSubnet -SubnetID <String> <COMMON PARAMETERS>

    New-CsNetworkSubnet -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -MaskBits <Int32> [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-NetworkSiteID <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會示範如何建立代表子網路 172.11.15.0/24 的新子網路物件。該子網路的 Identity 設為 172.11.15.0。此值會自動被指派為 SubnetID。您必須為子網路定義遮罩位元。作法是提供 MaskBits 參數的值 (在此範例中為 24)。最後，此網站 ID Vancouver 會傳遞給 NetworkSiteID 參數，讓子網路與該網站產生關聯。

    New-CsNetworkSubnet -Identity 172.11.15.0 -MaskBits 24 -NetworkSiteID Vancouver

## 範例 2

範例 2 會讀取 CSV 檔案，以建立一連串的子網路。此範例中的 CSV 檔案外觀應類似如下：

Identity, Mask, SiteID

172.11.12.0, 24, Redmond

172.11.13.0, 24, Chicago

172.11.14.0, 25, Vancouver

172.11.15.0, 31, Paris

...

此範例會從呼叫 **Import-CSV** Cmdlet 開始，並將 CSV 檔的路徑傳遞給它。此 Cmdlet 會將該檔案的內容讀入記憶體。接著，這些檔案內容會傳送到 foreach 函數。foreach 函數會一次一行、逐一查看內容。如同您可以在範例檔中看到的一樣，第一行是定義其餘內容的標題清單；foreach 函數將會使用這些標題依名稱存取逗點分隔值。

在 foreach 陳述式內，會呼叫 **New-CsNetworkSubnet** Cmdlet。因為 foreach 會逐一查看檔案內容的每一行，因此該行會當作 **New-CsNetworkSubnet** Cmdlet 參數的值來傳遞。例如，第一次執行 foreach 陳述式時， **New-CsNetworkSubnet** Cmdlet 會建立 Identity 為 172.11.12.0 的子網路：這是在以逗點分隔值的第一行中 Identity 位置的值 ($\_ 表示 foreach 迴圈中目前的值)。然後，Mask 值 (24) 會傳遞到 MaskBits 參數，而檔案中的 SiteID 值 (Redmond) 會傳遞到 NetworkSiteID 參數。

此處理序會繼續，直到讀取完檔案中的所有行，並使用其值建立新的子網路為止。

    Import-CSV C:\subnet.csv | foreach {New-CsNetworkSubnet -Identity $_.Identity -MaskBits $_.Mask -NetworkSiteID $_.SiteID}

## 詳細描述

為了判斷屬於此子網路的主機地理位置，每一個子網路都必須與網站相關聯。使用此 Cmdlet 可建立新的子網路，同時 (選擇性地) 將其指派至網站。

在已實作通話許可控制 (CAC) 的大多數 Lync Server 部署中，通常有大量子網路。因此，通常建議呼叫 **New-CsNetworkSubnet** Cmdlet 並搭配 **Import-CSV** Cmdlet。您可以同時使用這些 Cmdlet，一次從逗點分隔值 (CSV) 檔案讀入子網路設定並建立多個子網路。 如需詳細資訊，請參閱此 Cmdlet 的＜範例＞區段。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsNetworkSubnet** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkSubnet"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要建立之子網路的唯一子網路 ID。此 ID 必須是 IP 位址 (例如 174.11.12.0)，而且必須是子網路定義之 IP 位址範圍中的第一個位址。</p></td>
</tr>
<tr class="even">
<td><p><em>MaskBits</em></p></td>
<td><p>必要</p></td>
<td><p>System.Int32</p></td>
<td><p>要套用至所建立之子網路的位元遮罩。</p>
<p>有效值：1 到 32</p></td>
</tr>
<tr class="odd">
<td><p><em>SubnetID</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>這是與 Identity 相同的值。您必須指定 Identity 或 SubnetID，但不可兩者皆指定。無論您提供的是哪一個值，都將會自動套用至另一個。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>要建立之子網路的描述。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>此子網路所屬之網站的網站 ID。您可以呼叫 <strong>Get-CsNetworkSite</strong> Cmdlet 來擷取部署的網站識別碼。</p></td>
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

無。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsNetworkSubnet](remove-csnetworksubnet.md)  
[Set-CsNetworkSubnet](set-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkSite](get-csnetworksite.md)

