---
title: Set-CsProxyConfiguration
TOCTitle: Set-CsProxyConfiguration
ms:assetid: 2eb74d25-05b5-4901-aa92-eeda2f351e25
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425796(v=OCS.15)
ms:contentKeyID: 49290468
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsProxyConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的 Proxy 伺服器組態設定集合。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsProxyConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsProxyConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AcceptClientCompression <$true | $false>] [-AcceptServerCompression <$true | $false>] [-AllowPartnerPollingSubscribes <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisableNtlmFor2010AndLaterClients <$true | $false>] [-DnsCacheRecordCount <UInt32>] [-EnableLoggingAllMessageBodies <$true | $false>] [-EnableWhiteSpaceKeepAlive <$true | $false>] [-Force <SwitchParameter>] [-LoadBalanceEdgeServers <$true | $false>] [-LoadBalanceInternalServers <$true | $false>] [-MaxClientCompressionCount <UInt32>] [-MaxClientMessageBodySizeKb <UInt32>] [-MaxKeepAliveInterval <UInt32>] [-MaxServerCompressionCount <UInt32>] [-MaxServerMessageBodySizeKb <UInt32>] [-OutgoingTlsCount <UInt32>] [-Realm <IRealmChoice>] [-RequestServerCompression <$true | $false>] [-TreatAllClientsAsRemote <$true | $false>] [-UseCertificateForClientToProxyAuth <$true | $false>] [-UseKerberosForClientToProxyAuth <$true | $false>] [-UseNtlmForClientToProxyAuth <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，會修改 Identity 為 service:EdgeServer:atl-edge-001.litwareinc.com 的所有 Proxy 組態設定，以接受伺服器壓縮。作法是呼叫 **Set-CsProxyConfiguration** Cmdlet 搭配 AcceptServerCompression 參數，並將參數值設為 True。

    Set-CsProxyConfiguration -Identity service:EdgeServer:atl-edge-001.litwareinc.com -AcceptServerCompression $True

## 範例 2

範例 2 會找出接受伺服器壓縮的所有 Proxy 組態設定，然後將這些設定修改為也接受用戶端壓縮。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsProxyConfiguration** Cmdlet，以傳回組織正在使用的所有 Proxy 設定集合。然後再將集合管線傳送到 **Where-Object** Cmdlet，這會只挑出 AcceptServerCompression 屬性等於 True 的設定。接著將篩選後的集合管線傳送到 **Set-CsProxyConfiguration** Cmdlet，以取得集合中的每個項目，將 AcceptClientCompression 屬性設為 True。

    Get-CsProxyConfiguration | Where-Object {$_.AcceptServerCompression -eq $True} | Set-CsProxyConfiguration -AcceptClientCompression $True

## 範例 3

範例 3 會示範如何修改已在服務範圍設定的所有 Proxy 設定。為達成此目的，命令會先呼叫 **Get-CsProxyConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "service:\*" 可確保只會傳回 Identity 開頭為字串值 "service:" 的設定。然後再將篩選後的集合管線傳送到 **Set-CsProxyConfiguration** Cmdlet，以取得集合中的每個項目，並將 UseNtlmForClientToProxyAuth 屬性設為 False。

    Get-CsProxyConfiguration -Filter service:* | Set-CsProxyConfiguration -UseNtlmForClientToProxyAuth $False

## 詳細描述

Lync Server 可讓您透過 Proxy 伺服器組態設定管理您的 Proxy 伺服器。這些可同時在全域範圍和服務範圍上套用的設定 (雖然只針對 Edge Server 和登錄器服務)，可讓您控制能夠由用戶端端點使用的驗證通訊協定，以及是否在傳入和傳出的 Proxy 伺服器連線中使用壓縮。安裝 Lync Server 時，會自動為您建立全域的 Proxy 伺服器組態設定集合。如上述，您還可以在服務範圍上建立其他集合。

**Set-CsProxyConfiguration** Cmdlet 可讓您修改 Proxy 伺服器組態設定之現有集合的屬性值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsProxyConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsProxyConfiguration"}

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
<td><p><em>AcceptClientCompression</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，Proxy 伺服器會接受所有從用戶端端點傳入的壓縮要求。</p></td>
</tr>
<tr class="even">
<td><p><em>AcceptServerCompression</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，Proxy 伺服器會接受所有從其他伺服器傳入的壓縮要求。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPartnerPollingSubscribes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，可允許夥伴應用程式定期輪詢服務，以查看狀態變更。預設值為 False ($False)。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableNtlmFor2010AndLaterClients</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，使用者從 Lync 登入必須使用 Kerberos 通訊協定進行驗證。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>DnsCacheRecordCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>DNS 記錄快取中可保留的記錄數目上限。預設值是 3000。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLoggingAllMessageBodies</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時， Lync Server 會記錄所有立即訊息的實際內容。基於隱私權，通常會刪除訊息內容，只會在記錄檔中包含通訊端點的資訊。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableWhiteSpaceKeepAlive</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，Proxy 伺服器會預期用戶端定期傳送「空白字元訊息」(沒有內容的空訊息) 來表示其連線依然在作用中。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之 Proxy 伺服器組態設定的唯一識別碼。若要修改全域設定，請使用下列語法：-Identity global。若要修改在服務範圍設定的設定，請使用類似下列的語法：-Identity &quot;service:EdgeServer:atl-edge-001.litwareinc.com&quot;。</p>
<p>若未加入此參數，則 <strong>Set-CsProxyConfiguration</strong> Cmdlet 將會自動修改全域設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>ProxySettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>LoadBalanceEdgeServers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數為 True 時，會針對向 Edge Server 提出的要求採用軟體負載平衡。預設值為 True ($True)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LoadBalanceInternalServers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數為 True 時，會針對向登錄器及其他內部伺服器提出的要求採用軟體負載平衡。預設值為 True ($True)。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxClientCompressionCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指出在任何指定時間可壓縮之用戶端至伺服器的連線數目上限；超過此限制的其他連線不會被壓縮。可將壓縮計數設為介於 0 (含) 和 65535 (含) 之間的任何整數值。預設值為 15000。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxClientMessageBodySizeKb</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>從用戶端端點傳送的訊息本文所允許的大小上限 (單位為 KB)。預設值為 128，表示大於 128 KB 的訊息本文會被拒絕。可將用戶端訊息本文大小設為介於 64 (含) 和 256 (含) 之間的任何整數值。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxKeepAliveInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指定經過多少時間 (以分鐘為單位) 後，伺服器要驗證與用戶端的連線仍有效。預設值為 20 分鐘。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxServerCompressionCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指出在任何指定時間可壓縮之伺服器至伺服器的連線數目上限；超過此限制的其他連線不會被壓縮。可將伺服器壓縮計數設為介於 0 (含) 和 65535 (含) 之間的任何整數值。預設值為 1024。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxServerMessageBodySizeKb</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>從其他伺服器傳送的訊息本文所允許的大小上限 (KB)。預設值為 5000，表示大於 5000 KB 的訊息本文會被拒絕。可將伺服器訊息本文大小設為介於 1000 (含) 和 20000 (含) 之間的任何整數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutgoingTlsCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指定可用於每個內部伺服器的傳輸層安全性 (TLS) 連線數量上限。TLS 連線數目下限為 1，上限為 4。依據預設，OutgoingTlsCount 設為 4。</p></td>
</tr>
<tr class="even">
<td><p><em>Realm</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.IRealmChoice</p></td>
<td><p>表示安全性認證是由預設的 Proxy 伺服器領域 (SIP 通訊服務) 或由自訂領域處理。自訂領域必須使用 <strong>New-CsSipProxyCustom</strong> Cmdlet 指定 (或建立)。</p></td>
</tr>
<tr class="odd">
<td><p><em>RequestServerCompression</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，Proxy 伺服器會要求在所有連至伺服器的傳出連線上必須使用壓縮。</p></td>
</tr>
<tr class="even">
<td><p><em>TreatAllClientsAsRemote</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，Proxy 伺服器的運作會好像所有用戶端連線為透過 Edge Server 傳遞之外部連線一樣。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseCertificateForClientToProxyAuth</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，用戶端端點可以使用憑證進行驗證。</p></td>
</tr>
<tr class="even">
<td><p><em>UseKerberosForClientToProxyAuth</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，用戶端端點可以使用 Kerberos 通訊協定進行驗證。雖然 Kerberos 是比 NTLM 更安全的通訊協定，但是如果用戶端與伺服器屬於不同的領域，則無法使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseNtlmForClientToProxyAuth</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，用戶端端點可以使用 NTLM 通訊協定進行驗證。雖然 NTLM 是比 Kerberos 不安全的通訊協定，但是如果用戶端與伺服器屬於不同的網域，還是可以使用 NTLM。Kerberos 驗證則不是如此。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings 物件。**Set-CsProxyConfiguration** Cmdlet 接受 Proxy 設定物件的管線傳送執行個體。

## 傳回類型

**Set-CsProxyConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsProxyConfiguration](get-csproxyconfiguration.md)  
[New-CsProxyConfiguration](new-csproxyconfiguration.md)  
[Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)

