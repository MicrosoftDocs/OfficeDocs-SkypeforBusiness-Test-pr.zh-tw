---
title: Get-CsService
TOCTitle: Get-CsService
ms:assetid: f687d41b-2cb3-4c32-ae28-90e25cdd0d6a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413038(v=OCS.15)
ms:contentKeyID: 49292830
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsService

 

_**上次修改主題的時間：** 2015-03-09_

傳回 Lync Server 基礎結構中所使用的服務和伺服器角色相關資訊。服務是已部署於 Lync Server 集區中角色的執行個體。例如，您可能有一個所有電腦都執行監控服務的電腦集區。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsService [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsService [-ApplicationServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-ApplicationDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-ArchivingServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-ArchivingDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-BackupServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-CentralManagement <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-CentralManagementDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-ConferencingServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-Director <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-EdgeServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-TrustedApplicationPool <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-FileStore <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-PersistentChatServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-PersistentChatComplianceDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-PersistentChatDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-LegalInterceptServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-ManagementServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-MediationServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-MonitoringServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-MonitoringDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-PstnGateway <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-Registrar <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-UserServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-UserDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-WacServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-WebServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-PoolFqdn <String>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織中目前正在執行的所有 Lync Server 服務和伺服器角色相關資訊。

    Get-CsService

## 範例 2

範例 2 只會傳回 應用程式服務 的資訊。只需使用適當的參數，即可傳回其他服務/伺服器角色的資訊。例如，此命令會傳回檔案存放區的資訊：

    Get-CsService -ApplicationServer

## 範例 3

範例 3 會回報每個位於 atl-cs-001.litwareinc.com 集區之服務的 Identity。為達成此目的，命令會先呼叫 **Get-CsService** Cmdlet 搭配 PoolFqdn 參數，以傳回在 atl-cs-001.litwareinc.com 集區找到的服務和伺服器角色。然後再將集合管線傳送到 **Select-Object** Cmdlet，以回報集合中每個項目的 Identity。

    Get-CsService -PoolFqdn "atl-cs-001.litwareinc.com" | Select-Object Identity

## 範例 4

範例 4 會傳回所有在 Redmond 網站找到的服務/伺服器角色資訊。作法是先呼叫 **Get-CsService** Cmdlet 而不搭配任何參數，以傳回組織目前使用之所有服務和伺服器角色的集合。然後將此資料以管線傳送到 **Where-Object** Cmdlet，這會只挑出 SiteID 屬性等於 site:Redmond 的項目。

    Get-CsService | Where-Object {$_.SiteID -eq "site:Redmond"}

## 範例 5

範例 5 所示的命令會傳回將登錄器列為相依服務的所有服務相關資訊。為達成此目的，會呼叫 **Get-CsService** Cmdlet 傳回目前所使用之所有服務和伺服器角色的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以選取 DependentServiceList 屬性包含字串值 "Registrar" 的每個項目。 **Where-Object** Cmdlet 準則可以使用 -like 運算子和萬用字元值 "\*Registrar\*" 加以指定。

    Get-CsService | Where-Object {$_.DependentServiceList -like "*Registrar*"}

## 詳細描述

可以在 Lync Server 中找到的功能，通常會以服務或伺服器角色的形態出現。例如，您可以設定 Lync Server 自動儲存組織中所發生之各個立即訊息工作階段的記錄。若要執行此作業，必須安裝 封存伺服器 伺服器角色。服務和伺服器角色可以在您安裝 Lync Server 的同時加以設定，或者在啟動和執行該軟體之後再行設定。

**Get-CsService** Cmdlet 讓您能夠傳回組織內所執行之伺服器角色及服務的資訊。若呼叫時未指定任何其他參數， **Get-CsService** Cmdlet 便會傳回有關您所有服務和伺服器角色的詳細資訊。或者，您可以使用 PoolFqdn 參數，將傳回的資料限制為指定的集區。此外，可以使用任意數量的切換參數，將傳回的資料限制為特定類型的服務 切換參數是不需要參數值的參數。例如，下列命令會傳回有關您所有封存伺服器的資訊：

Get-CsService –ArchivingServer

請注意，每個命令只能使用一個這類切換參數。下列命令嘗試同時傳回封存伺服器和監控伺服器的資訊，因而將會失敗：

Get-CsService –ArchivingServer –MonitoringServer

若要傳回多個伺服器角色的資訊，您可以使用 **Get-CsService** Cmdlet 傳回服務資料的完整集合，然後將該資料傳送到 **Where-Object** Cmdlet：

Get-CsService | Where-Object {$\_.Role –eq "ArchivingServer" –or $\_.Role –eq "MonitoringServer"}

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsService** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsService"}

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
<td><p><em>ApplicationDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之應用程式資料庫的資訊。應用程式資料庫是由 應用程式服務 所使用。</p></td>
</tr>
<tr class="even">
<td><p><em>ApplicationServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回 應用程式服務 的資訊。 應用程式服務 可讓執行 Microsoft Unified Communications Managed API (UCMA) 所建立的應用程式。</p></td>
</tr>
<tr class="odd">
<td><p><em>ArchivingDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之封存資料庫的資訊。封存資料庫會儲存立即訊息工作階段的記錄。</p></td>
</tr>
<tr class="even">
<td><p><em>ArchivingServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之封存伺服器的資訊。封存伺服器讓您能夠儲存立即訊息工作階段的記錄。</p></td>
</tr>
<tr class="odd">
<td><p><em>BackupServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之備份伺服器的資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>CentralManagement</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之 中央管理服務的資訊。系統使用 中央管理服務將組態資料傳送至執行 Lync Server 服務的電腦。</p></td>
</tr>
<tr class="odd">
<td><p><em>CentralManagementDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之 中央管理存放區 的資訊。 中央管理存放區 會為 Lync Server 保留組態資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>ConferencingServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之 音訊/視訊會議服務 的資訊。系統使用 音訊/視訊會議服務 進行會議。</p></td>
</tr>
<tr class="odd">
<td><p><em>Director</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之 Director 的資訊。Director 有權處理使用者要求和使用者驗證，但不會保留使用者帳戶。Director 通常可用來處理外部使用者的要求。</p></td>
</tr>
<tr class="even">
<td><p><em>EdgeServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之 Edge Server 的資訊。Edge Server 提供內部網路與網際網路之間的連線。</p></td>
</tr>
<tr class="odd">
<td><p><em>FileStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之檔案存放區的資訊。檔案存放區可以用來保留 Lync Server 檔案，例如，宣告服務所使用的音訊檔案。</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>讓您能夠使用萬用字元來指定要傳回的服務 (或多個服務)。您無法在同一個命令中同時使用 Identity 和 Filter 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回之特定服務或伺服器角色的唯一識別碼。例如：-Identity &quot;Registrar:atl-cs-001.litwareinc.com&quot;。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>LegalInterceptServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之 Legal Intercept Server 的資訊。Legal Intercept Server 提供 Office 365 之立即訊息通訊的即時攔截。</p></td>
</tr>
<tr class="odd">
<td><p><em>ManagementServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之 中央管理伺服器 的資訊。通常會與前端伺服器一起收集 中央管理伺服器，且該伺服器負責存取 中央管理存放區 中的資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>MediationServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之中繼伺服器的資訊。中繼伺服器可協助提供介於 Enterprise Voice 網路與公用交換電話網路 (PSTN) 之間的橋接器。</p></td>
</tr>
<tr class="odd">
<td><p><em>MonitoringDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之監控資料庫的資訊。監控資料庫會儲存 Enterprise Voice 電話使用方式和通話品質資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>MonitoringServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之監控伺服器的資訊。監控伺服器可用來追蹤 Enterprise Voice 電話使用方式和通話品質。</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatComplianceDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回用於維護常設聊天室規範資訊之資料庫的資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>PersistentChatDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回用於維護常設聊天室資訊之資料庫的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之 Persistent Chat Server 的資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>PoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>裝載服務或伺服器角色之集區的完整網域名稱 (FQDN)。如果使用 PoolFqdn 參數且未指定服務特定的參數，則將傳回可在該集區中找到的所有服務和伺服器角色。</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnGateway</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用的公用交換電話網路 (PSTN) 閘道相關資訊。PSTN 閘道會將來自 Enterprise Voice 裝置的信號轉譯為 PSTN 裝置能瞭解的信號，反之亦然。</p></td>
</tr>
<tr class="even">
<td><p><em>Registrar</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之登錄器的資訊。登錄器可用來驗證使用者，並持續追蹤使用者的目前狀態。</p></td>
</tr>
<tr class="odd">
<td><p><em>TrustedApplicationPool</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之信任應用程式集區的資訊。信任的應用程式集區主控執行信任的應用程式之電腦。</p></td>
</tr>
<tr class="even">
<td><p><em>UserDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之 使用者資料庫 的資訊。使用者資料庫會儲存使用者伺服器服務所需的資料。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之 使用者服務 服務的資訊。 使用者服務 服務提供諸如下列的資訊：使用者複寫、In-Band 佈建、目前狀態發行與通知，以及連絡人卡片交換。</p></td>
</tr>
<tr class="even">
<td><p><em>WacServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回搭配 Microsoft Lync Server 使用之 Office Online Server 的資訊。Office Online Server 之前稱為 &quot;WacServer&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>WebServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組織所使用之 Web 服務 服務的資訊。 Web 服務 服務會主控諸如通訊錄服務的 Web 應用程式。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsService** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsService** Cmdlet 會根據呼叫 Cmdlet 時所使用的參數，傳回不同的物件。例如，如果您加入 MonitoringDatabase 參數， **Get-CsService** Cmdlet 會傳回 Microsoft.Rtc.Management.Xds.DisplayMonitoringDatabase 物件的執行個體。若要判斷使用其他參數傳回的物件，可使用這其中一個參數來呼叫 **Get-CsService** Cmdlet，然後將傳回的物件管線傳送到 **Get-Member** Cmdlet。例如：Get-CsService -Registrar | Get-Member。

## 請參閱

#### 其他資源

[Set-CsApplicationServer](set-csapplicationserver.md)  
[Set-CsArchivingServer](set-csarchivingserver.md)  
[Set-CsConferenceServer](set-csconferenceserver.md)  
[Set-CsDirector](set-csdirector.md)  
[Set-CsEdgeServer](set-csedgeserver.md)  
[Set-CsManagementServer](set-csmanagementserver.md)  
[Set-CsMediationServer](set-csmediationserver.md)  
[Set-CsMonitoringServer](set-csmonitoringserver.md)  
[Set-CsRegistrar](set-csregistrar.md)  
[Set-CsUserServer](set-csuserserver.md)  
[Set-CsWebServer](set-cswebserver.md)

