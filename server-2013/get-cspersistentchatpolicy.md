---
title: Get-CsPersistentChatPolicy
TOCTitle: Get-CsPersistentChatPolicy
ms:assetid: 0f33d177-dec6-44a3-a9ef-dd39029a4ddd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204673(v=OCS.15)
ms:contentKeyID: 49290100
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatPolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之常設聊天室原則的資訊。常設聊天室原則可指定使用者是否可以存取常設聊天室。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPersistentChatPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPersistentChatPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織之用之所有常設聊天室原則的資訊。

    Get-CsPersistentChatPolicy

## 範例 2

範例 2 只會傳回 Identity 為 RedmondPersistentChatPolicy 之個別使用者常設聊天室原則的資訊。

    Get-CsPersistentChatPolicy -Identity "RedmondPersistentChatPolicy"

## 範例 3

範例 3 會傳回在網站範圍所設定之所有常設聊天室原則的資訊。作法是加入 Filter 參數及 "site:\*" 參數值。

    Get-CsPersistentChatPolicy -Filter "site:*"

## 範例 4

範例 4 只會傳回啟用常設聊天室之常設聊天室原則的資訊。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsPersistentChatPolicy** Cmdlet，以傳回設定供組織使用之所有常設聊天室原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 EnablePersistentChat 屬性等於 True ($True) 的原則。

    Get-CsPersistentChatPolicy | Where-Object {$_.EnablePersistentChat -eq $True}

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

預設並不會授與使用者常設聊天室服務的權限。只有受允許使用者存取該服務之常設聊天室原則規範的使用者，才會有該項存取權。當您安裝 Lync 2013時，所有使用者皆由全域常設聊天室原則所管理，無法使用常設聊天室。若要允許所有使用者存取該項服務，只要將此全域原則中的 EnablePersistentChat 屬性設為 True 即可。除此之外也可另外在網站範圍或個別使用者範圍建立其他原則，只授予部分使用者常設聊天室的存取權。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatPolicy"}

**Lync Server 控制台：**若要在 Lync Server 控制台 中檢視常設聊天室原則資訊，請按一下 **\[常設聊天室\]**，然後按一下 **\[常設聊天室原則\]**。

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
<td><p>System.Strkng</p></td>
<td><p>可讓您在搜尋常設聊天室原則時使用萬用字元。例如，若要尋找在網站範圍所設定的所有原則，請使用下列語法：</p>
<p>-Filter &quot;site:*&quot;</p>
<p>請勿在同一個命令中同時使用 Filter 參數和 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>建立原則時指派給原則的唯一識別碼。常設聊天室原則可以就全域、網站或個別使用者範圍進行指派。若要參照全域執行個體，請使用下列語法：</p>
<p>-Identity global</p>
<p>若要參照網站範圍的原則，請使用下列語法：</p>
<p>-Identity site:Redmond</p>
<p>若要參照個別使用者範圍的原則，請使用類似下列的語法：</p>
<p>-Identity RedmondPersistentChatPolicy</p>
<p>Identity 參數不能使用萬用字元，例如星號 (*)。若要以萬用字元搜尋原則，請改用 Filter 參數。</p>
<p>若未指定 Identity 或 Filter 參數， <strong>Get-CsPersistentChatPolicy</strong> Cmdlet 會傳回設定供組織之用之所有常設聊天室原則的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取常設聊天室原則資料，而不從中央管理存放區擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsPersistentChatPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPersistentChatPolicy** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Grant-CsPersistentChatPolicy](grant-cspersistentchatpolicy.md)  
[New-CsPersistentChatPolicy](new-cspersistentchatpolicy.md)  
[Remove-CsPersistentChatPolicy](remove-cspersistentchatpolicy.md)  
[Set-CsPersistentChatPolicy](set-cspersistentchatpolicy.md)

