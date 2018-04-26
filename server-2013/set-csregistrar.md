---
title: Set-CsRegistrar
TOCTitle: Set-CsRegistrar
ms:assetid: e0c31acc-179c-4423-910e-8bd7807e6489
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398993(v=OCS.15)
ms:contentKeyID: 49292569
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRegistrar

 

_**上次修改主題的時間：** 2015-03-09_

可讓您修改一或多個登錄器的屬性。登錄器可用於驗證登入要求，以及維護使用者狀態與顯示狀態的資訊。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsRegistrar [-Identity <XdsGlobalRelativeIdentity>] [-ArchivingDatabase <String>] [-ArchivingServer <String>] [-BackupRegistrar <String>] [-Confirm [<SwitchParameter>]] [-EdgeServer <String>] [-EnableAutomaticFailover <$true | $false>] [-FailbackDetectionInterval <TimeSpan>] [-FailureDetectionInterval <TimeSpan>] [-Force <SwitchParameter>] [-LyssWcfMtlsPort <UInt16>] [-MirrorArchivingDatabase <String>] [-MirrorMonitoringDatabase <String>] [-MonitoringDatabase <String>] [-MonitoringServer <String>] [-Registrar <String>] [-SipHealthPort <UInt16>] [-SipPort <UInt16>] [-SipServerTcpPort <UInt16>] [-UserServer <String>] [-WebPort <UInt16>] [-WebServer <String>] [-WhatIf [<SwitchParameter>]] [-WinFabClientConnectionPort <UInt16>] [-WinFabFederationPort <UInt16>] [-WinFabIPCPort <UInt16>] [-WinFabLeaseAgentPort <UInt16>] [-WinFabReplicationPort <UInt16>] [-XmppGatewaySipPort <UInt16>]

## 範例

## 範例 1

範例 1 所示的命令會將登錄器 Registrar:atl-cs-001.litwareinc.com 的 SIP 連接埠設定為 5072。

    Set-CsRegistrar -Identity "Registrar:atl-cs-001.litwareinc.com" -SipPort 5072

## 範例 2

範例 2 會將組織內所有登錄器的 SIP 連接埠設定為 5072。為達成此目的，命令會先使用 **Get-CsService** Cmdlet 搭配 Registrar 參數，以傳回目前使用之所有登錄器的集合。然後，此集合會管線傳送到 **ForEach-Object** Cmdlet，以取得集合中的每一個登錄器，並執行 **Set-CsRegistrar** Cmdlet，將 SIP 連接埠變更為 5072。

    Get-CsService -Registrar | ForEach-Object {Set-CsRegistrar -Identity $_.Identity -SipPort 5072}

## 範例 3

範例 3 會設定登錄器 Registrar:atl-cs-001.litwareinc.com 的備份登錄器 (BackupRegistrar) 與自動容錯移轉 (EnableAutomaticFailover) 兩者。

    Set-CsRegistrar -Identity "Registrar:atl-cs-001.litwareinc.com" -BackupRegistrar "Registrar:dublin-cs-001.litwareinc.com" -EnableAutomaticFailover $True

## 詳細描述

登錄器可能是 Lync Server 中最重要的元件；畢竟，若無登錄器，使用者將無法登入系統，且 Lync Server 也無法追蹤使用者及其目前的狀態。當使用者登入 Lync Server 時，使用者登入的端點 (可能是電腦、行動電話或其他裝置) 會將 REGISTER 要求傳送至註冊伺服器；而伺服器藉由挑戰驗證認證的用戶端裝置進行回應。如果用戶端通過此挑戰 (即用戶端出示一組有效認證)，則使用者通過驗證，而且端點資訊 (例如 IP 位址、連接埠和使用者名稱) 會記錄到註冊資料庫中。當使用者登出時，這項資訊便會從資料庫移除。在登入後與登出前的這段時間，登錄器會保持最新的狀態資訊，並協助路由要給該使用者和該使用者傳來的訊息。

