---
title: Get-CsDialInConferencingLanguageList
TOCTitle: Get-CsDialInConferencingLanguageList
ms:assetid: 39355144-c8de-4ad3-9568-6426d3b97ccb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425869(v=OCS.15)
ms:contentKeyID: 49290621
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDialInConferencingLanguageList

 

_**上次修改主題的時間：** 2015-03-09_

傳回 Lync Server 電話撥入式會議所支援的語言清單，包括方言/少數民族語言。這些語言會用於將音訊訊息與指示轉送給透過電話參與會議的使用者。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsDialInConferencingLanguageList [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDialInConferencingLanguageList [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 示範如何查詢 **Get-CsDialInConferencingLanguageList** Cmdlet，以了解特定的語言是否出現在支援的語言清單。此範例會呼叫 **Get-CsDialInConferencingLanguageList** Cmdlet，以傳回所有支援語言的資訊；接著再使用 Windows PowerShell 運算子 -contains，以了解該支援語言的清單中是否包含語言代碼 "en-US"。如果有，**Get-CsDialInConferencingLanguageList** Cmdlet 會回報 "True" 值。如果在支援的語言清單中找不到 "en-US"，則 Cmdlet 會回報 "False"。

    (Get-CsDialInConferencingLanguageList).Languages -contains "en-US"

## 範例 2

範例 2 所示的命令會傳回完整的支援語言清單。DialInConferencingLanguageList 物件會將此資訊儲存在 Languages 屬性中。為了在畫面上顯示每種語言，此命令會先使用 **Get-CsDialInConferencingLanguageList** Cmdlet 傳回所有語言清單及其屬性的集合。會以括弧括住對 **Get-CsDialInConferencingLanguageList** Cmdlet 的呼叫，以確保 Windows PowerShell 會先執行此作業，再進行其他作業。在傳回資訊後，會使用標準的「點標記法」(物件名稱後面加上句點，再加上屬性名稱) 顯示儲存在 Languages 屬性中的所有值。

    (Get-CsDialInConferencingLanguageList).Languages

## 詳細描述

Lync Server 可讓使用者透過電話加入會議，這些以電話撥入方式參與的使用者無法檢視視訊或交換立即訊息，但他們可以完全參與會議的音訊部分。當使用者透過電話連線到會議時，他們會先聽到歡迎訊息，然後會聽到如何加入會議的指示(例如，根據會議設定方式不同，系統可能會要求使用者先說出自己的姓名，再按下井字 (\#) 鍵)。Lync Server 在各種狀況下可能需要發出額外的訊息或指示；例如，當使用者按下電話鍵盤上的 1，系統就會唸出使用者所有其他可用鍵盤選項的清單。

系統管理員可設定一或多個電話撥入式會議用於轉送訊息與指示的語言。**Get-CsDialInConferencingLanguageList** Cmdlet 可傳回支援的語言清單。系統會使用 5 個字元的語言代碼來傳回清單 (例如 ca-ES 代表卡達隆尼亞文)。

支援的語言清單為唯讀。您無法在清單上新增語言；因為您沒有辦法將新的支援語言新增到電話撥入式會議。請注意，可用語言清單是在全域範圍設定的，您無法將不同的清單指派給不同的網站。(但您可以將不同的語言指派給不同的電話撥入式會議存取號碼)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsDialInConferencingLanguageList** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDialInConferencingLanguageList"}

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>在指定電話撥入式語言清單時允許您使用萬用字元。因為只有一個物件 (全域)，所以您不必使用 Filter 或 Identity 參數傳回語言清單。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指出待傳回的電話撥入式會議語言清單。此時只有一個物件：全域。因此在呼叫 <strong>Get-CsDialInConferencingLanguageList</strong> Cmdlet 時，無須加入此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取語言清單，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsDialInConferencingLanguageList** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsDialInConferencingLanguageList** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingLanguageList 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsDialInConferencingAccessNumber](new-csdialinconferencingaccessnumber.md)  
[Set-CsDialInConferencingAccessNumber](set-csdialinconferencingaccessnumber.md)

