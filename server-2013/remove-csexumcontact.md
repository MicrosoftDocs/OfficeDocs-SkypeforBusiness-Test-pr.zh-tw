---
title: Remove-CsExUmContact
TOCTitle: Remove-CsExUmContact
ms:assetid: d79f7082-f58b-4cc3-a90d-230111e32850
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398946(v=OCS.15)
ms:contentKeyID: 49292465
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsExUmContact

 

_**上次修改主題的時間：** 2015-03-09_

移除代管之 Exchange 整合通訊 (UM) 的自動語音應答或使用者存取連絡人物件。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsExUmContact -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個範例會移除 SIP 位址為 exumsa1@fabrikam.com 的 Exchange UM 連絡人。

    Remove-CsExUmContact -Identity sip:exumsa1@fabrikam.com

## 範例 2

這個範例會移除 LineURI 值的開頭為 tel:425 的所有 Exchange UM 連絡人。此命令的第一部分會呼叫 **Get-CsExUmContact** Cmdlet 並搭配 Filter 參數，並使用下列運算式做為篩選器：LineURI -like "tel:425\*"。該篩選器指定我們想要擷取 LineURI 符合萬用字元字串 tel:425\* 的 Exchange UM 連絡人物件。換言之，以字串 tel:425 開頭，且以任何字元集結尾的所有 Line URI。取得該物件集合後，將集合傳送到 **Remove-CsExUmContact** Cmdlet，它會移除集合中所有的項目。

    Get-CsExUmContact -Filter {LineURI -like "tel:425*"} | Remove-CsExUmContact

## 詳細描述

Lync Server 搭配 Exchange UM 一起提供多項語音相關功能，包括自動語音應答和使用者存取。以主控服務 (非內部部署) 形式提供 Exchange UM 時，必須使用 Windows PowerShell 建立連絡人物件以套用「自動語音應答」和「使用者存取」功能。建立的任何物件可以使用 **Remove-CsExUmContact** Cmdlet 移除。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsExUmContact** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsExUmContact"}

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
<td><p>您要移除之連絡人物件的唯一識別碼。可以使用下列四種格式的其中一種來指定連絡人識別身分：1) 連絡人的 SIP 位址；2) 連絡人的使用者主體名稱 (UPN)；3) 連絡人的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\exum1)；和 4) 連絡人的 Active Directory 顯示名稱 (例如 Team Auto Attendant)。</p>
<p>完整資料類型：Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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

Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact 物件。接受 Exchange UM 連絡人物件管線傳送的輸入。

## 傳回類型

這個 Cmdlet 不會傳回物件。它會移除 Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact 類型的物件。

## 請參閱

#### 其他資源

[New-CsExUmContact](new-csexumcontact.md)  
[Set-CsExUmContact](set-csexumcontact.md)  
[Get-CsExUmContact](get-csexumcontact.md)  
[Move-CsExUmContact](move-csexumcontact.md)

