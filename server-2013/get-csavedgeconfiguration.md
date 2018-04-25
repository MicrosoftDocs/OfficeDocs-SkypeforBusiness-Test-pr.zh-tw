---
title: Get-CsAVEdgeConfiguration
TOCTitle: Get-CsAVEdgeConfiguration
ms:assetid: f1a0db80-158c-47bd-8a8e-30e3f095fb2a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413008(v=OCS.15)
ms:contentKeyID: 49292770
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAVEdgeConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回您組織中A/V Edge 服務 電腦的組態資訊。這些電腦上的組態設定 (又稱為 A/V Edge Server) 可讓內部使用者與外部使用者 (亦即未登入內部網路的使用者) 一起共用音訊和視訊資料，以及交換檔案與參與桌面期用工作階段。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAVEdgeConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsAVEdgeConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有 A/V Edge 組態設定的集合。呼叫不含任何參數的 **Get-CsAVEdgeConfiguration** Cmdlet 會傳回完整之 A/V Edge 組態設定的集合。

    Get-CsAVEdgeConfiguration

## 範例 2

範例 2 會傳回 A/V Edge 組態設定的單一集合：集合的 Identity 為 site:Redmond。

    Get-CsAVEdgeConfiguration -Identity site:Redmond

## 範例 3

範例 3 會傳回在網站範圍設定的所有 A/V Edge 組態設定集合。為成達此目的，會呼叫 **Get-CsAVEdgeConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "site:\*" 會將傳回的資料限制在 Identity 開頭為字元 "site:" 的設定。根據定義，這會將傳回的資料限制在網站範圍所設定的設定值。

    Get-CsAVEdgeConfiguration -Filter "site:*"

## 範例 4

在範例 4 中，唯一傳回的 A/V Edge 組態設定是 MaxBandwidthPerUserKB 屬性大於每秒 10,000 KB 的設定。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsAVEdgeConfiguration** Cmdlet，以傳回目前所使用之所有 A/V Edge 組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 MaxBandwidthPerUserKB 每秒大於 10000 千位元的設定。

    Get-CsAVEdgeConfiguration | Where-Object {$_.MaxBandwidthPerUserKB -gt 10000}

## 範例 5

範例 5 與範例 4 所示的命令類似；但是，在範例 5 中，只有 MaxBandwidthPerUserKB 屬性確實等於每秒 10000 千位元的 A/V Edge 設定才會被傳回。

    Get-CsAVEdgeConfiguration | Where-Object {$_.MaxBandwidthPerUserKB -eq 10000}

## 範例 6

範例 6 所示的命令只會傳回 MaxTokenLifetime 屬性小於 8 小時 (08 小時：00 分鐘：00 秒) 的 A/V Edge 組態設定。此命令會先呼叫不含任何參數的 **Get-CsAVEdgeConfiguration** Cmdlet，以傳回組織所使用之所有 A/V Edge 組態設定的集合。然後此將該集合管線傳送到 **Where-Object** Cmdlet，這會只挑出 MaxTokenLifetime 小於 8 小時 (08:00:00) 的設定。

    Get-CsAVEdgeConfiguration | Where-Object {$_.MaxTokenLifetime -lt "08:00:00"}

## 詳細描述

A/V Edge Server 提供一種方法，可穿過組織防火牆交換音訊和視訊流量。除此之外，這可讓使用者透過網際網路存取 Lync Server，然後與在防火牆內登入系統的使用者交換音訊和視訊資料。您可以在全域範圍、網站範圍和服務範圍指派 Edge Server 組態設定。A/V Edge 組態設定可讓系統管理員執行這類工作：管理使用者驗證在必須更新前的有效時間，以及限制單一使用者或單一連接埠可以使用的頻寬量。

**Get-CsAVEdgeConfiguration** Cmdlet 提供方法，讓您擷取目前組織中使用的 A/V Edge 組態設定相關資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsAVEdgeConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAVEdgeConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>讓您能夠在指出要傳回的 A/V Edge 組態設定時使用萬用字元。例如，若要傳回在網站範圍所設定的所有設定，請使用下列語法：-Filter site:*。若要傳回已在服務上設定的所有設定集合，請使用下列語法：-Filter &quot;service:*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之 A/V Edge 組態設定集合的唯一識別碼。若要擷取全域集合，請使用下列語法：-Identity global。若要擷取網站集合，請使用類似下列的語法：-Identity site:Redmond。您應使用如下的語法，提到在服務範圍設定的設定：-Identity service:EdgeServer:atl-cs-001.litwareinc.com。請注意，您在指定原則的 Identity 時，無法使用萬用字元。</p>
<p>若未加入此參數，<strong>Get-CsAVEdgeConfiguration</strong> Cmdlet 將傳回組織目前所使用之所有 Edge 組態設定的集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取 A/V Edge 組態資料，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsAVEdgeConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsAVEdgeConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.MediaRelaySettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)  
[Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)  
[Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

