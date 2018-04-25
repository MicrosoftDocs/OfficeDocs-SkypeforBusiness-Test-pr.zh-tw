---
title: Get-CsManagementStoreReplicationStatus
TOCTitle: Get-CsManagementStoreReplicationStatus
ms:assetid: ea7162d6-d1e5-4301-b162-38da4e422293
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399052(v=OCS.15)
ms:contentKeyID: 49292692
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsManagementStoreReplicationStatus

 

_**上次修改主題的時間：** 2015-03-09_

傳回 Lync Server 複寫程序的資訊，包括 Lync Server 電腦的複寫內容是否為最新。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsManagementStoreReplicationStatus [-ReplicaFqdn <String>] [-CentralManagementStoreStatus <SwitchParameter>]

## 範例

## 範例 1

在範例 1 中，會呼叫 **Get-CsManagementStoreReplicationStatus** Cmdlet 且不搭配任何參數；這會傳回所有 Lync Server 電腦的複寫狀態 (最新或非最新)。

    Get-CsManagementStoreReplicationStatus

## 範例 2

範例 2 會傳回並非最新複寫之所有電腦的集合。這可藉由先使用 **Get-CsManagementStoreReplicationStatus** Cmdlet 擷取包含所有伺服器複寫狀態的集合來達成目標。然後將此集合傳送到 **Where-Object** Cmdlet 以套用篩選，將傳回的資料限制為 UpToDate 屬性等於 False 的電腦。

    Get-CsManagementStoreReplicationStatus | Where-Object {$_.UpToDate -eq $False}

## 範例 3

範例 3 會將傳回的資料限制為單一電腦：atl-cs-001.litwareinc.com/

    Get-CsManagementStoreReplicationStatus -ReplicaFqdn atl-cs-001.litwareinc.com

## 範例 4

範例 4 會傳回在 2010 年 8 月 11 日 8:00 P.M. 之前最後複寫之電腦的相關資訊。為達成此目的，會先呼叫 **Get-CsManagementStoreReplicationStatus** Cmdlet 以傳回您所有 Lync Server 電腦的複寫資訊。然後再將該資訊管線傳送到 **Where-Object** Cmdlet，這會只選取 LastUpdateCreation 屬性早於 2010 年 8 月 11 日下午 8:00 (8/11/2010 8:00 PM) 的電腦。若要傳回在 2010 年 8 月 11 日 8:00 P.M.之後最後複寫之電腦的資訊，請使用 -gt (大於) 運算子：

Where-Object {$\_.LastUpdateCreation -gt "8/11/2010 8:00 PM"}

本範例中指定的日期採用英文 (美國) 格式的日期時間值。應該採用與您的 \[地區及語言選項\] 相容的格式來指定日期。

    Get-CsManagementStoreReplicationStatus | Where-Object {$_.LastUpdateCreation -lt "8/11/2010 8:00 PM"}

## 範例 5

範例 5 所示的命令使用 CentralManagementStoreStatus 參數傳回 中央管理存放區 目前狀態的詳細資訊。這包含 Active Master 與 File Transfer Agent 服務的完整網域名稱，以及針對這些服務偵測最新活動訊號的日期和時間。

    Get-CsManagementStoreReplicationStatus -CentralManagementStoreStatus

## 詳細描述

系統管理員對 Lync Server 進行某些變更 (例如，當系統管理員建立新的語音原則或變更 Address Book Server 組態設定) 時，該變更會記錄於 中央管理存放區 中。變更亦必須複寫到執行 Lync Server 服務或伺服器角色的所有電腦。

為了複寫資料，Master Replicator (執行於 中央管理伺服器) 會建立修改組態資料的快照；然後將此快照的複本傳送至執行 Lync Server 服務或伺服器角色的每一部電腦。在這些電腦上，複寫代理會接收快照並上載修改的資料；然後，代理會將報告最新複寫狀態的訊息傳送給 Master Replicator。

**Get-CsManagementStoreReplicationStatus** Cmdlet 可讓您確認您組織中任何 (或所有) Lync Server 電腦的複寫狀態。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsManagementStoreReplicationStatus** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsManagementStoreReplicationStatus"}

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
<td><p><em>CentralManagementStoreStatus</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回 中央管理存放區 之目前狀態的其他相關資訊，包括使用中的複寫清單以及已刪除的複寫清單；以及 Active Master 與 File Transfer Agent 服務的位置。</p></td>
</tr>
<tr class="even">
<td><p><em>ReplicaFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要檢查其複寫狀態之電腦的完整網域名稱 (FQDN)。例如：-ReplicaFqdn &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p>若未加入此參數，則將會傳回您所有 Lync Server 電腦的複寫狀態資訊。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsManagementStoreReplicationStatus** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

根據預設，**Get-CsManagementStoreReplicationStatus** Cmdlet 會傳回 Microsoft.Rtc.Management.Xds.ReplicaState 物件的執行個體。如果使用 CentralManagementStoreStatus 參數，則 Cmdlet 會傳回 Microsoft.Rtc.Management.Xds.CentralManagementStoreStatusResult 物件的執行個體。

## 請參閱

#### 其他資源

[Invoke-CsManagementStoreReplication](invoke-csmanagementstorereplication.md)

