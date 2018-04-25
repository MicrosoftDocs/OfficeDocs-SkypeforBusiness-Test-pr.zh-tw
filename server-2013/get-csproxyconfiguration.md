---
title: Get-CsProxyConfiguration
TOCTitle: Get-CsProxyConfiguration
ms:assetid: e4836619-026f-4df0-adbd-aa5216e36368
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399011(v=OCS.15)
ms:contentKeyID: 49292613
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsProxyConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回目前設定供組織使用之 Proxy 伺服器組態設定的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsProxyConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsProxyConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織目前使用之所有 Proxy 組態設定的集合。作法是呼叫不含任何參數的 **Get-CsProxyConfiguration** Cmdlet。

    Get-CsProxyConfiguration

## 範例 2

範例 2 會傳回 Identity 為 service:EdgeServer:atl-cs-001.litwareinc.com 之 Proxy 組態設定的資訊。由於 Identity 必須是唯一的，因此這個命令絕對不會傳回一個以上的設定集合。

    Get-CsProxyConfiguration -Identity "service:EdgeServer:atl-cs-001.litwareinc.com"

## 範例 3

範例 3 會傳回在服務範圍設定之所有 Proxy 設定的資訊。為達成此目的，命令會呼叫 **Get-CsProxyConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "service:\*" 會確保只傳回 Identity 開頭為字串值 "service:" 的設定。

    Get-CsProxyConfiguration -Filter "service:*"

## 範例 4

範例 4 會傳回不允許將用戶端認證做為驗證機制使用之 Proxy 組態設定的資訊。為了執行此工作，命令會先使用 **Get-CsProxyConfiguration** Cmdlet 傳回目前使用的所有 Proxy 組態設定集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 UseCertificateForClientToProxyAuth 屬性等於 False 的設定。

    Get-CsProxyConfiguration | Where-Object {$_.UseCertificateForClientToProxyAuth -eq $False}

## 範例 5

範例 5 會傳回用戶端訊息本文的大小上限小於 5000 KB 的所有 Proxy 組態設定。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsProxyConfiguration** Cmdlet，以傳回目前使用之所有 Proxy 組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 MaxClientMessageBodySizeKb 屬性小於 5000 KB 的設定。

    Get-CsProxyConfiguration | Where-Object {$_.MaxClientMessageBodySizeKb -lt 5000}

## 詳細描述

Lync Server 可讓您經由 Proxy 伺服器組態設定來管理 Proxy 伺服器。這些可同時在全域範圍和服務範圍上套用的設定 (雖然只針對 Edge Server 和登錄器服務)，可讓您控制能夠由用戶端端點使用的驗證通訊協定，以及是否在傳入和傳出的 Proxy 伺服器連線中使用壓縮。安裝 Lync Server 時，會自動為您建立全域的 Proxy 伺服器組態設定集合。如上述，您還可以在服務範圍上建立其他集合。

**Get-CsProxyConfiguration** Cmdlet 可讓您傳回目前組織所使用之任何 Proxy 伺服器組態設定的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsProxyConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsProxyConfiguration"}

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
<td><p>可讓您在指定要傳回的 Proxy 組態設定時，使用萬用字元。例如，此語法會傳回設定於服務範圍的所有設定：-Filter &quot;service:*&quot;。</p>
<p>您無法在同一個命令中同時使用 Filter 與 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之 Proxy 伺服器組態設定的唯一識別碼。若要傳回全域設定，請使用下列語法：-Identity global。若要傳回在服務範圍內所做的設定，請使用類似下列的語法：-Identity &quot;service:EdgeServer:atl-cs-001.litwareinc.com&quot;。請注意，如有指定 Identity，即無法使用萬用字元。如果您要 (或需要) 使用萬用字元，則請改用 Filter 參數。</p>
<p>如果未加入此參數，<strong>Get-CsProxyConfiguration</strong> Cmdlet 會傳回目前組織使用的所有 Proxy 伺服器設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取 Proxy 組態資料，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsProxyConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsProxyConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsProxyConfiguration](new-csproxyconfiguration.md)  
[Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)  
[Set-CsProxyConfiguration](set-csproxyconfiguration.md)

