---
title: Get-CsAnnouncement
TOCTitle: Get-CsAnnouncement
ms:assetid: d692b377-8df2-4668-b9d3-06458dd4d96d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398937(v=OCS.15)
ms:contentKeyID: 49292436
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAnnouncement

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之 Lync Server 宣告的資訊。宣告會在使用者撥打有效但未經指派的電話號碼時播放，其可以是訊息 (例如 "This number is temporarily out of service" (此號碼暫時無法提供服務)) 或忙線訊號。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAnnouncement [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsAnnouncement [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回設定供組織使用的所有宣告。作法是呼叫不含任何參數的 **Get-CsAnnouncement** Cmdlet。

    Get-CsAnnouncement

## 範例 2

範例 2 所示的命令會傳回一個宣告：Identity 為 ApplicationServer:redmond.litwareinc.com/1951f734-c80f-4fb2-965d-51807c792b90 的宣告。如需擷取特定宣告的替代方法 (可以說是比較簡單的方法)，請參閱範例 5。

    Get-CsAnnouncement -Identity "ApplicationServer:redmond.litwareinc.com/1951f734-c80f-4fb2-965d-51807c792b90" 

## 範例 3

範例 3 所示的命令會傳回所有針對在 ApplicationServer:redmond.litwareinc.com 服務上使用而設定之宣告的資訊。

    Get-CsAnnouncement -Identity "ApplicationServer:redmond.litwareinc.com"

## 範例 4

範例 4 會傳回所有針對在 Redmond 網站 (所有網域上) 中使用而設定之宣告的資訊。完成這項作業的方法是，加上 Filter 參數和篩選值 "\*ApplicationServer:Redmond\*"，如此可將傳回的資料限制為 Identity 包含 "ApplicationServer:Redmond" 字串值的宣告。根據定義，這些宣告是針對在 Redmond site 中使用而設定的宣告。

    Get-CsAnnouncement -Filter "*ApplicationServer:Redmond*"

## 範例 5

範例 5 示範傳回特定宣告或宣告組的替代方法；此範例會傳回所有名為 Welcome Announcement 的宣告。為達成此目的，會先呼叫不含任何參數的 **Get-CsAnnouncement** Cmdlet，以傳回組織使用之所有宣告的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 Name 等於 (-eq) "Welcome Announcement" 的宣告。

    Get-CsAnnouncement | Where-Object {$_.Name -eq "Welcome Announcement"}

## 範例 6

範例 6 和範例 5 相似，不過此範例會示範另一個傳回單一宣告的方法。我們再次呼叫 **Get-CsAnnouncement** Cmdlet，不過這次需要將 Identity 指定為 ApplicationServer:redmond.litwareinc.com。如此可傳回所有與該服務相關聯之宣告的集合。和範例 5 一樣，會將此集合管線傳送到 **Where-Object** Cmdlet，這會挑出 Name 等於 (-eq) "Welcome Announcement" 的宣告。由於 應用程式服務 Cmdlet 中的宣告名稱必須是唯一，所以，此命令絕對不會傳回一個以上的項目。

    Get-CsAnnouncement -Identity "ApplicationServer:redmond.litwareinc.com" | Where-Object {$_.Name -eq "Welcome Announcement"}

## 範例 7

此範例和範例 5 相似，我們會先擷取所有宣告，然後再將宣告的集合傳送到 **Where-Object** Cmdlet。然而在範例 5 中，我們在 Where 子句中使用 –eq 運算子來找出名稱完全相符的項目。在此範例中，我們使用 –like 運算子和萬用字元值來找出所有宣告。在此案例中即是開頭為 Welcome 字串的宣告。

    Get-CsAnnouncement | Where-Object {$_.Name -like "Welcome*"}

## 範例 8

範例 8 會傳回使用文字轉換語音 (TTS) 提示 (做為主要宣告或音訊檔的遞補)，但語言不是「英文 (美國)」的所有宣告。為了執行此工作，命令會先呼叫 **Get-CsAnnouncement** Cmdlet，以傳回目前已設定之所有宣告的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以選取所有 TextToSpeechPrompt 屬性不是空白 (不等於 $Null) 且 Language 屬性不等於 (-ne) en-US 的宣告。

    Get-CsAnnouncement | Where-Object {($_.TextToSpeechPrompt -ne $Null) -and ($_.Language -ne "en-US")}

## 詳細描述

組織可擁有未指派給使用者或話機的電話號碼，但它仍然是可撥打的有效號碼。根據預設，當某人撥打其中一個電話號碼，該來電者會收到忙線訊號，且來電可能會導致傳回 SIP 用戶端的錯誤。透過將宣告設定套用至未指派的號碼，系統管理員可播放訊息、傳回忙線訊號或將來電重新導向。此 Cmdlet 會擷取其中一或多個宣告設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsAnnouncement** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAnnouncement"}

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
<td><p>此參數可讓您執行萬用字元搜尋，以便搜尋所有為組織設定之宣告的 Identity。您可以使用萬用字元 (*) 來篩選 Identity 的任何部分。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之宣告的識別碼。如果省略此參數和 Filter 參數，系統會顯示所有為組織設定之宣告的執行個體。您可以利用下列兩種方法提供 Identity 參數的值：</p>
<p>- 針對您要擷取的多個宣告，輸入 應用程式服務 的 Identity。這將擷取所有以指定服務 Identity 設定的宣告。例如，ApplicationServer:Redmond.litwareinc.com。</p>
<p>- 針對您要擷取的單一宣告，輸入完整的 Identity。此值將永遠為 &lt;serviceID&gt;/&lt;GUID&gt; 格式，其中 serviceID 是執行宣告服務之應用程式伺服器的 Identity，而 GUID 是與此宣告相關聯的全域唯一識別碼。例如：ApplicationServer:Redmond.litwareinc.com/bef5fa3b-3c97-4af0-abe7-611deee7616c.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取宣告資訊，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

傳回 Microsoft.Rtc.Management.WritableConfig.Settings.AnnouncementServiceSettings.Announcement 物件的一個或多個執行個體。

## 請參閱

#### 其他資源

[New-CsAnnouncement](new-csannouncement.md)  
[Remove-CsAnnouncement](remove-csannouncement.md)  
[Set-CsAnnouncement](set-csannouncement.md)  
[Import-CsAnnouncementFile](import-csannouncementfile.md)

