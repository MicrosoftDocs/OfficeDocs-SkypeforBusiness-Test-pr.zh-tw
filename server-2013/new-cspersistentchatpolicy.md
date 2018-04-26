---
title: New-CsPersistentChatPolicy
TOCTitle: New-CsPersistentChatPolicy
ms:assetid: f7d42a24-598a-4ea3-8a0f-25575b5235ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205396(v=OCS.15)
ms:contentKeyID: 49292859
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatPolicy

 

_**上次修改主題的時間：** 2015-03-09_

在網站範圍或個別使用者範圍建立新的常設聊天室原則。常設聊天室原則可指定使用者是否可以存取常設聊天室。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsPersistentChatPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnablePersistentChat <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立其 Identity 為 RedmondPersistentChatPolicy 的新個別使用者常設聊天室原則。此範例會使用參數 EnablePersistentChat 和參數值 $True 來啟用常設聊天室。

    New-CsPersistentChatPolicy -Identity "RedmondPersistentChatPolicy" -EnablePersistentChat $True

## 範例 2

範例 2 是範例 1 所示命令的另一種變化；唯一不同是新原則會套用至網站範圍，而不會套用至個別使用者範圍。作法是將 Identity 設為字串值 "site:"，再加上網站本身的名稱 (在此範例中為 site:Redmond)。

    New-CsPersistentChatPolicy -Identity "site:Redmond" -EnablePersistentChat $True

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

預設並不會授與使用者常設聊天室服務的權限。只有受允許使用者存取該服務之常設聊天室原則規範的使用者，才會有該項存取權。當您安裝 Lync 2013時，所有使用者皆由全域常設聊天室原則所管理，無法使用常設聊天室。若要允許所有使用者存取該項服務，只要將此全域原則中的 EnablePersistentChat 屬性設為 True 即可。除此之外也可另外在網站範圍或個別使用者範圍建立其他原則，只授予部分使用者常設聊天室的存取權。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatPolicy"}

**Lync Server 控制台：**若要使用 Lync Server 控制台 建立新的常設聊天室原則，請依序按一下 **\[常設聊天室\]**、**\[常設聊天室原則\]** 及 **\[新增\]**，然後按一下 **\[網站原則\]** 或 **\[使用者原則\]**。

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
<td><p>指派給原則的唯一識別碼。新的常設聊天室原則可以在網站原則範圍或個別使用者範圍建立。若要建立新的網站原則，請使用首碼 &quot;site:&quot; 以及網站名稱做為您的 Identity。例如，這個語法會為 Redmond 網站建立新的原則：</p>
<p>-Identity site:Redmond</p>
<p>若要建立新的個別使用者原則，請使用類似下列的 Identity：</p>
<p>-Identity SalesPersistentChatPolicy</p>
<p>請注意，您無法建立新的全域原則；如果您要對全域原則進行變更，請改用 <strong>Set-CsPersistentChatPolicy</strong> Cmdlet。同樣地，如果使用該 Identity 的原則已存在，您便無法建立新的網站原則或個別使用者原則。如果您需要變更現有的原則，請使用 <strong>Set-CsPersistentChatPolicy</strong> Cmdlet。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員提供原則隨附的說明文字。例如，Description 可包含被指派原則的使用者相關資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePersistentChat</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，受此原則影響的使用者可以使用常設聊天室。設為 False 時 (預設值)，受此原則影響的使用者不可以使用常設聊天室。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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

無。**New-CsPersistentChatPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsPersistentChatPolicy** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatPolicy](get-cspersistentchatpolicy.md)  
[Grant-CsPersistentChatPolicy](grant-cspersistentchatpolicy.md)  
[Remove-CsPersistentChatPolicy](remove-cspersistentchatpolicy.md)  
[Set-CsPersistentChatPolicy](set-cspersistentchatpolicy.md)

