---
title: Remove-CsManagementConnection
TOCTitle: Remove-CsManagementConnection
ms:assetid: 2fe69a3d-0154-418f-b6ee-99a88e5a9c7d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425803(v=OCS.15)
ms:contentKeyID: 49290485
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsManagementConnection

 

_**上次修改主題的時間：** 2015-03-09_

將管理連線重設為中央管理存放區的 Active Directory 服務控制點。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsManagementConnection [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除現有的管理連線資訊，並以儲存在 Active Directory 中的預設連線資訊取代。

    Remove-CsManagementConnection

## 詳細描述

Lync Server 的組態資料是儲存在中央管理存放區；Windows PowerShell 和管理複寫服務必須能夠找到此資料庫。安裝 Lync Server 時，在 Active Directory 網域服務 中會建立一個服務控制點，提供此資料庫的位置資訊。通常，電腦要藉由此服務控制點連線到中央管理存放區。若要查看此連線的詳細資料 (亦即，如果您想知道中央管理存放區在哪部電腦上執行，以及連接至該中央管理存放區的 SQL Server 連線相關資訊)，可執行 **Get-CsManagementConnection** Cmdlet。

您通常不需要變更管理連線。但您可能需要暫時使用新的管理連線。當您準備好切換回預設連線時，只需要執行 **Remove-CsManagementConnection** Cmdlet 就可以了；這個 Cmdlet 會清除目前的連線資訊，並以儲存在 Active Directory 服務控制指標中的連線資訊取代。這表示您不需要重新建立原始的連線資訊；**Remove-CsManagementConnection** Cmdlet 將為您完成。

請注意，如果在使用預設連線時呼叫此 Cmdlet，將不會發生任何問題。如果您這樣做，只需繼續使用儲存在 Active Directory 的預設連線資訊。另請注意，此 Cmdlet 只會影響您目前 Windows PowerShell 工作階段的管理連線資訊：對管理連線所進行的變更會限制為您的本機電腦以及 Windows PowerShell 的本機執行個體。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsManagementConnection** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsManagementConnection"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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

無。**Remove-CsManagementConnection** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。反之，**Remove-CsManagementConnection** Cmdlet 會刪除 Microsoft.Rtc.Management.Xds.ManagementConnection 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsManagementConnection](get-csmanagementconnection.md)  
[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)  
[Set-CsManagementConnection](set-csmanagementconnection.md)

