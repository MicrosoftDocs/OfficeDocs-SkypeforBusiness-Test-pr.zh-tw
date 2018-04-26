---
title: Get-CsDatabaseMirrorState
TOCTitle: Get-CsDatabaseMirrorState
ms:assetid: 458f5367-ee04-4281-971f-08f79a625509
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204845(v=OCS.15)
ms:contentKeyID: 49290778
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDatabaseMirrorState

 

_**上次修改主題的時間：** 2015-03-09_

傳回指定集區上的指定資料庫是否已經執行鏡像的資訊。資料庫鏡像可讓您同時維護兩個資料庫，而兩個資料庫各在不同的伺服器上。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsDatabaseMirrorState -PoolFqdn <Fqdn> [-DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt>] [-LocalStore <SwitchParameter>] [-Report <String>]

## 範例

## 範例 1

範例 1 所示的命令會針對 atl-cs-001.litwareinc.com 集區，傳回指派給監控資料庫之資料庫鏡像的狀態。

    Get-CsDatabaseMirrorState -PoolFqdn "atl-cs-001.litwareinc.com" -DatabaseType Monitoring

## 詳細描述

**Get-CsDatabaseMirrorState** Cmdlet 會傳回設定供集區使用之鏡像資料庫的資訊，包括前端伺服器資料庫、位置資訊服務資料庫、通話詳細記錄與經驗品質資料庫等等是否設有鏡像資料庫。此 Cmdlet 會針對每一個資料庫回報其主要資料庫與鏡像資料庫的同步狀態。在某些情況下，您會看到類似下列包含屬性值 DatabaseInaccessibleOrMirroringNotEnabled 的輸出：

DatabaseName : lcscdr

StateOnPrimary : DatabaseInaccessibleOrMirroringNotEnabled

StateOnMirror : DatabaseInaccessibleOrMirroringNotEnabled

MirroringStatusOnPrimary :

MirroringStatusOnSecondary :

這通常表示主要資料庫未指派鏡像資料庫 (此案例使用資料庫 lcscdr 維護通話詳細資料)。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDatabaseMirrorState"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsDatabaseMirrorState** Cmdlet 所執行的功能。

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
<td><p>要檢查資料庫鏡像狀態之集區的完整網域名稱。例如：</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseType</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.DatabaseNameType</p></td>
<td><p>要檢查鏡像狀態之資料庫的類型。允許的值為：</p>
<p>Application</p>
<p>Archiving</p>
<p>CentralAdmin</p>
<p>CentralMgmt</p>
<p>Edge</p>
<p>Lyss</p>
<p>Monitoring</p>
<p>PersistentChat</p>
<p>PersistentChatCompliance</p>
<p>Provision</p>
<p>Registrar</p>
<p>User</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取備份鏡像狀態，而不從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：</p>
<p>-Report &quot;C:\Logs\DatabaseMirrorState.html&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsDatabaseMirrorState** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsDatabaseMirrorState** Cmdlet 會傳回 Microsoft.Rtc.Management.Deployment.DatabaseMirrorState 類別的執行個體。

## 請參閱

#### 其他資源

[Install-CsMirrorDatabase](install-csmirrordatabase.md)  
[Uninstall-CsMirrorDatabase](uninstall-csmirrordatabase.md)

