---
title: Remove-CsDialInConferencingAccessNumber
TOCTitle: Remove-CsDialInConferencingAccessNumber
ms:assetid: a6d5a6f4-5ad1-4253-b1c4-27f81851046f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412782(v=OCS.15)
ms:contentKeyID: 49291912
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDialInConferencingAccessNumber

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的電話撥入式會議存取號碼。電話撥入式會議可讓使用者使用一般的電話或行動電話 (亦即公用交換電話網路 (PSTN) 上的裝置) 加入會議的音訊部分。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsDialInConferencingAccessNumber -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除 Identity 為 sip:RedmondDialIn@litwareinc.com 的電話撥入式會議存取號碼。

    Remove-CsDialInConferencingAccessNumber -Identity sip:RedmondDialIn@litwareinc.com

## 範例 2

範例 2 會刪除所有的免付費電話撥入式會議存取號碼；在此範例中，這表示 LineUri 是以 "tel:+1800" 開頭的任何號碼。為達成此目的，命令會使用 **Get-CsDialInConferencingAccessNumber** Cmdlet 搭配 Filter 參數，以傳回設定供組織使用之所有免付費存取號碼的集合 (篩選值 {LineUri -like "tel:+1800\*"} 可將傳回的資料限制為 LineUri 屬性是以字串值 "tel:+1800" 開頭的電話號碼)。然後再將此篩選後的集合管線傳送到 **Remove-CsDialInConferencingAccessNumber** Cmdlet，以刪除集合中的每一個號碼。

    Get-CsDialInConferencingAccessNumber -Filter {LineUri -like "tel:+1800*"} | Remove-CsDialInConferencingAccessNumber

## 範例 3

範例 3 會刪除 Redmond 地區的所有電話撥入式會議存取號碼。為了執行此工作，會先呼叫 **Get-CsDialInConferencingAccessNumber** Cmdlet 搭配 Region 參數，以傳回 Redmond 地區的所有存取號碼集合 (亦即，地區清單中所有包含 Redmond 的存取號碼)。然後，此集合會管線傳送到 **Remove-CsDialInConferencingAccessNumber** Cmdlet，以刪除集合中的所有存取號碼。

    Get-CsDialInConferencingAccessNumber -Region "Redmond" | Remove-CsDialInConferencingAccessNumber

## 範例 4

範例 4 會刪除所有沒有與地區關聯的電話撥入式會議存取號碼。為達成此目的，會呼叫 **Get-CsDialInConferencingAccessNumber** Cmdlet 搭配 Region 參數，並使用參數值 $Null，以傳回 Regions 屬性為空白的存取號碼集合。然後，此集合會管線傳送到 **Remove-CsDialInConferencingAccessNumber** Cmdlet，以刪除集合中的所有號碼。

    Get-CsDialInConferencingAccessNumber -Region $Null | Remove-CsDialInConferencingAccessNumber

## 範例 5

範例 5 所示的命令會刪除所有主要語言不是設為 Italian 的電話撥入式會議存取號碼。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsDialInConferencingAccessNumber** Cmdlet，以傳回設定供組織使用之所有電話撥入式會議存取號碼的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 PrimaryLanguage 屬性不等於 Italian ("it-IT") 的所有號碼。接著將篩選後的集合管線傳送到 **Remove-CsDialInConferencingAccessNumber** Cmdlet，以刪除集合中的所有存取號碼。

    Get-CsDialInConferencingAccessNumber | Where-Object {$_.PrimaryLanguage -ne "it-IT"} | Remove-CsDialInConferencingAccessNumber

## 範例 6

範例 6 會刪除顯示名稱為 "Default Dial-In Access Number" 的電話撥入式會議存取號碼。為達成此目的，會呼叫 **Get-CsDialInConferencingAccessNumber** Cmdlet 搭配 Filter 參數，並使用篩選值 {DisplayName -eq "Default Dial-In Access Number"}；此篩選值可將傳回的資料限制為 DisplayName 屬性等於 "Default Dial-In Access Number" 的存取號碼。然後再將傳回的物件管線傳送到 **Remove-CsDialInConferencingAccessNumber** Cmdlet，以刪除對應的存取號碼。

    Get-CsDialInConferencingAccessNumber -Filter {DisplayName -eq "Default Dial-In Access Number"} | Remove-CsDialInConferencingAccessNumber

## 詳細描述

電話撥入式會議讓使用者可以使用任何一種電話 (例如，標準的「地面通訊」電話、行動電話或 Voice over Internet Protocol 電話)，來加入會議的音訊部分。讓使用者即使沒有電腦或網際網路連線也可以參與會議。使用者可用完整的音訊功能：他們可以對其他參與者講話，聽到其他人所說的每句話。他們只是看不到共用的投影片、視訊播放，或其他視覺元素。

若要為使用者提供電話撥入式會議的功能，您必須建立電話撥入式會議存取號碼：使用者要連線到會議時撥打的電話號碼。電話撥入式會議存取號碼是使用 **New-CsDialInConferencingAccessNumber** Cmdlet 所建立。當您建立新的電話撥入式會議存取號碼時，其實是在 Active Directory 網域服務中建立新的連絡人物件；此連絡人物件是用來代表存取號碼及其所有屬性。**Remove-CsDialInConferencingAccessNumber** Cmdlet 讓您可以刪除任何使用 **New-CsDialInConferencingAccessNumber** Cmdlet 所建立的電話撥入式會議號碼。當您執行 **Remove-CsDialInConferencingAccessNumber** Cmdlet 時，Cmdlet 不只會從電話撥入式會議存取號碼的集合中刪除號碼，也會刪除代表指定存取號碼的 Active Directory 連絡人物件。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsDialInConferencingAccessNumber** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDialInConferencingAccessNumber"}

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
<td><p>要移除的電話撥入式會議存取號碼的 SIP 位址 (亦即代表該號碼的連絡人物件)。指定 Identity 時，必須加上 sip: 指定 Identity 時的首碼；例如：-Identity &quot; sip:RedmondDialIn@litwareinc.com&quot;。</p></td>
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

Microsoft.Rtc.Management.Xds.AccessNumber 物件。**Remove-CsDialInConferencingAccessNumber** Cmdlet 接受存取號碼物件管線傳送的輸入。

## 傳回類型

**Remove-CsDialInConferencingAccessNumber** Cmdlet 會刪除 Microsoft.Rtc.Management.Xds.AccessNumber 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsDialInConferencingAccessNumber](get-csdialinconferencingaccessnumber.md)  
[New-CsDialInConferencingAccessNumber](new-csdialinconferencingaccessnumber.md)  
[Set-CsDialInConferencingAccessNumber](set-csdialinconferencingaccessnumber.md)

