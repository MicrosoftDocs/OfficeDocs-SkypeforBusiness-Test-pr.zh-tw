---
title: Get-CsBackupServiceStatus
TOCTitle: Get-CsBackupServiceStatus
ms:assetid: 7f56cc81-534c-48e8-9f74-5741d4534a83
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205032(v=OCS.15)
ms:contentKeyID: 49291466
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsBackupServiceStatus

 

_**上次修改主題的時間：** 2015-03-09_

傳回指定集區之備份服務的目前狀態資訊。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsBackupServiceStatus -PoolFqdn <Fqdn> [-Category <UserData | CMS>] [-Force <SwitchParameter>]

## 範例

## 範例 1

上述命令會傳回 atl-cs-001.litwareinc.com 集區的備份服務狀態。

    Get-CsBackupServiceStatus -PoolFqdn "atl-cs-001.litwareinc.com"

## 詳細描述

**Get-CsBackupServiceStatus** Cmdlet 可讓系統管理員確認指定的登錄器集區是否已設定備份服務並正常運作。請注意，預設只有 RTCUniversalServerAdmins 群組的成員可以執行此 Cmdlet 檢查集區的備份狀態。若要提供權限讓其他群組也能執行此 Cmdlet，可使用 **Set-CsBackupServiceConfiguration** Cmdlet 將這些群組加入 AuthorizedUniversalGroups 屬性中。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsBackupServiceStatus"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsBackupServiceStatus** Cmdlet 所執行的功能。

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
<td><p>要檢查備份服務狀態之集區的完整網域名稱。例如：</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Category</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Hadr.BackupService.BackupCategory</p></td>
<td><p>要檢查其狀態的備份類型。允許的值為：</p>
<p>* CMS</p>
<p>* UserData</p>
<p>若未指定此參數，則兩種備份類型都會檢查。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsBackupServiceStatus** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

傳回備份服務的相關資訊。

## 請參閱

#### 其他資源

[Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)

