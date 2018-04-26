---
title: Set-CsUserReplicatorConfiguration
TOCTitle: Set-CsUserReplicatorConfiguration
ms:assetid: 7164960f-8e88-4c8d-9a12-1814aa2b9047
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398540(v=OCS.15)
ms:contentKeyID: 49291283
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUserReplicatorConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改使用者複寫器組態設定的現有集合。使用者複寫器會定期從 Active Directory 網域服務 擷取最新的使用者帳戶資訊，然後將新資訊與 Lync Server 所儲存的目前使用者資料同步。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsUserReplicatorConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsUserReplicatorConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ADDomainNamingContextList <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-ReplicationCycleInterval <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會將全域使用者複寫器設定的 ReplicationCycleInterval 值設為五分鐘 (00 小時: 05分鐘: 00 秒)。

    Set-CsUserReplicatorConfiguration -Identity global -ReplicationCycleInterval "00:05:00"

## 範例 2

範例 2 所示的命令會清除 ADDomainNamingContextList 屬性的值。作法是加入 ADDomainNamingContextList 參數並指定參數值 Null。藉由將此值設定為 Null，使用者複寫器將可自動探索所有可用的網域並進行同步。

    Set-CsUserReplicatorConfiguration -Identity global -ADDomainNamingContextList $Null

## 範例 3

範例 3 將其他名稱新增至通用使用者複寫器設定的 ADDomainNamingContextList 屬性。為了執行這項作業，會使用語法 @{Add=}，以及新增網域的辨別名稱。執行這個命令之後，fabrikam.com 會新增至網域名稱的清單中。若要設定通用設定，讓清單上只有 fabrikam.com，請使用此語法：

\-ADDomainNamingContextList @{Replace="dc=fabrikam,dc=com"}

當 AdDomainNamingContextList 內容已設定為 Null 值以外的任何值時，使用者複寫器將只會與屬性值中所列的網域同步。即使部署中有其他網域，還是會維持此情況。

    Set-CsUserReplicatorConfiguration -Identity global -ADDomainNamingContextList @{Add="dc=fabrikam,dc=com"}

## 範例 4

範例 4 從全域使用者複寫器組態設定的 ADDomainNamingContextList 屬性中移除網域 fabrikam.com。為了執行這項作業，會使用語法 @{Remove=}，以及網域的辨別名稱 (DN) (dc=fabrikam,dc=com)。

    Set-CsUserReplicatorConfiguration -Identity global -ADDomainNamingContextList @{Remove="dc=fabrikam,dc=com"}

## 詳細描述

雖然 Lync Server 會維護它自己的使用者帳戶資料庫和使用者帳戶資料，但 Lync Server 仍依賴 AD DS 做為使用者資訊的基本來源。例如，建立新的 Active Directory 使用者帳戶時，您必須提供關於使用者帳戶的基本資訊 (例如，Active Directory 顯示名稱)。不過，如果使用者已啟用 Lync Server，則無須指定新的顯示名稱。這是因為 Lync Server 會使用已經儲存於 AD DS 中的顯示名稱。

使用者帳戶資訊 (包括 Active Directory 顯示名稱) 會隨著時間的推移而變更。例如，結婚的使用者可能變更姓氏，於是也需要變更其顯示名稱。為了確保 Lync Server 資料庫和 AD DS 保持同步， Lync Server 必須定期檢查 AD DS、擷取最新的使用者帳戶更新，然後據以修改 Lync Server 使用者資料庫。AD DS 和 Lync Server 之間的同步由使用者複寫器負責執行。

安裝 Lync Server 時，會為您建立全域的使用者複寫器組態設定集合。根據預設，這些設定會用來管理整個組織的使用者複寫器。使用者複寫器的管理包含識別 Lync Server 必須同步的網域，以及指出使用者複寫器為使用者帳戶更新檢查 AD DS 的時間頻率。根據預設，使用者複寫器會探索所有可用的網域並進行同步。不過，您可以使用 AdDomainNamingContextList 屬性，將同步化限制為特定的一組網域：出現在 AdDomainNamingContextList 屬性中的網域。

您也可以在服務範圍上建立其他集合，但僅限於使用 Lync Online。

**Set-CsUserReplicatorConfiguration** Cmdlet 可讓您修改目前用於組織的所有使用者複寫器設定。您可以使用這個 Cmdlet，從使用者複寫器必須同步的網域清單中新增或移除網域，以及修改複寫循環之間的時間間隔。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsUserReplicatorConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回已指派此 Cmdlet 的所有 RBAC 角色清單 (包括您自行建立的任何自訂角色型存取控制 (RBAC) 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUserReplicatorConfiguration"}

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
<td><p><em>ADDomainNamingContextList</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>使用者複寫器必須同步之 Active Directory 網域的辨別名稱。例如，若要新增網域至清單，請使用如下語法：</p>
<p>-ADDomainNamingContextList @{Add=&quot;dc=fabrikam,dc=com&quot;}</p>
<p>如果您設定此屬性為 Null 值，則使用者複寫器會探索所有可用的網域並與其同步。如果此內容不為 Null，使用者複寫器將只會與 ADDomainNamingContextList 中指定的網域同步。</p></td>
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
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之使用者複寫器組態設定的唯一識別碼。若要修改全域設定，請使用下列語法：-Identity global.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>UserReplicatorConfiguration 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>ReplicationCycleInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>表示在 AD DS 中檢查使用者帳戶更新之前，使用者複寫器的等待時間。複寫循環間隔可以是 1 秒和 23 小時、59 分和 59 秒之間的任何時間值，預設值為 1 分鐘。間隔必須使用時:分:秒的格式表示。例如，此語法設定時間間隔為 1 小時 15 分：</p>
<p>-ReplicationCycleInterval 01:15:00</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.UserReplicator.UserReplicatorConfiguration 物件。**Set-CsUserReplicatorConfiguration** Cmdlet 接受使用者複寫器組態物件管線傳送的輸入。

## 傳回類型

**Set-CsUserReplicatorConfiguration** Cmdlet 不會傳回任何物件或值，而是修改 Microsoft.Rtc.Management.WritableConfig.Settings.UserReplicator.UserReplicatorConfiguration 物件的全域執行個體 (此類唯一的執行個體)。

## 請參閱

#### 其他資源

[Get-CsUserReplicatorConfiguration](get-csuserreplicatorconfiguration.md)  
[New-CsUserReplicatorConfiguration](new-csuserreplicatorconfiguration.md)  
[Remove-CsUserReplicatorConfiguration](remove-csuserreplicatorconfiguration.md)

