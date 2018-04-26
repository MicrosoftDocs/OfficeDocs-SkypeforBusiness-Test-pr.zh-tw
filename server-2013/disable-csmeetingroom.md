---
title: Disable-CsMeetingRoom
TOCTitle: Disable-CsMeetingRoom
ms:assetid: 1bce6b58-484f-4e59-a259-aa315d37d9b0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204723(v=OCS.15)
ms:contentKeyID: 49290261
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsMeetingRoom

 

_**上次修改主題的時間：** 2015-03-09_

停用 Lync Server 2013 會議室。會議室是專為小型會議室之視訊會議及共同作業案例而設計的會議裝置。若是停用會議室物件，將會移除所有指派給會議室代表使用者帳戶之 Lync Server 相關的 Active Directory 屬性。但不會刪除 Active Directory 使用者帳戶本身。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Disable-CsMeetingRoom -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會停用 sip:RedmondMeetingRoom@litwareinc.com 會議室。

    Disable-CsMeetingRoom -Identity "sip:RedmondMeetingRoom@litwareinc.com"

## 範例 2

在範例 2 中，會停用組織中目前使用的所有會議室。為達成此目的，會先使用 **Get-CsMeetingRoom** Cmdlet 來擷取所有會議室的集合。然後，此集合會管線傳送到 **Disable-CsMeetingRoom** Cmdlet，以停用集合中的每個會議室。

    Get-CsMeetingRoom | Disable-CsMeetingRoom

## 詳細描述

在 Lync Server 中，會議室是安裝在會議室中，提供下列進階會議功能的內建電腦設備：

  - 單鍵加入會議功能

  - 多格檢視視訊庫

  - 在會議室畫面前方提供觸控式白板

  - 整合行事曆供查看排程會議

  - 內容共用及切換

若要管理這些新端點裝置，您必須為裝置建立並啟用 Microsoft Exchange Server 2013 資源信箱帳戶，然後再啟用 Lync Server 2013 的資源帳戶。請注意，沒有任何 Cmdlet 可以為 Lync Server 建立或移除會議室。您必須使用 [Enable-CsMeetingRoom](enable-csmeetingroom.md) Cmdlet 啟用會議室，以及使用 **Disable-CsMeetingRoom** Cmdlet 停用會議室。另外還必須有資源帳戶才可啟用會議室，停用會議室只會從會議室集合中移除該會議室，而不會刪除資源信箱帳戶。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Disable-CsMeetingRoom"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Disable-CsMeetingRoom** Cmdlet 所執行的功能。

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
<td><p>指出要設成會議室之使用者帳戶的 Identity。識別通常可以使用下列四種格式的其中一種來指定：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (例如 Ken Myer)。</p>
<p>您也可以利用使用者的 Active Directory 辨別名稱來參考使用者帳戶。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會傳回所有顯示名稱結尾為 &quot; Smith&quot; 字串值的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以停用會議室。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如 atl-dc-001) 或其完整網域名稱 (FQDN) (例如 atl-dc-001.litwareinc.com)。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您經由管線傳遞代表所要停用之會議室的會議室物件。根據預設，<strong>Disable-CsMeetingRoom</strong> Cmdlet 不會透過管線傳遞物件。</p></td>
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

**Disable-CsMeetingRoom** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom 物件執行個體。

## 傳回類型

無。反之，**Disable-CsMeetingRoom** Cmdlet 會刪除 Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom 物件的執行個體。

## 請參閱

#### 其他資源

[Enable-CsMeetingRoom](enable-csmeetingroom.md)  
[Get-CsMeetingRoom](get-csmeetingroom.md)  
[Move-CsMeetingRoom](move-csmeetingroom.md)  
[Set-CsMeetingRoom](set-csmeetingroom.md)

