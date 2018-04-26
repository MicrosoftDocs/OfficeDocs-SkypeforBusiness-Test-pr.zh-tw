---
title: Move-CsMeetingRoom
TOCTitle: Move-CsMeetingRoom
ms:assetid: 4ea6b8bd-b134-4453-9ae4-6118330a62ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204889(v=OCS.15)
ms:contentKeyID: 49290878
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsMeetingRoom

 

_**上次修改主題的時間：** 2015-03-09_

在登錄器集區之間移動 Lync Server 2013 會議室物件。會議室是專為小型會議室之視訊會議及共同作業案例而設計的會議裝置。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Move-CsMeetingRoom -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將顯示名稱為 "Room 14" 的會議室移至 atl-cs-001.litwareinc.com 集區。

    Move-CsMeetingRoom -Target "atl-cs-001.litwareinc.com" -Identity "Room 14"

## 範例 2

範例 2 會將組織中的所有會議室移至 atl-cs-001.litwareinc.com 集區。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsMeetingRoom** Cmdlet，以傳回設定供組織使用之所有會議室的集合。然後，此集合會管線傳送到 **Move-CsMeetingRoom** Cmdlet，以將集合中的每個會議室移至新集區。

    Get-CsMeetingRoom | Move-CsMeetingRoom -Target "atl-cs-001.litwareinc.com"

## 詳細描述

在 Lync Server 中，會議室是安裝在會議室中，提供下列進階會議功能的內建電腦設備：

  - 單鍵加入會議功能

  - 多格檢視視訊庫

  - 在會議室畫面前方提供觸控式白板

  - 整合行事曆供查看排程會議

  - 內容共用及切換

若要管理這些新端點裝置，您必須為裝置建立並啟用 Microsoft Exchange Server 2013資源信箱帳戶，然後再啟用 Lync Server 2013的資源帳戶。請注意，沒有任何 Cmdlet 可以為 Lync Server 建立或移除會議室。您必須使用 [Enable-CsMeetingRoom](enable-csmeetingroom.md) Cmdlet 啟用會議室，以及使用 [Disable-CsMeetingRoom](disable-csmeetingroom.md) Cmdlet 停用會議室。另外還必須有資源帳戶，才可啟用會議室。停用會議室只會從會議室集合中移除該會議室，而不會刪除資源信箱帳戶。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsMeetingRoom"}

Lync Server 控制台：Lync Server 控制台不提供 **Move-CsMeetingRoom** Cmdlet 所執行的功能。

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
<td><p>指出所要移動之會議室的 Identity。會議室會以下列四種格式之一來指定：1) 會議室的 SIP 位址；2) 會議室的使用者主體名稱 (UPN)；3) 會議室的網域名稱和登入名稱，必須是「網域\登入」格式 (例如，litwareinc\kenmyer)；以及 4) 會議室的 Active Directory 顯示名稱 (例如 Main Conference Room)。也可以利用會議室的 Active Directory 辨別名稱來參照使用者 Identity。</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>應移動其會議室之登錄器集區的 FQDN (例如，atl-cs-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以移動會議室。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-dc-001) 或其完整網域名稱 (FQDN) (例如，atl-dc-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，會指示 <strong>Move-CsMeetingRoom</strong> Cmdlet 忽略執行移動作業時可能發生的所有錯誤。一般來說，除非必須，否則應避免使用 Force 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會指示電腦忽略後端資料庫可能發生的任何錯誤，並嘗試移動會議室，而不管那些錯誤。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您經由管線傳遞代表所要移動之會議室的會議室物件。根據預設，<strong>Move-CsMeetingRoom</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>此參數不會與內部部署的 Lync Server 2013版本搭配使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Moves-CsMeetingRoom Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom 物件執行個體。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Disable-CsMeetingRoom](disable-csmeetingroom.md)  
[Enable-CsMeetingRoom](enable-csmeetingroom.md)  
[Get-CsMeetingRoom](get-csmeetingroom.md)  
[Set-CsMeetingRoom](set-csmeetingroom.md)

