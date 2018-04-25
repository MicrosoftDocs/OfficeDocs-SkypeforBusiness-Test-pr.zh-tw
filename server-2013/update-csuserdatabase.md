---
title: Update-CsUserDatabase
TOCTitle: Update-CsUserDatabase
ms:assetid: 86ed4291-70cc-4c41-ab2a-e5f7546a0f1f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398682(v=OCS.15)
ms:contentKeyID: 49291557
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsUserDatabase

 

_**上次修改主題的時間：** 2015-03-09_

強制後端使用者資料庫清除其在 Active Directory 上複寫狀態。這可讓資料庫重新讀取 Active Directory 網域服務 中所儲存的所有使用者資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Update-CsUserDatabase [-Force <SwitchParameter>] [-Fqdn <Fqdn>]

## 範例

## 範例 1

範例 1 所示的命令會找出本機電腦所在集區的使用者資料庫，然後強制該資料庫連線至 Active Directory，並從 Active Directory 傳回完整的使用者資訊。

    Update-CsUserDatabase

## 範例 2

範例 2 顯示您可以如何強制特定使用者資料庫重新讀取 Active Directory 的資料。在此範例中就是 atl-cs-001.litwareinc.com 集區的使用者資料庫。

    Update-CsUserDatabase -Fqdn atl-cs-001.litwareinc.com

## 詳細描述

Lync Server 使用者資料庫會保留如連絡人、群組和存取權限等詳細的資訊。因此，此資料庫的內容需要定期與 Active Directory 中儲存的資訊同步化。

使用者資料庫與 Active Directory 之間通常會有自動同步化，以保持使用者資料庫內的資訊為最新狀態。但有時候可能會發生問題，使得自動同步化無法執行。在這種情況下，您可以使用 **Update-CsUserDatabase** Cmdlet，強制使用者資料庫重新讀取 Active Directory 中儲存的所有使用者資訊，以重新整理自己的內容。如果產品更新包含使用者複寫器的變更，您也需要執行這個 Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Update-CsUserDatabase** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Update-CsUserDatabase"}

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
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Fqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>裝載使用者資料庫之電腦的完整網域名稱 (FQDN)。若未指定此參數，則 <strong>Update-CsUserDatabase</strong> Cmdlet 會更新本機電腦所屬之集區的使用者資料庫。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Update-CsUserDatabase** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。反之，**Update-CsUserDatabase** Cmdlet 會更新 Microsoft.Rtc.Management.Xds.DisplayuserDatabase 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsUserDatabaseState](get-csuserdatabasestate.md)  
[Set-CsUserDatabaseState](set-csuserdatabasestate.md)

