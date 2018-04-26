---
title: Remove-CsPersistentChatPolicy
TOCTitle: Remove-CsPersistentChatPolicy
ms:assetid: d6bfe22b-084b-4d7f-8e4a-58f738493b31
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205301(v=OCS.15)
ms:contentKeyID: 49292437
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatPolicy

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的常設聊天室原則。常設聊天室原則可指定使用者是否可以存取常設聊天室。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsPersistentChatPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除其 Identity 為 RedmondPersistentChatPolicy 的個別使用者常設聊天室原則。

    Remove-CsPersistentChatPolicy -Identity "RedmondPersistentChatPolicy"

## 範例 2

範例 2 會刪除套用至網站範圍的所有常設聊天室原則。為達成此目的，命令會先使用 **Get-CsPersistentChatPolicy** Cmdlet 搭配 Filter 參數，以傳回在網站範圍設定的所有常設聊天室原則 (作法是使用篩選值 "site:\*")。然後將這些原則管線傳送到 **Remove-CsPersistentChatPolicy** Cmdlet 加以刪除。

    Get-CsPersistentChatPolicy -Filter "site:*" | Remove-CsPersistentChatPolicy

## 範例 3

範例 3 會刪除已啟用常設聊天室的所有常設聊天室原則。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsPersistentChatPolicy** Cmdlet，以傳回設定供組織使用之所有常設聊天室原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 EnablePersistentChat 屬性等於 True ($True) 的原則。接著將該集合管線傳送到 **Remove-CsPersistentChatPolicy** Cmdlet，以刪除集合中的每一個原則。

    Get-CsPersistentChatPolicy | Where-Object {$_.EnablePersistentChat -eq $True} | Remove-CsPersistentChatPolicy

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

預設並不會授與使用者常設聊天室服務的權限。只有受允許使用者存取該服務之常設聊天室原則規範的使用者，才會有該項存取權。當您安裝 Lync 2013時，所有使用者皆由全域常設聊天室原則所管理，無法使用常設聊天室。若要允許所有使用者存取該項服務，只要將此全域原則中的 EnablePersistentChat 屬性設為 True 即可。除此之外也可另外在網站範圍或個別使用者範圍建立其他原則，只授予部分使用者常設聊天室的存取權。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatPolicy"}

**Lync Server 控制台：**若要使用 Lync Server 控制台 移除常設聊天室原則，請按一下 **\[常設聊天室\]**，然後按一下 **\[常設聊天室原則\]**。選取所要移除的原則，按一下 **\[編輯\]**，然後按一下 **\[刪除\]**。

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
<td><p>要刪除之常設聊天室原則的唯一識別。若要移除網站範圍原則，請使用類似下列的語法：</p>
<p>-Identity site:Redmond</p>
<p>若要刪除個別使用者原則，請使用類似下列的語法：</p>
<p>-Identity RedmondPolicy</p>
<p>您也可以對全域的常設聊天室原則執行 <strong>Remove-CsPersistentChatPolicy</strong> Cmdlet。但在此情況下，不會實際刪除全域原則，而是會將全域原則中的所有屬性重設為預設值。</p></td>
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
<td><p>如果存在，將導致 <strong>Remove-CsPersistentChatPolicy</strong> Cmdlet 刪除個別使用者原則，即使原則目前已指派給至少一位使用者也一樣。如果不存在，系統將要求您在移除仍在使用中的原則之前，先確認刪除要求。</p></td>
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

**Remove-CsPersistentChatPolicy** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy 物件執行個體。

## 傳回類型

無。反之， **Remove-CsPersistentChatPolicy** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatPolicy](get-cspersistentchatpolicy.md)  
[Grant-CsPersistentChatPolicy](grant-cspersistentchatpolicy.md)  
[New-CsPersistentChatPolicy](new-cspersistentchatpolicy.md)  
[Set-CsPersistentChatPolicy](set-cspersistentchatpolicy.md)

