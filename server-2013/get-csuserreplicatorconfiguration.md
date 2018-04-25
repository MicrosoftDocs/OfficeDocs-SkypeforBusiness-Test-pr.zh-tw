---
title: Get-CsUserReplicatorConfiguration
TOCTitle: Get-CsUserReplicatorConfiguration
ms:assetid: 7318ae92-e07b-4817-9ec1-be9c7f35aa26
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398548(v=OCS.15)
ms:contentKeyID: 49291305
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUserReplicatorConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織目前所使用之使用者複寫器組態設定的資訊。使用者複寫器會定期從 Active Directory 擷取最新的使用者帳戶資訊，然後同步新資訊與 Lync Server 目前所儲存的使用者資料。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsUserReplicatorConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsUserReplicatorConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回目前用於組織的所有使用者複寫器組態設定資訊。

    Get-CsUserReplicatorConfiguration

## 詳細描述

雖然 Lync Server 會維護它自己的使用者帳戶資料庫和使用者帳戶資料，但 Lync Server 仍依賴 Active Directory 做為使用者資訊的基本來源。例如，建立新的 Active Directory 使用者帳戶時，您必須提供關於使用者帳戶的基本資訊 (例如，Active Directory 顯示名稱)。不過，如果使用者已啟用 Lync Server，則無須為該使用者指定新的顯示名稱。這是因為 Lync Server 會使用已經儲存於 Active Directory 網域服務 中的顯示名稱。

當然，使用者帳戶資訊 (包括 Active Directory 顯示名稱) 會隨著時間的推移而變更。例如，結婚的使用者可能變更姓氏，於是也需要變更其顯示名稱。為了確保 Lync Server 資料庫和 Active Directory 保持同步，Lync Server 必須定期檢查 Active Directory，擷取最新的使用者帳戶更新，並修改本身的使用者資料庫。Active Directory 和 Lync Server 之間的同步由使用者複寫器負執行。

當您安裝 Lync Server 時，系統會為您建立一組全域 User Replicator 組態設定。根據預設，這些設定會用來管理整個組織的 User Replicator。User Replicator 的管理包含識別 Lync Server 必須同步的網域，以及指出 User Replicator 檢查 Active Directory 中是否有使用者帳戶更新的頻率。根據預設，User Replicator 會探索所有可用的網域並進行同步。不過，您可以使用 AdDomainNamingContextList 內容，將同步化限制為特定的一組網域：出現在 AdDomainNamingContextList 內容中的網域。

如果您使用 Lync Server，也可以使用 CsUserReplicatorConfiguration Cmdlet，在服務範圍建立和管理組態設定。不過，若是使用 Lync Server 的內部部署版本，則會受到指派給全域範圍之單一組態設定集合的限制。

系統管理員可使用 **Get-CsUserReplicatorConfiguration** Cmdlet，傳回組織目前使用的所有使用者複寫器設定資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsUserReplicatorConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUserReplicatorConfiguration"}

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
<td><p>可讓您使用萬用字元指定要傳回的使用者複寫器組態設定之集合。例如，下列命令會傳回在服務範圍設定的所有設定：-Filter &quot;service:*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回的使用者複寫器組態設定的唯一識別碼。若要傳回服務範圍的設定，請使用類似下列的語法：-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot; (請注意，唯有當您執行的是 Lync Online，才能使用服務範圍設定)。若要傳回全域設定，請使用下列語法：-Identity global。若未指定此參數，則會傳回目前用於組織的所有使用者複寫器組態設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取使用者複寫器組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsUserReplicatorConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsUserReplicatorConfiguration** Cmdlet 傳回 Microsoft.Rtc.Management.WritableConfig.Settings.UserReplicator.UserReplicatorConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsUserReplicatorConfiguration](new-csuserreplicatorconfiguration.md)  
[Remove-CsUserReplicatorConfiguration](remove-csuserreplicatorconfiguration.md)  
[Set-CsUserReplicatorConfiguration](set-csuserreplicatorconfiguration.md)

