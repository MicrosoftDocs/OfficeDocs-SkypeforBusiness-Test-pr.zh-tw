---
title: Remove-CsProxyConfiguration
TOCTitle: Remove-CsProxyConfiguration
ms:assetid: 738f731c-4d62-4395-bdc3-3f5e5738f443
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398553(v=OCS.15)
ms:contentKeyID: 49291327
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsProxyConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的 Proxy 伺服器組態設定集合。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsProxyConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除具有 Identity service:EdgeServer:atl-edge-litwareinc.com 的 Proxy 組態設定。

    Remove-CsProxyConfiguration -Identity service:EdgeServer:atl-edge-011.litwareinc.com 

## 範例 2

範例 2 會刪除在服務範圍套用的所有 Proxy 組態設定。為了完成此工作，命令會先呼叫 **Get-CsProxyConfiguration** Cmdlet 並搭配 Filter 參數；篩選值 "service:\*" 可確保只會傳回 Identity 開頭為字串值 "service:" 的 Proxy 設定。然後再將篩選後集合管線傳送到 **Remove-CsProxyConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsProxyConfiguration -Filter "service:*" | Remove-CsProxyConfiguration

## 範例 3

範例 3 會刪除將所有用戶端視為遠端用戶端的任何 Proxy 組態設定。為達此目的，會先呼叫不含任何參數的 **Get-CsProxyConfiguration** Cmdlet，以傳回目前正在使用的所有 Proxy 伺服器組態設定集合。然後，此集合會以管線傳送到 **Where-Object** Cmdlet，只選取 TreatAllClientsAsRemote 屬性等於 True 的設定。接著將此 Proxy 組態設定的子集合以管線傳送到 **Remove-CsProxyConfiguration** Cmdlet，以移除集合中的所有設定。

    Get-CsProxyConfiguration | Where-Object {$_.TreatAllClientsAsRemote -eq $True} | Remove-CsProxyConfiguration

## 詳細描述

Lync Server 可讓您透過 Proxy 伺服器組態設定管理您的 Proxy 伺服器。這些可同時在全域範圍和服務範圍上套用的設定 (雖然只針對 Edge Server 和登錄器服務)，可讓您控制能夠由用戶端端點使用的驗證通訊協定，以及是否在傳入和傳出的 Proxy 伺服器連線中使用壓縮。安裝 Lync Server 時，會自動為您建立全域的 Proxy 伺服器組態設定集合。如上述，您還可以在服務範圍上建立其他集合。

任何您建立的新 Proxy 伺服器設定都可以在之後使用 **Remove-CsProxyConfiguration** Cmdlet 移除。您也可以對全域集合執行 **Remove-CsProxyConfiguration** Cmdlet。但在此狀況下不會移除全域設定；因為 Lync Server 不容許您移除全域設定。而是將該全域集合中的所有屬性重設為預設值。例如，根據預設，Proxy 伺服器設定容許用戶端使用 Kerberos 通訊協定進行驗證。您可以變更全域設定以停用 Kerberos。不過，如果您對全域集合執行 **Remove-CsProxyConfiguration** Cmdlet，則上述的屬性 (UseKerberosForClientToProxyAuth) 將重設為預設值，且 Kerberos 會再度啟用，做為驗證通訊協定之用。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsProxyConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsProxyConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要移除之 Proxy 伺服器組態設定的唯一識別碼，例如：-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;。</p>
<p>您也可以對全域設定執行 <strong>Remove-CsProxyConfiguration</strong> Cmdlet。但在此狀況下不會移除設定。而是將該全域集合中的屬性全部重設為預設值。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings 物件。 **Remove-CsProxyConfiguration** Cmdlet 接受 Proxy 設定物件的管線傳送執行個體。

## 傳回類型

無。反之， **Remove-CsProxyConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsProxyConfiguration](get-csproxyconfiguration.md)  
[New-CsProxyConfiguration](new-csproxyconfiguration.md)  
[Set-CsProxyConfiguration](set-csproxyconfiguration.md)

