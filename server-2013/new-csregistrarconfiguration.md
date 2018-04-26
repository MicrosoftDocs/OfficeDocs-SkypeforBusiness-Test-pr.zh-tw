---
title: New-CsRegistrarConfiguration
TOCTitle: New-CsRegistrarConfiguration
ms:assetid: 3cd02e36-629f-4ace-841a-1064fc423cfd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425893(v=OCS.15)
ms:contentKeyID: 49290660
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRegistrarConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的登錄器組態設定集合。登錄器可用於驗證登入要求，以及維護使用者狀態與顯示狀態的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRegistrarConfiguration -Identity <XdsIdentity> [-BackupStoreUnavailableThreshold <TimeSpan>] [-Confirm [<SwitchParameter>]] [-DefaultEndpointExpiration <Int32>] [-EnableDHCPServer <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxEndpointExpiration <Int32>] [-MaxEndpointsPerUser <UInt16>] [-MaxUserCount <UInt64>] [-MinEndpointExpiration <Int32>] [-PoolState <FailedOver | Active | FailingOver | FailingBack>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會針對 Redmond 網站 (-Identity site:Redmond)，建立新的登錄器組態設定集合。除了指定新設定的 Identity 之外，此命令也會將每個使用者的端點上限設為 4 (-MaxEndpointsPerUser 4)，並允許使用 DHCP 伺服器進行用戶端登錄 (-EnableDHCPServer $True)。請注意，如果已指派 Redmond 網站登錄器組態設定集合，此命令將會失敗。

    New-CsRegistrarConfiguration -Identity site:Redmond -MaxEndpointsPerUser 4 -EnableDHCPServer $True

## 範例 2

範例 2 所示的命令也會針對 Redmond 網站 (-Identity site:Redmond)，建立新的登錄器組態設定集合。不過，在此範例中，這些設定一開始僅在記憶體中建立，稍後才會套用至網站本身。

為了執行此工作，第一個命令會使用 **New-CsRegistrarConfiguration** Cmdlet 建立 site:Redmond 的新設定集合 (在命令最後加上 InMemory 參數的目的在確保這些設定只會建立在記憶體之中，而不會立即套用到 Redmond 網站)。由於這些設定僅存於記憶體中，因此必須儲存在變數中；在此範例中，變數的名稱為 $x。

在命令 2 和 3 中，這些新虛擬設定的兩個屬性 (MaxEndpointsPerUser 和 EnableDHCPServer) 會經過修改。接著，此範例中的最後一個命令會使用 **Set-CsRegistrarConfiguration** Cmdlet，將儲存在 $x 中的虛擬設定轉換為套用到 Redmond 網站的一組實際登錄器組態設定。如果您沒有呼叫 **Set-CsRegistrarConfiguration** Cmdlet，將不會建立 Redmond 網站的新設定，而且只要您結束 Windows PowerShell 工作階段或刪除變數 $x，虛擬設定就會消失。

    $x = New-CsRegistrarConfiguration -Identity site:Redmond -InMemory 
    $x.MaxEndpointsPerUser = 4 
    $x.EnableDHCPServer = $True
    Set-CsRegistrarConfiguration -Instance $x

## 詳細描述

登錄器可能是 Lync Server 中最重要的元件；畢竟，若無登錄器，使用者將無法登入系統，且 Lync Server 也無法追蹤使用者及其目前的狀態。當使用者登入 Lync Server 時，使用者從中登入的端點會傳送 REGISTER 要求給登錄器；而伺服器則以要求用戶端裝置提出驗證認證做為回應。如果用戶端通過質詢 (亦即，如果用戶端呈現一組有效的認證)，則使用者會通過驗證，並將 IP 位址、連接埠與使用者名稱等端點資訊記錄到登錄資料庫中。當使用者登出時，這項資訊便會從資料庫移除。在登入後與登出前的這段時間，登錄器會保持最新的狀態資訊，並協助路由要給該使用者和該使用者傳來的訊息。

登錄器組態設定用於協助管理端點與端點訂閱；這些設定可以在全域、網站或服務範圍內套用。(服務範圍的設定僅能搭配登錄程式服務使用)。

**New-CsRegistrarConfiguration** Cmdlet 可讓您在網站或服務範圍建立新的登錄器組態設定。請注意，指定的網站或服務最多只能有一個這種設定集合；如果您嘗試將新的集合加到已經主控登錄器組態設定集合的網站或服務，您的命令將會失敗。如果您嘗試在全域範圍建立新設定，您的命令也會失敗。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRegistrarConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRegistrarConfiguration"}

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
<td><p>要建立之登錄器組態設定的唯一識別碼。若要建立在網站範圍設定的設定，請使用類似下列的語法：-Identity site:Redmond。若要建立服務層級的設定，請使用類似下列的語法：-Identity service:Registrar:atl-cs-001.litwareinc.com。請注意，指定的網站或服務最多只能有一個單一的登錄器設定集合。如果您嘗試使用 Identity site:Redmond 建立新的集合，而且 Redmond 網站已經主控登錄器設定集合，則您的命令將會失敗。</p>
<p>此外，您無法在全域範圍建立新的登錄器設定。如果您要在全域範圍變更值，請使用 <strong>Set-CsRegistrarConfiguration</strong> Cmdlet。</p></td>
</tr>
<tr class="even">
<td><p><em>BackupStoreUnavailableThreshold</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指定系統確認備份存放區無法使用之前所需等待的時間。在此情況下，會將使用者置於生存能力模式。預設值為 30 分鐘 (00:30:00)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultEndpointExpiration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>當端點登入時，可以選擇要求等待時間逾時；這會指定在端點必須連絡伺服器並要求擴充前，可以在系統中維持登入狀態的時間間隔。DefaultEndpointExpiration 屬性表示沒有要求特定逾時值之用戶端的等待時間逾時間隔。</p>
<p>DefaultEndpointExpiration 必須介於 300 (5 分鐘) 和 900 (15 分鐘) 之間。預設值為 600 (10 分鐘)。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDHCPServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示端點是否可以使用 DHCP 伺服器尋找登錄程式。若為 True，用戶端將在第一次啟動時傳送 DHCP 通知訊息，而 DHCP 伺服器會傳送可用來登入使用者之登錄器的完整網域名稱 (FQDN) 來回應</p></td>
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
<td><p><em>MaxEndpointExpiration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>端點登入時，會看到要求到期逾時的選項；這個選項能指定端點在必須連絡伺服器並要求延長之前，仍可在系統上保留登入狀態的時間間隔。MaxEndpointExpiration 屬性代表可授與用戶端的時間長度上限。例如，如果時間上限設為 600 秒，而用戶端要求的逾時間隔為 800 秒，則用戶端會獲得下列允許的到期時間上限：600 秒。</p>
<p>MaxEndpointExpiration 必須介於 300 (5 分鐘) 和 900 (15 分鐘) 之間。預設值為 900。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxEndpointsPerUser</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>表示使用者可以同時連線到系統的端點數目上限 (例如，同時使用電腦和行動電話登入 Lync Server 的使用者算使用 2 個端點)。MaxEndpointsPerUser 必須設為介於 1 與 64 (含) 之間的值。預設值為 8。</p>
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
<td><p>端點登入時，會看到要求到期逾時的選項；這個選項能指定端點在必須連絡伺服器並要求延長之前，仍可在系統上保留登入狀態的時間間隔。MinEndpointExpiration 屬性代表可授與用戶端的時間長度下限。例如，如果時間下限設為 600 秒，而用戶端要求的逾時間隔為 200 秒，則用戶端將獲得下列允許的到期時間下限：600 秒。</p>
<p>MinEndpointExpiration 必須介於 300 (5 分鐘) 和 900 (15 分鐘) 之間。預設值為 300。</p></td>
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

無。**New-CsRegistrarConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsRegistrarConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.RegistrarSettings 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsRegistrarConfiguration](get-csregistrarconfiguration.md)  
[Remove-CsRegistrarConfiguration](remove-csregistrarconfiguration.md)  
[Set-CsRegistrarConfiguration](set-csregistrarconfiguration.md)

