---
title: Remove-CsUserAcp
TOCTitle: Remove-CsUserAcp
ms:assetid: dec450bb-d523-468d-aee4-07fdc3d567c4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398982(v=OCS.15)
ms:contentKeyID: 49292546
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUserAcp

 

_**上次修改主題的時間：** 2015-03-09_

移除一或多個指派給使用者或使用者群組的音訊會議提供者。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsUserAcp -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Name <String>] [-ParticipantPasscode <String>] [-PassThru <SwitchParameter>] [-TollNumber <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除已指派給使用者 Ken Myer 的所有音訊會議提供者。

    Remove-CsUserAcp -Identity "Ken Myer"

## 範例 2

範例 2 示範如何移除指派給已針對 Lync Server 啟用之所有使用者的所有音訊會議提供者。為達成此目的，命令會先使用 **Get-CsUser** Cmdlet，以擷取已針對 Lync Server 啟用之所有使用者的集合。然後，此集合會管線傳送到 **Remove-CsUserAcp** Cmdlet，以移除已指派給集合中每一位使用者的所有音訊會議提供者。

    Get-CsUser | Remove-CsUserAcp

## 範例 3

範例 3 會從 Ken Myer 的使用者帳戶移除具有 Name 為 "Fabrikam ACP" 的所有音訊會議提供者。

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Fabrikam ACP"

## 範例 4

範例 4 會從已指派音訊會議提供者的所有使用者帳戶移除含有免付費電話號碼 "14255551298" 的音訊會議提供者。為執行此工作，命令會先使用 **Get-CsUserAcp** Cmdlet，以傳回指派給您所有使用者之所有音訊會議提供者的資訊。然後將此資訊管線傳送到 **Where-Object** Cmdlet，這會只選取 AcpInfo 屬性包含 (-match) 電話號碼 "14255551298" 的帳戶。接著將此篩選後的集合管線傳送到 **Remove-CsUserAcp** Cmdlet，以從篩選後之集合中的每一個帳戶移除對應的音訊會議提供者。

    Get-CsUserAcp | Where-Object {$_.AcpInfo -match "14255551298"} | Remove-CsUserAcp

## 詳細描述

音訊會議提供者是提供組織會議服務的第三方公司。總而言之，音訊會議提供者提供處於異地之使用者在未連接至公司網路或網際網路，可參與會議之語音部分的方法。音訊會議提供者通常會提供高階服務，例如現場翻譯、記錄及現場個別會議總機服務。

Lync Server 不允許與音訊會議提供者完全整合。**CsUserAcp** Cmdlet 確實可讓系統管理員設定電話號碼和密碼，以及設定在使用者排程會議時隨時可用於音訊會議提供者整合的其他資訊。但是，因為這些 Cmdlet 並非設計來供 Lync Server 的內部部署版本使用 (他們的主要目的是和 Lync Online 搭配使用)，所以，除了指派內容值之外，不會提供任何其他音訊會議提供者整合。

任何指派給使用者的音訊會議提供者稍後都可以使用 **Remove-CsUserAcp** Cmdlet 來移除。呼叫不含任何參數 (指出要修改之使用者帳戶的 Identity 參數以外的參數) 的 **Remove-CsUserAcp** Cmdlet，以移除指派給使用者的所有音訊會議提供者。或者，您可以使用 **Remove-CsUserAcp** Cmdlet 隨附的選用參數，從使用者帳戶移除所選的提供者。例如，此命令會尋找 Ken Myer 使用者帳戶，並移除 Name 等於 “Fabrikam ACP” 的所有音訊會議提供者：

Remove-CsUserAcp –Identity "Ken Myer" –Name "Fabrikam ACP"

若要提供音訊會議提供者的較細部移除，只要包含其他參數即可。例如，這個命令會移除具有 Name 為 “Fabrikam ACP” 及 TollNumber 等於 "14255551298" 的任何音訊會議提供者，如下所示：

Remove-CsUserAcp –Identity "Ken Myer" –Name "Fabrikam ACP" –TollNumber "14255551298"

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsUserAcp** Cmdlet：RTCUniversalUserAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUserAcp"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>指出將要移除音訊會議提供者之使用者帳戶的 Identity。您可以使用下列四種格式的其中一種來指定使用者的 Identity：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；4) 使用者的 Active Directory 網域服務 顯示名稱 (如 Ken Myer)。您也可以使用使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
<p>使用「顯示名稱」做為使用者識別時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回所有顯示名稱是以字串 &quot; Smith&quot; 結束的使用者。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>音訊會議提供者的名稱。例如：-Name &quot;Fabrikam Conference Services&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>ParticipantPasscode</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>使用音訊會議提供者連接至會議時所需的密碼。例如：-PassCode &quot;0712&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過管線傳遞使用者物件，表示擁有音訊會議提供者的使用者已遭移除。根據預設，<strong>Remove-CsUserAcp</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="even">
<td><p><em>TollNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>用於音訊會議的非免付費電話號碼。例如：-TollNumber &quot;14255551298&quot;。</p></td>
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

字串或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Remove-CsUserAcp** Cmdlet 會接受代表已針對 Lync Server 啟用之使用者帳戶 Identity 的管線傳送字串值。此 Cmdlet 也接受管線傳送的 Active Directory 使用者物件執行個體。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Get-CsUserAcp](get-csuseracp.md)  
[Set-CsUserAcp](set-csuseracp.md)

