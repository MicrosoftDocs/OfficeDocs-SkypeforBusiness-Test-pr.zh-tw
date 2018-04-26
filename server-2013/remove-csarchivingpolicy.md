---
title: Remove-CsArchivingPolicy
TOCTitle: Remove-CsArchivingPolicy
ms:assetid: 41f11a99-14f1-4292-9d58-eb7a7761b829
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425924(v=OCS.15)
ms:contentKeyID: 49290725
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsArchivingPolicy

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的立即訊息 (IM) 封存原則。IM 封存原則可指定 Lync Server 是否要自動儲存內部使用者之間及/或內部使用者與同盟協力廠商之間所發生的所有 IM 工作階段。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsArchivingPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中， **Remove-CsArchivingPolicy** Cmdlet 用於刪除 Identity 為 site:Redmond 的原則。請注意，刪除在網站範圍設定的原則時，先前由該網站原則管理的使用者會自動改由全域範圍封存原則管理。

    Remove-CsArchivingPolicy -Identity site:Redmond

## 範例 2

範例 2 會移除在網站範圍設定的所有封存原則。首先會使用 **Get-CsArchivingPolicy** Cmdlet 搭配 Filter 參數，擷取在網站範圍指派之所有封存原則的集合。然後再使用篩選值 "site:\*" 指示 **Get-CsArchivingPolicy** Cmdlet 只傳回 Identity 開頭為字串值 "site:" 的原則。傳回集合後，再將資料管線傳送到 **Remove-CsArchivingPolicy** Cmdlet，以刪除集合中的所有原則。

    Get-CsArchivingPolicy -Filter site:* | Remove-CsArchivingPolicy

## 範例 3

範例 3 會刪除 ArchiveExternal 屬性設為 False 的所有封存原則。為達成此目的，命令會先使用 **Get-CsArchivingPolicy** Cmdlet 傳回設定供組織使用之所有封存原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 ArchiveExternal 屬性等於 False 的原則。接著將篩選後的集合管線傳送到 **Remove-CsArchivingPolicy** Cmdlet，以刪除集合中的每個原則。

    Get-CsArchivingPolicy | Where-Object {$_.ArchiveExternal -eq $False} | Remove-CsArchivingPolicy 

## 詳細描述

許多組織都發現保留其使用者參與之所有 IM 工作階段的封存很有用處；有些組織則是依法保留此類封存。若要使用 Lync Server 封存 IM 工作階段，您必須執行兩個步驟。首先，您需要使用 **Set-CsArchivingConfiguration** Cmdlet，在全域範圍和/或網站範圍啟用封存。這可讓您能夠封存 IM 工作階段，不過，它不會自動開始封存這些工作階段。

但是，若要實際儲存 IM 工作階段的文字記錄，您必須完成步驟 2：建立一或多個封存原則。這些原則會決定哪些使用者要記錄其 IM 工作階段，以及要封存哪些類型的 IM 工作階段 (內部和/或外部)。內部 IM 工作階段是工作階段中，所有參與者都是擁有組織中 Active Directory 帳戶的已驗證使用者；外部 IM 工作階段是工作階段中，至少有一個參與者是沒有組織中 Active Directory 帳戶的未驗證使用者。您可以選擇只封存內部工作階段、只封存外部工作階段，或是同時封存內部和外部工作階段。

封存原則可以指派給全域範圍或網站範圍。此外，這些原則還可以指派給個別使用者範圍，然後套用至特定使用者或特定一組使用者。例如，假設您的全域原則只會封存所有使用者的內部 IM 工作階段。在此情況下，您可以建立同時封存內部和外部工作階段的次要原則，然後只將該原則套用到您自己的銷售人員。因為個別使用者原則的優先順序高於全域範圍和網站原則，因此銷售人員的成員將會封存其所有 IM 工作階段。其他使用者 (也就是不在銷售部門且不受銷售原則影響的使用者) 就只會封存其內部 IM 工作階段。

**Remove-CsArchivingPolicy** Cmdlet 可讓您刪除針對用於組織中而建立的封存原則。如果您刪除某個個別使用者原則，已被指派該原則的所有使用者都會自動由相關的網站原則管轄。如果沒有網站原則，這些使用者會由全域原則管理。如果您移除某個網站原則，受該原則影響的使用者會自動由全域原則管轄。

請注意，您也可以對全域原則執行 **Remove-CsArchivingPolicy** Cmdlet，不過無法移除全域原則。針對全域原則執行 **Remove-CsArchivingPolicy** Cmdlet 反而會導致該原則中的所有內容重設為其預設值；這表示將不會封存內部或外部 IM 工作階段。那是因為這些屬性 (ArchiveInternal 和 ArchiveExternal) 的預設值都為 False。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsArchivingPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsArchivingPolicy"}

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
<td><p>要移除之封存原則的唯一識別碼。封存原則可以在全域、網站或個別使用者範圍設定。若要移除全域原則，請使用下列語法：-Identity global。(請注意，實際上無法移除全域原則，而是將所有原則屬性重設為其預設值)。</p>
<p>若要移除網站原則，請使用類似下列的語法：-Identity site:Redmond。若要移除個別使用者原則，請使用類似下列的語法：-Identity SalesArchivingPolicy。</p>
<p>指定 Identity 時不允許使用萬元字元。</p></td>
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
<td><p>如果使用此參數，即使原則目前已指派給至少一個使用者，也將會遭到自動移除。若未使用此參數， <strong>Remove-CsArchivingPolicy</strong> Cmdlet 就不會自動移除已指派給至少一個使用者的個別使用者原則。但是會顯示確認提示，詢問您是否確定要移除該原則。您必須回答是 (按下 Y 鍵)，命令才會繼續並移除該原則。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.IM.IMArchivingPolicy 物件。 **Remove-CsArchivingPolicy** Cmdlet 接受管線傳送的封存原則物件輸入。

## 傳回類型

**Remove-CsArchivingPolicy** Cmdlet 不會傳回值或物件，而會移除 Microsoft.Rtc.Management.WritableConfig.Policy.IM.IMArchivingPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsArchivingPolicy](get-csarchivingpolicy.md)  
[Grant-CsArchivingPolicy](grant-csarchivingpolicy.md)  
[New-CsArchivingPolicy](new-csarchivingpolicy.md)  
[Set-CsArchivingPolicy](set-csarchivingpolicy.md)

