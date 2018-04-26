---
title: Get-CsManagementConnection
TOCTitle: Get-CsManagementConnection
ms:assetid: b0e2377c-6aab-45d8-b71d-0d37c6f6dae3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412849(v=OCS.15)
ms:contentKeyID: 49292022
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsManagementConnection

 

_**上次修改主題的時間：** 2015-03-09_

傳回中央管理存放區的管理連線資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsManagementConnection

## 範例

## 範例 1

範例 1 的命令會傳回有關連至 中央管理存放區 的管理連線資訊。

    Get-CsManagementConnection

## 詳細描述

Lync Server 的組態資料是儲存在中央管理存放區中；Windows PowerShell 和管理複本服務必須能夠找到這個資料庫。安裝 Lync Server 時，在 Active Directory 網域服務 中會建立一個服務控制點，提供有關此資料庫的位置資訊。通常，電腦要靠這個服務控制點連線到中央管理存放區。若要查看此連線背後的詳細資訊 (亦即，如果您想知道中央管理存放區正在哪部電腦上執行，以及連至該中央管理存放區的 SQL Server 連線相關資訊)，可執行 **Get-CsManagementConnection** Cmdlet。

如果您已使用 **Set-CsManagementConnection** Cmdlet 來設定目前 Windows PowerShell 執行個體的暫時管理連線 (例如，以便從本機複本工作)，**Get-CsManagementConnection** Cmdlet 將會回報該暫時管理連線的資訊。相較之下，**Get-CsConfigurationStoreLocation** Cmdlet 一律會傳回 Active Directory 中服務控制點的資訊，而不論本機管理連線指向何處。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsManagementConnection** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsManagementConnection"}

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>此 Cmdlet 只提供一般的 Windows PowerShell 參數。</p></td>
<td> </td>
<td> </td>
<td> </td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsManagementConnection** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsManagementConnection** Cmdlet 會傳回 Microsoft.Rtc.Management.Xds.ManagementConnection 物件的執行個體。

## 請參閱

#### 其他資源

[Remove-CsManagementConnection](remove-csmanagementconnection.md)  
[Set-CsManagementConnection](set-csmanagementconnection.md)