**Set-CsRegistrar** Cmdlet 提供您修改您組織中一或多個登錄器屬性的方法。這些修改包含變更連接埠設定，並指定若登錄器無法使用時應採取的動作。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsRegistrar** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRegistrar\\b"}

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
<td><p><em>ArchivingDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>Archiving Service 所使用之資料庫的服務識別。</p></td>
</tr>
<tr class="even">
<td><p><em>ArchivingServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與登錄器相關聯之 封存伺服器 的服務位置。例如：-ArchivingServer &quot;ArchivingServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>BackupRegistrar</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>若此登錄器無法使用，要使用之登錄器的服務位置。例如：-BackupRegistrar &quot;Registrar:dublin-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EdgeServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與登錄器相關聯之 Edge Server 的服務位置。例如：-EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableAutomaticFailover</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，當主要登錄器無法使用時，便會使用備份登錄器。若為 False，當主要登錄器無法使用時，不會使用備份登錄器。</p>
<p>此參數也會影響已使用備份登錄器註冊的使用者。如果此參數設定為 True，則會從備份登錄器捨棄這些使用者，若可使用該登錄器時，將在主要登錄器上重新註冊。</p></td>
</tr>
<tr class="odd">
<td><p><em>FailbackDetectionInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指定系統在檢查以查看變成無法使用的登錄器現在是否可以使用之前將等候的時間長度。如果您已將 EnableAutomaticFailover 設為 True，系統隨時會在登錄器變成無法使用時「容錯移轉」至備份登錄器。這只是表示系統將接管已登入失敗登錄器的使用者，並嘗試讓他們登入備份登錄器。</p>
<p>FailbackDetectionInterval 內容會指定系統在檢查以查看原本的登錄器是否可再次使用之前將等候的時間長度。如果可用， Lync Server 接著將嘗試「容錯回復」至該登錄器。「容錯回復」只是表示回復為最初使用的登錄器；換句話說，讓使用者登入回到其原本的登錄器。</p>
<p>請注意，容錯回復是一項只能自動進行的程序。您無法手動從一個登錄器容錯回復至另一個登錄器。</p>
<p>偵測時間間隔可設定為介於 30 秒至 84,400 秒 (24 小時) 之間的任何值；請使用「小時:分鐘:秒」格式來指定時間範圍。例如，這會設定時間間隔為 1 小時 15 分：- FailbackDetectionInterval 01:15:00。</p>
<p>除非您已指定了備份登錄器，否則無法使用此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>FailureDetectionInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指定在決定登錄器無法使用時，系統將等候的時間間隔。如果已將 EnableAutomaticFailover 設定為 True，則系統將嘗試讓使用者改為登入備份登錄器。</p>
<p>偵測時間間隔可設定為介於 30 秒至 84,400 秒 (24 小時) 之間的任何值；請使用「小時:分鐘:秒」格式來指定時間範圍。例如，這會設定時間間隔為 1 小時 15 分：- FailureDetectionInterval 01:15:00。</p>
<p>除非您已指定了備份登錄器，否則無法使用此參數。</p></td>
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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改的登錄器服務位置。例如：-Identity &quot;Registrar:atl-cs-001.litwareinc.com&quot;。</p>
<p>請注意，當您在指定登錄器時，可以省略首碼 &quot;Registrar:&quot;。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>LyssWcfMtlsPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Lync Storage Service (LYSS) 所使用的連接埠。預設值為 5077。</p></td>
</tr>
<tr class="even">
<td><p><em>MirrorArchivingDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>Archiving Service 所使用之鏡像資料庫的服務識別。</p></td>
</tr>
<tr class="odd">
<td><p><em>MirrorMonitoringDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>Monitoring Service 所使用之鏡像資料庫的服務識別。</p></td>
</tr>
<tr class="even">
<td><p><em>MonitoringDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與登錄器相關聯之監控資料庫的服務識別。</p></td>
</tr>
<tr class="odd">
<td><p><em>MonitoringServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與登錄器相關聯之 監控伺服器 的服務位置。例如：-MonitoringServer &quot;MonitoringServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Registrar</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>登錄器的服務位置。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipHealthPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於監視伺服器狀況的連接埠。</p></td>
</tr>
<tr class="even">
<td><p><em>SipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於 SIP (工作階段初始通訊協定) 流量的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipServerTcpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>SIP 聆聽連接埠。預設值為 5060。</p></td>
</tr>
<tr class="even">
<td><p><em>UserServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與登錄器相關聯之 使用者服務 伺服器的服務位置。例如：-UserServer &quot;UserServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>WebPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於與 Web 伺服器進行通訊的連接埠。</p></td>
</tr>
<tr class="even">
<td><p><em>WebServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與登錄器相關聯之 Web 伺服器的服務位置。例如：-WebServer &quot;WebServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
<tr class="even">
<td><p><em>WinFabClientConnectionPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於 Windows Fabric 之用戶端連線的連接埠。預設值為 5092。</p></td>
</tr>
<tr class="odd">
<td><p><em>WinFabFederationPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於 Windows Fabric 同盟的連接埠。同盟是指 Windows Fabric 路由訊息的程序。預設值為 5090。</p></td>
</tr>
<tr class="even">
<td><p><em>WinFabIPCPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Windows Fabric 用於處理序間通訊 (IPC) 的連接埠。IPC 是可讓程序中多個執行緒交換資料的技術。預設值為 5093。</p></td>
</tr>
<tr class="odd">
<td><p><em>WinFabLeaseAgentPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Windows Fabric 租用代理使用的連接埠。租用代理可用來與核心層級的租用驅動程式互動。預設值為 5091。</p></td>
</tr>
<tr class="even">
<td><p><em>WinFabReplicationPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於 Windows Fabric 複寫的連接埠。 Lync Server 2013使用 Windows Fabric 將會議目錄複寫至登錄器集區內的所有前端伺服器。預設值為 5094。</p></td>
</tr>
<tr class="odd">
<td><p><em>XmppGatewaySipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>與登錄器相關聯之 XMPP 閘道使用的連接埠。Extensible Messaging and Presence Protocol (XMPP) 是使用 XML 交換訊息的開放標準通訊協定。允許的合作夥伴是指 IM 和目前狀態提供者，其使用者可與您的 Lync Server 使用者交換立即訊息和目前狀態資訊。預設值為 5098。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Set-CsRegistrar** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsRegistrar** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.Xds.DisplayRegistrar 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsService](get-csservice.md)

