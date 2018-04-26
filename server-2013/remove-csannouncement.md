---
title: Remove-CsAnnouncement
TOCTitle: Remove-CsAnnouncement
ms:assetid: a3c62d15-1b0a-49d3-973f-abc06c730bb2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412766(v=OCS.15)
ms:contentKeyID: 49291886
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAnnouncement

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的 Lync Server 宣告。宣告會在使用者撥打有效但未經指派的電話號碼時播放，其可以是訊息 (例如 "This number is temporarily out of service" (此號碼暫時無法提供服務)) 或忙線訊號。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsAnnouncement -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會移除 Identity 為 "ApplicationServer:Redmond.litwareinc.com/1951f734-c80f-4fb2-965d-51807c792b90" 的宣告。由於 Identity 必須是唯一的，因此這個命令最多只會移除單一宣告。

    Remove-CsAnnouncement -Identity "ApplicationServer:Redmond.litwareinc.com/1951f734-c80f-4fb2-965d-51807c792b90"

## 範例 2

範例 2 會刪除所有套用至 ApplicationServer:Redmond.litwareinc.com 服務的宣告。為達成此目的，會呼叫 **Remove-CsAnnouncement** Cmdlet 搭配 Identity 參數。指定參數值 "ApplicationServer:Redmond.litwareinc.com" (未加上用來識別唯一宣告的 GUID) 會移除所有針對指定服務所設定的宣告。

    Remove-CsAnnouncement -Identity "ApplicationServer:Redmond.litwareinc.com"

## 詳細描述

組織可擁有未指派給使用者或話機的電話號碼，但它仍然是可撥打的有效號碼。根據預設，當某人撥打其中一個電話號碼，該來電者會收到忙線訊號，且來電可能會導致傳回 SIP 用戶端的錯誤。透過將宣告設定套用至未指派的號碼，系統管理員可播放訊息、傳回忙線訊號或將來電重新導向。此 Cmdlet 會移除其中一或多個宣告設定。

如果您嘗試移除與未指派的號碼範圍相關聯的宣告，則根據預設您將收到提示，詢問是否真的要移除宣告。如果刪除宣告，則該範圍的 AnnouncementName 屬性將顯示為 Null，而且當別人撥打那些號碼時，將不會聽到任何宣告，而只會聽到忙線訊號。然而，AnnouncementId 屬性值 (已移除之宣告的 GUID) 仍然維持可見。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsAnnouncement** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsAnnouncement"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要移除之宣告的唯一識別碼。您可以利用下列兩種方法提供 Identity 參數的值：</p>
<p>- 針對您要移除的宣告，輸入應用程式服務的 Identity。這將移除所有設定有指定服務 Identity 的宣告。例如，ApplicationServer:Redmond.litwareinc.com。</p>
<p>- 針對您要移除的單一宣告，輸入完整的 Identity。此值將永遠為 &lt;serviceID&gt;/&lt;GUID&gt; 格式，其中 serviceID 是執行宣告服務之應用程式伺服器的 Identity，而 GUID 是與此宣告相關聯的全域唯一識別碼。例如：ApplicationServer:Redmond.litwareinc.com/bef5fa3b-3c97-4af0-abe7-611deee7616c.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
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

無。

## 傳回類型

刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.AnnouncementServiceSettings.Announcement 物件執行個體。

## 請參閱

#### 其他資源

[New-CsAnnouncement](new-csannouncement.md)  
[Set-CsAnnouncement](set-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)

