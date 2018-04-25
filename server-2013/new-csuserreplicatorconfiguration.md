---
title: New-CsUserReplicatorConfiguration
TOCTitle: New-CsUserReplicatorConfiguration
ms:assetid: eb4dee9e-9ba4-4726-8f7c-b355433ed594
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399059(v=OCS.15)
ms:contentKeyID: 49292700
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsUserReplicatorConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的使用者複寫器組態設定的集合。使用者複寫器定期從 Active Directory 擷取最新的使用者帳戶資訊，然後將新資訊與 Lync Server 所儲存的現行使用者資料同步。此 Cmdlet 旨在搭配 Lync Online 使用，無法與 Lync Server 的內部部署版本共同作業。

## 語法

    New-CsUserReplicatorConfiguration -Identity <XdsIdentity> [-ADDomainNamingContextList <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-ReplicationCycleInterval <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會針對服務 Registrar:atl-cs-001.litwareinc.com 建立使用者複寫器組態設定的新集合。由於未指定其他參數，因此新集合將會使用預設的使用者複寫器值。

    New-CsUserReplicatorConfiguration -Identity "service:Registrar:atl-cs-001.litwareinc.com"

## 範例 2

範例 2 也會針對服務 Registrar:atl-cs-001.litwareinc.com 建立使用者複寫器組態設定的新集合。但是，在此案例中，會新增 ADDomainNamingContextList，以及要進行同步處理之兩個網域的辨別名稱：fabrikam.com 及 contoso.com。即使沒有其他可用的網域，使用者複寫器組態設定的此新集合也僅會利用這兩個網域進行設定。

    New-CsUserReplicatorConfiguration -Identity "service:Registrar:atl-cs-001.litwareinc.com" -ADDomaiNamingContextList @{Add="dc=fabrikam,dc=com","dc=contoso.com"}

## 詳細描述

雖然 Lync Server 會維護它自己的使用者帳戶資料庫和使用者帳戶資料，但 Lync Server 仍依賴 Active Directory 做為使用者資訊的基本來源。例如，建立新的 Active Directory 使用者帳戶時，您必須提供關於使用者帳戶的基本資訊 (例如，Active Directory 顯示名稱)。不過，如果使用者已啟用 Lync Server，則無需指定新的顯示名稱。這是因為 Lync Server 使用 Active Directory 中已儲存的顯示名稱。

使用者帳戶資訊 (包括 Active Directory 顯示名稱) 會隨著時間的推移而變更。例如，結婚的使用者可能變更姓氏，於是也需要變更其顯示名稱。為了確保 Lync Server 資料庫和 Active Directory 保持同步， Lync Server 必須定期檢查 Active Directory、擷取最新的使用者帳戶更新，並隨之修改 Lync Server 使用者資料庫。Active Directory 和 Lync Server 之間的同步由使用者複寫器負責執行。

當您安裝 Lync Server 時，系統會為您建立一組全域 User Replicator 組態設定。根據預設，這些設定會用來管理整個組織的 User Replicator。User Replicator 的管理包含識別 Lync Server 必須同步的網域，以及指出 User Replicator 檢查 Active Directory 中是否有使用者帳戶更新的頻率。您也可以在服務範圍上建立其他集合，但僅限於使用 Lync Online。

新的使用者複寫器組態設定是使用 **New-CsUserReplicatorConfiguration** Cmdlet 所建立。請注意，設定僅能於服務範圍內設定，而且只能針對 Lync Online 建立。您無法針對 Lync Server 的內部部署版本建立新的使用者複寫器設定。

誰可以執行這個 Cmdlet：根據預設，下列群組成員已獲得授權，可以執行 **New-CsUserReplicatorConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsUserReplicatorConfiguration"}

``` 
```

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
<td><p>要建立之使用者複寫器組態設定的唯一識別碼。設定僅能於服務範圍內設定，而且只能針對登錄器服務建立。這表示新設定必須具備類似下列的 Identity：-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;。</p>
<p>請注意，這僅適用於 Lync Server。</p></td>
</tr>
<tr class="even">
<td><p><em>ADDomainNamingContextList</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>使用者複寫器必須同步之 Active Directory 網域的辨別名稱。例如，若要新增網域至清單，請使用如下語法：</p>
<p>-ADDomainNamingContextList @{Add=&quot;dc=fabrikam,dc=com&quot;}</p>
<p>呼叫 <strong>New-CsUserReplicatorConfiguration</strong> Cmdlet 時，可以加入多個網域名稱。若要執行此作業，只需使用逗號分隔網域名稱即可：</p>
<p>-ADDomainNamingContextList @{Add=&quot;dc=fabrikam,dc=com&quot;,&quot;dc=contoso,dc=com&quot;}</p>
<p></p>
<p>如果您設定此屬性為 Null 值，則使用者複寫器會探索所有可用的網域並與其同步。如果此屬性並非 Null，則複寫器僅會與 ADDomainNamingContextList 中指定的網域同步。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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
<td><p><em>ReplicationCycleInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>表示在 Active Directory 中檢查使用者帳戶更新之前，使用者複寫器的等待時間。複寫循環間隔可以是 1 秒和 23 小時、59 分和 59 秒之間的任何時間值，預設值為 1 分鐘。間隔必須使用時:分:秒的格式表示。例如，此語法設定時間間隔為 1 小時 15 分：-ReplicationCycleInterval 01:15:00。</p></td>
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

無。**New-CsUserReplicatorConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsUserReplicatorConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.UserReplicator.UserReplicatorConfiguration 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsUserReplicatorConfiguration](get-csuserreplicatorconfiguration.md)  
[Remove-CsUserReplicatorConfiguration](remove-csuserreplicatorconfiguration.md)  
[Set-CsUserReplicatorConfiguration](set-csuserreplicatorconfiguration.md)

