---
title: Set-CsPersistentChatPolicy
TOCTitle: Set-CsPersistentChatPolicy
ms:assetid: b724bc13-d4fe-4529-9a48-e4cec8b7dce2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205192(v=OCS.15)
ms:contentKeyID: 49292094
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatPolicy

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的常設聊天室原則。常設聊天室原則可指定使用者是否可以存取常設聊天室。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsPersistentChatPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPersistentChatPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnablePersistentChat <$true | $false>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會為常設聊天室全域原則啟用常設聊天室。

    Set-CsPersistentChatPolicy -Identity "global" -EnablePersistentChat $True

## 範例 2

範例 2 會為組織中所有的常設聊天室原則啟用常設聊天室。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsPersistentChatPolicy** Cmdlet，以傳回所有常設聊天室原則的集合。然後，此集合會管線傳送到 **Set-CsPersistentChatPolicy** Cmdlet，以將集合中每一個原則的 EnablePersistentChat 參數設為 True ($True)。

    Get-CsPersistentChatPolicy | Set-CsPersistentChatPolicy -EnablePersistentChat $True

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

預設並不會授與使用者常設聊天室服務的權限。只有受允許使用者存取該服務之常設聊天室原則規範的使用者，才會有該項存取權。當您安裝 Lync 2013時，所有使用者皆由全域常設聊天室原則所管理，無法使用常設聊天室。若要允許所有使用者存取該項服務，只要將此全域原則中的 EnablePersistentChat 屬性設為 True 即可。除此之外也可另外在網站範圍或個別使用者範圍建立其他原則，只授予部分使用者常設聊天室的存取權。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatPolicy"}

**Lync Server 控制台：**若要使用 Lync Server 控制台 修改現有的常設聊天室原則，請依序按一下 **\[常設聊天室\]** 與 **\[常設聊天室原則\]**，然後連按兩下所要修改的原則。

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員提供原則隨附的說明文字。例如，Description 可包含被指派原則的使用者相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePersistentChat</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，受原則影響的使用者可以使用常設聊天室。設為 False 時 (預設值)，受原則影響的使用者不可以使用常設聊天室。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之常設聊天室原則的唯一識別。若要修改全域原則，請使用下列語法：</p>
<p>-Identity global</p>
<p>若要修改網站範圍原則，請使用下列語法：</p>
<p>-Identity site:Redmond</p>
<p>若要修改個別使用者原則，請使用類似下列的語法：</p>
<p>-Identity RedmondPolicy</p>
<p>若未加入 -Identity 參數， <strong>Set-CsPersistentChatPolicy</strong> Cmdlet 將自動修改全域原則。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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

**Set-CsPersistentChatPolicy** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy 物件執行個體。

## 傳回類型

無。反之， **Set-CsPersistentChatPolicy** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatPolicy](get-cspersistentchatpolicy.md)  
[Grant-CsPersistentChatPolicy](grant-cspersistentchatpolicy.md)  
[New-CsPersistentChatPolicy](new-cspersistentchatpolicy.md)  
[Remove-CsPersistentChatPolicy](remove-cspersistentchatpolicy.md)

