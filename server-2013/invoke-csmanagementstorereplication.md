---
title: Invoke-CsManagementStoreReplication
TOCTitle: Invoke-CsManagementStoreReplication
ms:assetid: fa3dece3-afd8-4669-94f9-fc3b70201e81
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413060(v=OCS.15)
ms:contentKeyID: 49292873
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsManagementStoreReplication

 

_**上次修改主題的時間：** 2015-03-09_

強制 Lync Server 複寫服務將完整的組態資料傳送至指定的電腦。作法是從中央管理存放區刪除電腦的複寫狀態。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Invoke-CsManagementStoreReplication [-ReplicaFqdn <String>] [-Force <SwitchParameter>]

## 範例

## 範例 1

範例 1 會呼叫不含任何參數的 **Invoke-CsManagementStoreReplication** Cmdlet，這會強制在所有 Lync Server 電腦上執行複寫。

    Invoke-CsManagementStoreReplication

## 範例 2

在範例 2 中，在呼叫 **Invoke-CsManagementStoreReplication** Cmdlet 時會使用 ReplicaFqdn 參數。結果就只會在 atl-cs-001.litwareinc.com 電腦上執行複寫。

    Invoke-CsManagementStoreReplication -ReplicaFqdn atl-cs-001.litwareinc.com

## 詳細描述

系統管理員對 Lync Server 進行變更 (例如，當系統管理員建立新的語音原則或變更 Address Book Server 組態設定) 時，該變更會記錄於 中央管理存放區 中。變更亦必須複寫到執行 Lync Server 服務或伺服器角色的所有電腦。

為了複寫資料，Master Replicator (執行於 中央管理伺服器) 會建立修改組態資料的快照；然後將此快照的複本傳送至執行 Lync Server 服務或伺服器角色的每一部電腦。在這些電腦上，複寫代理會接收快照並上載修改的資料；然後，代理會將報告最新複寫狀態的訊息傳送給 Master Replicator。

複寫通常不需要人為介入；事實上，通常最好是讓 Master Replicator 來處理複寫程序。但是，有時您還是需要在電腦 (或一組電腦) 上強制啟動複寫，而不等到標準複寫週期來執行複寫程序。如果發生這種情況，您可以使用 **Invoke-CsManagementStoreReplication** Cmdlet，強制將資訊複寫到電腦。

通常複寫會以累積方式進行：複寫資料時，系統只會複寫變更，而非複寫整個組態資料集。但是，當您呼叫 **Invoke-CsManagementStoreReplication** Cmdlet，您就強制完全複寫所有資料，不像一般只複寫變更。請注意，當您呼叫 **Invoke-CsManagementStoreReplication** Cmdlet 時，複寫不一定會立即發生。而是會有兩、三分鐘延遲，因為 Master Replicator 需要時間處理變更。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Invoke-CsManagementStoreReplication** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsManagementStoreReplication"}

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
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>ReplicaFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>應在其上啟動複寫之電腦的完整網域名稱 (FQDN)。例如：-ReplicaFqdn &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p>若未加入此參數，則系統會在您的所有 Lync Server 電腦上啟動複寫。</p>
<p></p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Invoke-CsManagementStoreReplication** Cmdlet 不會接受管線傳送的輸入。

## 傳回類型

**Invoke-CsManagementStoreReplication** Cmdlet 不會傳回任何物件。

## 請參閱

#### 其他資源

[Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)

