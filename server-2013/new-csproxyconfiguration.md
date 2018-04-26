---
title: New-CsProxyConfiguration
TOCTitle: New-CsProxyConfiguration
ms:assetid: 5133470e-1d77-4958-8844-a091336b2a3c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398335(v=OCS.15)
ms:contentKeyID: 49290903
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsProxyConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的 Proxy 組態設定集合。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsProxyConfiguration -Identity <XdsIdentity> [-AcceptClientCompression <$true | $false>] [-AcceptServerCompression <$true | $false>] [-AllowPartnerPollingSubscribes <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisableNtlmFor2010AndLaterClients <$true | $false>] [-DnsCacheRecordCount <UInt32>] [-EnableLoggingAllMessageBodies <$true | $false>] [-EnableWhiteSpaceKeepAlive <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-LoadBalanceEdgeServers <$true | $false>] [-LoadBalanceInternalServers <$true | $false>] [-MaxClientCompressionCount <UInt32>] [-MaxClientMessageBodySizeKb <UInt32>] [-MaxKeepAliveInterval <UInt32>] [-MaxServerCompressionCount <UInt32>] [-MaxServerMessageBodySizeKb <UInt32>] [-OutgoingTlsCount <UInt32>] [-Realm <IRealmChoice>] [-RequestServerCompression <$true | $false>] [-TreatAllClientsAsRemote <$true | $false>] [-UseCertificateForClientToProxyAuth <$true | $false>] [-UseKerberosForClientToProxyAuth <$true | $false>] [-UseNtlmForClientToProxyAuth <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立 EdgeServer:atl-edge-001.litwareinc.com 服務之 Proxy 組態設定的新集合。除下列兩項外，這些新設定會使用所有預設的 Proxy 伺服器屬性值：RequestServerCompression 設為 True；MaxClientMessageBodySizeKb 設為 256。請注意，如果已經為 EdgeServer:atl-edge-001.litwareinc.com 服務設定 Proxy 伺服器設定，此命令會失敗。

    New-CsProxyConfiguration -Identity "service:EdgeServer:atl-edge-001.litwareinc.com" -RequestServerCompression $True -MaxClientMessageBodySizeKb 256

## 範例 2

範例 2 所示的命令示範如何建立最初只存在於記憶體內的 Proxy 伺服器設定集合。為達成此目的，命令會先呼叫 **New-CsProxyConfiguration** Cmdlet 搭配 Identity (指定設定的 Identity) 和 InMemory (指定只可在記憶體中建立新設定) 兩個參數。產生的物件會儲存在 $x 變數中。

建立這些虛擬設定後，命令 2 和 3 會分別用來修改 RequestServerCompression 和 MaxClientMessageBodySizeKb 屬性的值。最後，命令 4 用來將虛擬 Proxy 伺服器組態設定轉換為套用到 service EdgeServer:atl-edge-001.litwareinc.com 服務的實際設定集合。最後一個命令是必要項目。如果您沒有呼叫 **Set-CsProxyConfiguration** Cmdlet，則設定不會套用到 EdgeServer:atl-edge-001.litwareinc.com，並在您結束 Windows PowerShell 工作階段或刪除變數 $x 時，虛擬設定會消失。

    $x = New-CsProxyConfiguration -Identity "service:EdgeServer:atl-edge-001.litwareinc.com" -InMemory
    $x.RequestServerCompression = $True 
    $x.MaxClientMessageBodySizeKb = 256
    Set-CsProxyConfiguration -Instance $x

## 詳細描述

Lync Server 可讓您經由 Proxy 伺服器組態設定來管理 Proxy 伺服器。這些可同時在全域範圍和服務範圍上套用的設定 (雖然只針對 Edge Server 和登錄器服務)，可讓您控制能夠由用戶端端點使用的驗證通訊協定，以及是否在傳入和傳出的 Proxy 伺服器連線中使用壓縮。安裝 Lync Server 時，會自動為您建立全域的 Proxy 伺服器組態設定集合。如上述，您還可以在服務範圍上建立其他集合。這些新集合可以使用 **New-CsProxyConfiguration** Cmdlet 來建立。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsProxyConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsProxyConfiguration"}

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
<td><p>要建立之 Proxy 伺服器組態設定的唯一識別碼。Proxy 伺服器組態設定只能建立在服務範圍上，並只適用於 Edge Server 和登錄器服務。您無法在全域範圍上建立設定；同樣地，如果在該服務已託管一個 Proxy 伺服器設定的集合，則您無法在服務範圍上建立設定。例如，如果 Registrar:atl-cs-001.litwareinc.com 服務已主控一個 Proxy 伺服器設定，任何嘗試為該服務建立新設定的命令都會失敗。</p>
<p>若要指定新 Proxy 伺服器設定的 Identity，請使用如下語法：-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>AcceptClientCompression</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，Proxy 伺服器會接受所有從用戶端端點傳入的壓縮要求。</p></td>
</tr>
<tr class="odd">
<td><p><em>AcceptServerCompression</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，Proxy 伺服器會接受所有從其他伺服器傳入的壓縮要求。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowPartnerPollingSubscribes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，可允許夥伴應用程式定期輪詢服務，以查看狀態變更。預設值為 False ($False)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DisableNtlmFor2010AndLaterClients</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，使用者從 Lync 登入必須使用 Kerberos 通訊協定進行驗證。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>DnsCacheRecordCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>DNS 記錄快取中可保留的記錄數目上限。預設值是 3000。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLoggingAllMessageBodies</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，Microsoft Lync Server 會記錄所有立即訊息的實際內容。基於隱私權，通常會刪除訊息內容，只會在記錄檔中包含通訊端點的資訊。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableWhiteSpaceKeepAlive</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，Proxy 伺服器會預期用戶端定期傳送「空白字元」訊息 (沒有內容的空訊息) 來表示其連線依然在作用中。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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
<td><p>指出是否由預設的 Proxy 伺服器領域 (SIP Communications Service) 或由自訂領域處理安全性認證。必須使用 <strong>New-CsSipProxyCustom</strong> Cmdlet 來指定 (和建立) 自訂領域。</p></td>
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
<td><p>設為 True 時，Proxy 伺服器的運作會好像所有用戶端連線為透過執行 Access Edge Service 的 Edge Server 傳遞之外部連線一樣。預設值為 False。</p></td>
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
<td><p>設為 True (預設值) 時，用戶端端點可以使用 NTLM 通訊協定進行驗證。雖然 NTLM 的安全性低於 Kerberos 通訊協定，但如果用戶端與伺服器分屬於不同網域，它還是可以使用。這種情況不適用於 Kerberos 驗證。</p></td>
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

無。**New-CsProxyConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsProxyConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsProxyConfiguration](get-csproxyconfiguration.md)  
[Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)  
[Set-CsProxyConfiguration](set-csproxyconfiguration.md)

