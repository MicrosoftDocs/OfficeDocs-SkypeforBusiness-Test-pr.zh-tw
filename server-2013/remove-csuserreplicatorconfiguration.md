---
title: Remove-CsUserReplicatorConfiguration
TOCTitle: Remove-CsUserReplicatorConfiguration
ms:assetid: 26c3a357-558f-406f-8df3-059911f771f0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425738(v=OCS.15)
ms:contentKeyID: 49290387
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUserReplicatorConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的使用者複寫器組態設定集合。使用者複寫器會定期從 Active Directory 擷取最新的使用者帳戶資訊，然後同步新資訊與 Lync Server 目前所儲存的使用者資料。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsUserReplicatorConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會重設全域使用者複寫器組態設定。

    Remove-CsUserReplicatorConfiguration -Identity global

## 詳細描述

雖然 Lync Server 可保留自己的使用者帳戶資料庫和使用者帳戶資料，但 Lync Server 仍依賴 Active Directory 做為使用者資訊的基本來源。例如，建立新的 Active Directory 使用者帳戶時，您必須提供關於使用者帳戶的基本資訊 (例如，Active Directory 顯示名稱)。不過，使用者已啟用 Lync Server 時，您不需要指定新的顯示名稱。這是因為 Lync Server 使用 Active Directory 中已儲存的顯示名稱。

當然，使用者帳戶資訊 (包括 Active Directory 顯示名稱) 會隨著時間而變更。例如，結婚的使用者可能變更姓氏，於是也需要變更其顯示名稱。為了確保 Lync Server 資料庫和 Active Directory 保持同步，Lync Server 必須定期連線至 Active Directory、擷取最新的使用者帳戶更新，並隨之修改 Lync Server 使用者資料庫。Active Directory 和 Lync Server 之間的同步由使用者複寫器負責執行。

當您安裝 Lync Server 時，系統會為您建立一組全域使用者複寫器組態設定。根據預設，這些設定會用來管理整個組織的使用者複寫器。使用者複寫器的管理包含識別 Lync Server 必須同步的網域，以及指出使用者複寫器檢查 Active Directory 中是否有使用者帳戶更新的頻率。根據預設，使用者複寫器會探索所有可用的網域並進行同步。不過，您可以使用 AdDomainNamingContextList 屬性，將同步化限制為特定的一組網域：出現在 AdDomainNamingContextList 屬性中的網域。

您也可以在服務範圍上建立其他集合，但僅限於使用 Lync Online。

如果您需要變更，可以使用 **Remove-CsUserReplicatorConfiguration** Cmdlet 移除在服務範圍建立的自訂設定。請注意，您也可以針對全域組態設定執行此 Cmdlet。不過，在該情況下，將不會移除全域設定。而是會將全域集合內的所有屬性都重設為預設值。就 User Replicator 而言，這表示清除必須同步的網域清單 (因此讓複寫器與所有可探索的網域同步)，並將複寫間隔週期設為 1 分鐘。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsUserReplicatorConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUserReplicatorConfiguration"}

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
<td><p>要移除之使用者複寫器組態設定的唯一識別碼。若要在服務範圍移除設定，請使用如下的語法：-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;。(請注意，如果您使用 Lync Online，則只能移除服務範圍的設定)。若要重設全域設定，請使用下列語法：-Identity global。在指定 Identity 時無法使用萬用字元。</p></td>
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
<td><p>抑制顯示執行命令時可能引起的任何非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.UserReplicator.UserReplicatorConfiguration 物件。**Remove-CsUserReplicatorConfiguration** Cmdlet 接受管線傳送的 User Replicator 組態物件輸入。

## 傳回類型

無。反之，**Remove-CsUserReplicatorConfiguration** Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.UserReplicator.UserReplicatorConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsUserReplicatorConfiguration](get-csuserreplicatorconfiguration.md)  
[New-CsUserReplicatorConfiguration](new-csuserreplicatorconfiguration.md)  
[Set-CsUserReplicatorConfiguration](set-csuserreplicatorconfiguration.md)

