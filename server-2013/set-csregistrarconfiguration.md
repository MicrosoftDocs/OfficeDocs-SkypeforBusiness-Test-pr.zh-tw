---
title: Set-CsRegistrarConfiguration
TOCTitle: Set-CsRegistrarConfiguration
ms:assetid: 9616b967-09dd-470d-8d0a-acce1ff4fbf9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398764(v=OCS.15)
ms:contentKeyID: 49291736
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRegistrarConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有登錄器組態設定集合中的屬性值。登錄器可用於驗證登入要求，以及維護使用者狀態與顯示狀態的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsRegistrarConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsRegistrarConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BackupStoreUnavailableThreshold <TimeSpan>] [-Confirm [<SwitchParameter>]] [-DefaultEndpointExpiration <Int32>] [-EnableDHCPServer <$true | $false>] [-Force <SwitchParameter>] [-MaxEndpointExpiration <Int32>] [-MaxEndpointsPerUser <UInt16>] [-MaxUserCount <UInt64>] [-MinEndpointExpiration <Int32>] [-PoolState <FailedOver | Active | FailingOver | FailingBack>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會修改已套用至 Redmond 網站的登錄器組態設定 (-Identity site:Redmond)。在此範例中，EnableDHCPServer 屬性的值設為 True。

    Set-CsRegistrarConfiguration -Identity site:Redmond -EnableDHCPServer $True

## 範例 2

範例 2 會修改允許使用者具有超過 8 個端點的登錄器組態設定。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsRegistrarConfiguration** Cmdlet，以傳回組織所使用之所有登錄器組態設定的集合。然後再將此集合管線傳送至 **Where-Object** Cmdlet，這會只挑出 MaxEndpointsPerUser 屬性大於 (-gt) 8 的設定。最後將篩選後的集合管線傳送至 **Set-CsRegistrarConfiguration** Cmdlet，以將該集合中每個項目的端點數上限都設為 8。

    Get-CsRegistrarConfiguration | Where-Object {$_.MaxEndpointsPerUser -gt 8} | Set-CsRegistrarConfiguration -MaxEndpointsPerUser 8

## 範例 3

範例 3 所示的命令會針對組織中裝載登錄器組態設定集合的每個網站，停用透過 DHCP 的用戶端登錄。為達成此目的，命令會呼叫 **Get-CsRegistrarConfiguration** Cmdlet 並搭配 Filter 參數 (參數值 "site:\*" 可將傳回的資料限制在網站範圍設定的設定)。然後，此集合會管線傳送到 **Set-CsRegistrarConfiguration** Cmdlet，以使用 EnableDHCPServer 參數和 $False 參數值，防止用戶端使用 DHCP 伺服器尋找登錄器。

    Get-CsRegistrarConfiguration -Filter "site:*"| Set-CsRegistrarConfiguration -EnableDHCPServer $False

## 詳細描述

登錄器可能是 Lync Server 中最重要的元件；畢竟，若無登錄器，使用者將無法登入系統，且 Lync Server 也無法追蹤使用者及其目前的狀態。當使用者登入 Lync Server 時，使用者從中登入的端點會傳送 REGISTER 要求給登錄器；而伺服器則以要求用戶端裝置提出驗證認證做為回應。如果用戶端通過此挑戰 (即用戶端出示一組有效認證)，則使用者通過驗證，而且端點資訊 (例如 IP 位址、連接埠和使用者名稱) 會記錄到註冊資料庫中。當使用者登出時，這項資訊便會從資料庫移除。在登入後與登出前的這段時間，登錄器會保持最新的狀態資訊，並協助路由要給該使用者和該使用者傳來的訊息。

登錄器組態設定用於協助管理端點與端點訂閱；這些設定可以在全域、網站或服務範圍內套用。(服務範圍設定只與登錄器服務搭配使用)。**Set-CsRegistrarConfiguration** Cmdlet 可以用來修改您組織中目前使用的任何 (或所有) 登錄器組態集合。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsRegistrarConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRegistrarConfiguration"}

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
<td><p><em>BackupStoreUnavailableThreshold</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指定系統確認備份存放區無法使用之前所需等待的時間。在此情況下，會將使用者置於生存能力模式。預設值為 30 分鐘 (00:30:00)。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultEndpointExpiration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>端點登入時，會看到要求到期逾時的選項；這個選項能指定端點在必須聯絡伺服器並要求延長之前，仍可在系統上保留登入狀態的時間間隔。DefaultEndpointExpiration 屬性代表當用戶端不要求特定逾時值時的到期逾時間隔。</p>
<p>DefaultEndpointExpiration 必須介於 300 (5 分鐘) 與 900 (15 分鐘) 之間。預設值為 600 (10 分鐘)。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDHCPServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示端點是否可以使用 DHCP 伺服器來尋找登錄器。若為 True，用戶端將在第一次啟動時傳送 DHCP 通知訊息，而 DHCP 伺服器會傳送可用來登入使用者之登錄器的完整網域名稱 (FQDN) 來回應</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之登錄器組態設定的唯一識別碼。若要修改全域設定，請使用下列語法：-Identity global。若要修改在網站範圍設定的設定值，請使用下列語法：-Identity site:Redmond。若要修改服務層級的設定，請使用下列語法：-Identity service:Registrar:atl-cs-001.litwareinc.com。請注意，登錄器設定只能套用至登錄器服務。如果嘗試將這些設定套用至任何其他服務，將發生錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>RegistrarSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEndpointExpiration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>端點登入時，會看到要求到期逾時的選項；這個選項能指定端點在必須聯絡伺服器並要求延長之前，仍可在系統上保留登入狀態的時間間隔。MaxEndpointExpiration 屬性代表可以授與用戶端的時間長度上限。例如，如果時間上限設為 600 秒，而用戶端要求 800 秒的逾時間隔，則用戶端將獲得最高允許的到期時間：600 秒。</p>
<p>MaxEndpointExpiration 必須介於 300 (5 分鐘) 與 900 (15 分鐘) 之間。預設值為 900。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxEndpointsPerUser</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>表示使用者可以同時用來連接至系統的端點數上限。例如，同時使用電腦和行動電話登入 Lync Server 的使用者算使用兩個端點。MaxEndPointsPerUser 必須設為介於 1 與 64 (含) 之間的值。預設值為 8。</p>
<p>雖然一個使用者可允許最多 64 個端點，但仍建議端點數目上限不要超過 8。在極少數的情況下，Microsoft 支援部門的人員會建議 9 或以上的值，以用於回溯相容性。對於新的部署，端點數目上限應不超過 8。</p>
<p>請注意，端點數目上限的用意是讓個別使用者有多個顯示端點。確切來說，此設定是專為個別使用者所設計，而非群組使用者 (例如整個部門)。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxUserCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>指定可以同時登入登錄器的使用者人數上限。MaxUserCount 可以設為 2000 到 100000 (含) 之間的任意整數值。預設值為 12000。</p></td>
</tr>
<tr class="odd">
<td><p><em>MinEndpointExpiration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>端點登入時，會看到要求到期逾時的選項；這個選項能指定端點在必須聯絡伺服器並要求延長之前，仍可在系統上保留登入狀態的時間間隔。MinEndpointExpiration 屬性代表可以授與用戶端的時間長度下限。例如，如果時間下限設為 600 秒，而用戶端要求 200 秒的逾時間隔，則用戶端將獲得最低允許的到期時間：600 秒。</p>
<p>MinEndpointExpiration 必須介於 300 (5 分鐘) 與 900 (15 分鐘) 之間。預設值為 300。</p></td>
</tr>
<tr class="even">
<td><p><em>PoolState</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.PoolState</p></td>
<td><p>登錄器集區的目前狀態。允許的值為：</p>
<p>* Active</p>
<p>* FailedOver</p>
<p>* FailingOver</p>
<p>* FailedBack</p>
<p>預設值為 Active。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.RegistrarSettings 物件。**Set-CsRegistrarConfiguration** Cmdlet 接受管線傳送的登錄器設定物件執行個體。

## 傳回類型

**Set-CsRegistrarConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.RegistrarSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsRegistrarConfiguration](get-csregistrarconfiguration.md)  
[New-CsRegistrarConfiguration](new-csregistrarconfiguration.md)  
[Remove-CsRegistrarConfiguration](remove-csregistrarconfiguration.md)

