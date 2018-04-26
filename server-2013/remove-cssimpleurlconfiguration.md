---
title: Remove-CsSimpleUrlConfiguration
TOCTitle: Remove-CsSimpleUrlConfiguration
ms:assetid: 6cf483ed-7a53-47b0-b87a-6ef70493ba32
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398515(v=OCS.15)
ms:contentKeyID: 49291236
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsSimpleUrlConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除組織目前所使用之一或多個易記 URL 組態集合。易記 URL 可方便使用者加入會議，以及方便系統管理員登入 Lync Server 控制台。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsSimpleUrlConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除套用至 Redmond 網站的簡易 URL 組態集合。此命令會刪除指派給指定網站的所有簡易 URL。

    Remove-CsSimpleUrlConfiguration -Identity "site:Redmond"

## 範例 2

範例 2 會刪除在網站範圍套用的所有簡易 URL 組態集合。為達成此目的，命令會先使用 **Get-CsSimpleUrlConfiguration** Cmdlet 並搭配 Filter 參數，以傳回網站範圍所設定的所有簡易 URL 集合；篩選值 "site:\*" 可將傳回的資料限制在 Identity 開頭為字串值 "site:" 的集合。然後再將篩選後的集合管線傳送到 **Remove-CsSimpleUrlConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsSimpleUrlConfiguration -Filter "site:*" | Remove-CsSimpleUrlConfiguration 

## 詳細描述

在 Microsoft Office Communications Server 2007 R2 中，會議具有類似下列的 URL：

https://imdf.litwareinc.com/Join?uri=sip%3Akenmyer%40litwareinc.com%3Bgruu%3Bopaque%3Dapp%3Aconf%3Afocus%3Aid%3A125f95a0b0184dcea706f1a0191202a8\&key=EcznhLh5K5t

不過，這種 URl 不是很直覺，不容易傳達給其他人。Lync Server 2010 中採用的簡易 URL 提供類似下列的 URL 給使用者，有助於克服這些問題：

https://meet.litwareinc.com/kenmyer/071200

Simple URL 為 Office Communications Server 中使用的 URL 進行改進。但是系統不會自動建立簡易 URL；而是您必須自行設定 URL。此外，您還必須執行其他動作，例如建立每個 URL 的網域名稱系統 (DNS) 記錄、設定外部存取的反向 Proxy 規則、將簡易 URL 新增至前端伺服器憑證等。

Lync Server 可讓您建立三個不同的易記 URL：

Meet – 用於會議。您的每個 SIP 網域都必須至少有一個 Meet URL。

Admin – 用於將系統管理員指向 Lync Server。

Dialin – 用於電話撥入式會議網頁。

易記 URL 儲存在簡易 URL 組態集合中。當您安裝 Lync Server 後，系統會建立全域集合，您也可以在網站範圍建立自訂集合。這讓您能夠在每個網站使用不同的易記 URL。

簡易 URL 組態集合是使用 **New-CsSimpleUrlConfiguration** Cmdlet 所建立；您接著可以使用其他 Cmdlet (例如 **New-CsSimpleUrlEntry** Cmdlet 和 **Set-CsSimpleUrlConfiguration** Cmdlet) 將簡易 URL 填入這些集合。如果您之後決定要刪除一或多個網站範圍的集合，可以使用 **Remove-CsSimpleUrlConfiguration** Cmdlet 完成。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsSimpleUrlConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsSimpleUrlConfiguration"}

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
<td><p>要移除之簡易 URL 集合的唯一識別碼。若要移除站範圍的集合，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。請注意，如有指定 Identity，即無法使用萬用字元。</p>
<p>您也可以使用此語法，針對全域集合執行此 Cmdlet：-Identity global。不過，在該情況下，將不會刪除全域集合，而是刪除該集合中的所有簡易 URL。</p></td>
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
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要刪除之簡易 URL 組態設定的 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令來傳回每位租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.SimpleUrl.SimpleUrlConfiguration 物件。**Remove-CsSimpleUrlConfiguration** Cmdlet 接受管線傳送的簡易 URL 組態物件執行個體。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)  
[New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)  
[Set-CsSimpleUrlConfiguration](set-cssimpleurlconfiguration.md)

