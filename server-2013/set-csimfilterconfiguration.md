---
title: Set-CsImFilterConfiguration
TOCTitle: Set-CsImFilterConfiguration
ms:assetid: c2b08cc0-8261-4b8b-b2e9-5efa902ceb40
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412960(v=OCS.15)
ms:contentKeyID: 49292232
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsImFilterConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的立即訊息 (IM) 篩選組態。IM 篩選設定可用於禁止使用者包含有效 (可按一下) 超連結的立即訊息。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsImFilterConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsImFilterConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Action <Allow | Block | Warn>] [-AllowMessage <String>] [-BlockFileExtension <$true | $false>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-IgnoreLocal <$true | $false>] [-Prefixes <PSListModifier>] [-WarnMessage <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例所示的命令可停用 Identity 為 site:Redmond 之 IM 篩選器組態的 URI 篩選功能。為達此目的，我們會在 **Set-CsImFilterConfiguration** Cmdlet 的呼叫中指定 Enabled 參數搭配 $False 的值。

    Set-CsImFilterConfiguration -Identity site:Redmond -Enabled $False

## 範例 2

範例 2 可將 URI 前置詞 (urn:) 新增至 site:Redmond 之 IM 篩選組態所禁止的前置詞清單中。若要新增前置詞，可使用 **Get-CsImFilterConfiguration** Cmdlet 來擷取 site:Redmond 的組態，而代表該組態的回傳物件會儲存在名為 $x 的變數中。擷取設定後，我們在第二行呼叫 Add() 方法以將 urn: 新增至儲存在 Prefixes 屬性中的前置詞組合。這會變更物件參照 $x 的值。為了變更實際的組態，我們在第三行呼叫 **Set-CsImFilterConfiguration** Cmdlet，單獨以參數值形式傳遞 $x。

    $x = Get-CsImFilterConfiguration -Identity site:Redmond
    $x.Prefixes.Add("urn:")
    Set-CsImFilterConfiguration -Instance $x

## 範例 3

範例 3 執行的動作和範例 2 完全相同，差別在於範例 3 只以一行完成所有動作。在此命令中，**Set-CsImFilterConfiguration** Cmdlet 的 -Prefixes 參數可用來將 urn:新增至前置詞清單中。add 清單修飾詞可用來將這個值新增至 Prefixes 清單中。

    Set-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{add="urn:"}

## 範例 4

在此範例中，我們將前置詞 urn:移出 site:Redmond 之 IM 篩選組態所封鎖的前置詞清單之外。除了呼叫 add 清單修飾詞將前置詞新增至清單中和呼叫 remove 修飾詞移除前置詞之外，此範例和範例 3 相同。

    Set-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{remove="urn:"}

## 詳細描述

傳送立即訊息時，使用者可以在該訊息的文字中內嵌統一資源識別元 (URI)，讓交談中的其他參與者參考特定的網站或共用。您可以設定 Lync Server，以封鎖或停用具有特定首碼的超連結 (換句話說，參與者無法只是按一下連結，就前往 URI 所指的任何網站；他們必須手動複製連結並將其貼入瀏覽器)。

**Set-CsImFilterConfiguration** Cmdlet 可讓您修改要篩選的 URI 首碼清單，還能讓您一併啟用或停用全域或特定網站內的篩選功能。您也可以利用這個 Cmdlet 更新各種提供使用者警告的訊息。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsImFilterConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsImFilterConfiguration"}

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
<td><p><em>Action</em></p></td>
<td><p>選用</p></td>
<td><p>UrlFilterAction</p></td>
<td><p>當立即訊息中包含超連結時，此參數值會決定將採取的動作。</p>
<p>Allow - 將含有底線的超連結加入首碼，使連結不再為使用中的連結。除此之外，如果訊息是指定在 AllowMessage 內容中，則該訊息會插入在每個含有超連結之立即訊息的開頭。</p>
<p>Block - 封鎖包含有效超連結的訊息傳遞，Lync Server 傳送錯誤訊息給傳送者。</p>
<p>Warn - 將包含使用中的超連結的訊息傳遞給接收參與者，同時在該訊息的開頭插入警告訊息。可使用 WarnMessagehe 屬性來指定警告訊息。如果指定警告但沒有輸入 WarnMessage，雖然仍接受 BlockFileExtension 屬性的設定，IM 篩選還是會停用。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>AllowMessage</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>如果已指定此參數的值，當 Action 屬性的值設為「允許」時，每一個包含超連結的訊息開頭都會插入該字串。您可以使用此訊息通知使用者，例如按一下不明連結的潛在危險，或組織的相關原則和需求。</p></td>
</tr>
<tr class="odd">
<td><p><em>BlockFileExtension</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>如果此參數設為 True，則會封鎖包含 Extensions 屬性所指定之副檔名 (定義在 Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration 類別中) 的檔案路徑之超連結 (透過呼叫 <strong>Get-CsFileTransferFilterConfiguration</strong> Cmdlet 擷取)，並將錯誤訊息傳回給傳送者。如果將此參數設為 False，則不會針對檔案路徑和副檔名進行任何特殊檢查。</p>
<p>預設值：True</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>啟用或停用此功能。如果此參數設為 True，則會掃描超連結的立即訊息，並且套用這個組態內的規則。如果此參數設為 False，則不會檢查超連結的訊息。</p>
<p>預設值：True</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsIdentity</p></td>
<td><p>要修改之 IM 篩選器組態設定的唯一識別碼。這個值是 global 或 site:&lt;網站名稱&gt;，其中 &lt;網站名稱&gt; 代表套用設定的網站，如 site:Redmond。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreLocal</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>此參數值控制是否執行立即訊息中傳遞的近端內部網路 URI 的篩選。如果此參數設為 True，本機電腦內部網路區域上定義的所有 URI 都會被忽略(本機電腦為執行 IM 篩選應用程式的 前端伺服器)。如果此參數設為 False，會套用指定的篩選至所有超連結。</p>
<p>預設值：True</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>ImFilterConfiguration</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。這個 Cmdlet 可接受屬於 Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration 類型的物件，其可藉由呼叫 <strong>Get-CsImFilterConfiguration</strong> Cmdlet 來加以擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Prefixes</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>將篩選 URI 首碼的清單。依據指定的設定來篩選立即訊息中，含有與清單內其中一個首碼相符之首碼的超連結。</p>
<p>預設值：callto:，file:，ftp.，ftp:，gopher:，href，http:，https:，ldap:，mailto:，news:，nntp:，sip:，sips:，tel:，telnet:，www*。</p></td>
</tr>
<tr class="odd">
<td><p><em>WarnMessage</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>此參數包含警告訊息，當 Action 屬性的值設為「警告」時，該訊息會插入在含有超連結的每一個立即訊息的開頭。通常此訊息是用來陳述點選不明連結的潛在危險，或組織的相關原則和需求。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration 物件。接受管線傳送的 IM 篩選組態物件輸入。

## 傳回類型

**Set-CsImFilterConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsImFilterConfiguration](new-csimfilterconfiguration.md)  
[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

