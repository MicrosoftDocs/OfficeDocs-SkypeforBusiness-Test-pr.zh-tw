---
title: New-CsImFilterConfiguration
TOCTitle: New-CsImFilterConfiguration
ms:assetid: 1964cbf9-d7f1-4b4e-99d1-951ac42d82fe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398244(v=OCS.15)
ms:contentKeyID: 49290231
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsImFilterConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的立即訊息 (IM) 篩選組態。IM 篩選可用於防止使用者傳送內含使用中之超連結的立即訊息。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsImFilterConfiguration -Identity <XdsIdentity> [-Action <Allow | Block | Warn>] [-AllowMessage <String>] [-BlockFileExtension <$true | $false>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-IgnoreLocal <$true | $false>] [-InMemory <SwitchParameter>] [-Prefixes <PSListModifier>] [-WarnMessage <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會使用 **New-CsImFilterConfiguration** Cmdlet 建立 Identity 為 site:Redmond 的新 IM 篩選組態 (因為沒有指定其他參數，所以會使用預設值建立這些設定)。

    New-CsImFilterConfiguration -Identity site:Redmond

## 範例 2

這個命令使用 **New-CsImFilterConfiguration** Cmdlet 來建立 Identity 為 site:Redmond 的新 IM 篩選器組態。由於指定了 Prefixes 參數，所以新組態會包含全部的預設值，包括篩選的預設首碼，加上兩個其他 URI 首碼：rtsp:和 urn:。我們使用新增清單修飾詞來新增這些首碼，將這些首碼新增至預設清單。

    New-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{add="rtsp:","urn:"}

## 範例 3

這個命令使用 **New-CsFileTransferFilterConfiguration** Cmdlet 來建立 Identity 為 site:Redmond 的新 IM 篩選器組態。這個範例和範例 2 類似，除了使用取代清單修飾詞代替新增清單修飾詞以外。這表示所有預設 URI 首碼都會被這兩個首碼取代 (rtsp:和 urn:)。因此，只有含有 rtsp: 或 urn: 首碼的 URI 會在網站 Redmond 的立即訊息內篩選。

    New-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{replace="rtsp:","urn:"}

## 詳細描述

傳送立即訊息時，使用者可以在該訊息的文字中內嵌一個統一資源識別元 (URI)，讓交談中的其他參與者參考特定的網站或共用。您可以設定 Lync Server，以封鎖或停用具有特定首碼的超連結 (換句話說，參與者無法只是按一下連結，就被帶往 URI 所指的任何地方；他們必須手動將連結複製並貼入瀏覽器)。

除了可在特定網站內啟用及停用所有篩選之外，**New-CsImFilterConfiguration** Cmdlet 還可讓您定義要篩選的 URI 首碼清單。呼叫只含有指定的 Identity 之 **New-CsImFilterConfiguration** Cmdlet 可建立含有該識別的新組態，使用一組將篩選的預設首碼來填入該網站的首碼清單。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsImFilterConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsImFilterConfiguration"}

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
<td><p>XdsIdentity</p></td>
<td><p>指定 IM 篩選組態範圍的唯一識別碼。全域設定根據預設存在，並且無法使用 <strong>New-CsImFilterConfiguration</strong> Cmdlet 重新建立，但您可以指定 site:&lt;網站名稱&gt; 的 Identity 來建立網站層級的設定，其中，&lt;網站名稱&gt; 是將套用設定的網站名稱 (例如 site:Redmond)。</p>
<p>完整資料類型：Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
</tr>
<tr class="even">
<td><p><em>Action</em></p></td>
<td><p>選用</p></td>
<td><p>UrlFilterAction</p></td>
<td><p>當立即訊息中包含超連結時，此參數值會決定將採取的動作。</p>
<p>Allow - 將含有底線的超連結加入首碼，使連結不再為使用中的連結。如果訊息是指定在 AllowMessage 內容中，則該訊息會插入在每個含有超連結之立即訊息的開頭。</p>
<p>Block - 封鎖包含有效超連結的訊息傳遞，Lync Server 傳送錯誤訊息給傳送者。</p>
<p>Warn - 將包含使用中的超連結的訊息傳遞給接收參與者，同時在該訊息的開頭插入警告訊息。可使用 WarnMessagehe 屬性來指定警告訊息。如果指定警告但沒有輸入 WarnMessage，雖然仍接受 BlockFileExtension 屬性的設定，IM 篩選還是會停用。</p>
<p>預設值：允許，除非訊息包含超過 1,000 個 URL，這種情況預設值為「Block」。</p>
<p>完整資料類型：Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.UrlFilterAction</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowMessage</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如果已指定此參數的值，當 Action 屬性的值設為「Allow」時，每一個包含超連結的訊息開頭都會插入該字串。您可以使用此訊息通知使用者，例如按一下不明連結的潛在危險，或組織的相關原則和需求。</p></td>
</tr>
<tr class="even">
<td><p><em>BlockFileExtension</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>若此參數設為 True，則會封鎖包含 Extensions 屬性所指定之副檔名 (定義在 Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration 類別中) 的檔案路徑之超連結 (透過呼叫 <strong>Get-CsFileTransferFilterConfiguration</strong> Cmdlet 擷取)，並將錯誤訊息傳回給傳送者 如果此參數設為 False，則不對副檔名進行特別檢查。</p>
<p>預設值：True</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>啟用或停用此功能。若此參數設為 True，則會掃描超連結的立即訊息，並且套用這個組態內的規則。如果此參數設為 False，則不會檢查超連結的訊息。</p>
<p>預設值：True</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreLocal</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>此參數值控制是否執行立即訊息中傳遞的近端內部網路 URI 的篩選。如果此參數設為 True，本機電腦內部網路區域上定義的所有 URI 都會被忽略(本機電腦為執行 IM 篩選應用程式的前端伺服器)。如果此參數設為 False，會套用指定的篩選至所有超連結。</p>
<p>預設值：True</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>Prefixes</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>將篩選 URI 首碼的清單。依據指定的設定來篩選立即訊息中，含有與清單內其中一個首碼相符之首碼的超連結。</p>
<p>預設值：callto:, file:, ftp., ftp:, gopher:, href, http:, https:, ldap:, mailto:, news:, nntp:, sip:, sips:, tel:, telnet:, www*。</p></td>
</tr>
<tr class="odd">
<td><p><em>WarnMessage</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>此參數包含警告訊息，當 Action 屬性的值設為「Warn」時，該訊息會插入在含有超連結的每一個立即訊息的開頭。通常此訊息是用來陳述點選不明連結的潛在危險，或組織的相關原則和需求。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

建立類型 Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration 的物件。

## 請參閱

#### 其他資源

[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Set-CsImFilterConfiguration](set-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

