---
title: Debug-CsInterPoolReplication
TOCTitle: Debug-CsInterPoolReplication
ms:assetid: 945bfd1c-1759-4869-9316-b3260fcc633d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619185(v=OCS.15)
ms:contentKeyID: 49291693
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Debug-CsInterPoolReplication

 

_**上次修改主題的時間：** 2015-03-09_

確認登錄器集區與其指定的備份集區之間正在進行複寫。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Debug-CsInterPoolReplication -PoolFqdn <Fqdn> [-BackupModule <All | CentralMgmt | PresenceFocus | DataConf>] [-Force <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令可確認集區 atl-cs-001.litwareinc.com 與其先前指定的備份集區之間的完整複寫狀態。

    Debug-CsInterPoolReplication -PoolFqdn "atl-cs-001.litwareinc.com"

## 範例 2

在範例 2 中，只會確認在集區 atl-cs-001.litwareinc.com 與其先前指定的備份集區之間複寫的資料會議資料。

    Debug-CsInterPoolReplication -PoolFqdn "atl-cs-001.litwareinc.com" -BackupModule DataConf

## 詳細描述

在 Lync Server 2013 中，每個登錄器集區都能與一個備份集區關聯。備份集區會保留主要集區上儲存之所有資料的複本。萬一主要集區無法使用，該集區的使用者就能夠自動容錯移轉到備份集區。如此一來，即使那些使用者的主集區無法使用，他們仍可繼續使用 Lync Server。Debug-CsInterPoolReplication Cmdlet 可用來比較主要集區與其備份集區上儲存的資料，因而可確認在兩個集區之間的複寫是否如預期運作。

請注意，如果正要測試的集區尚未指定備份集區，此命令將會失敗。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Debug-CsInterPoolReplication"}

**Lync Server 控制台：** 無法在 Lync Server 控制台 中使用由 Debug-CsInterPoolReplication Cmdlet 執行的功能。

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
<td><p><em>PoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>正要測試之集區的完整網域名稱。例如：</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>BackupModule</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Hadr.BackupService.BackupModules</p></td>
<td><p>可讓管理指定要驗證的資料存放區。允許的值為：</p>
<p>* All</p>
<p>* CentralMgmt</p>
<p>* PresenceFocus</p>
<p>* DataConf</p>
<p>預設值為 All。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。Debug-CsInterPoolReplication 不接受管線傳送的資料。

## 傳回類型

字串值。

