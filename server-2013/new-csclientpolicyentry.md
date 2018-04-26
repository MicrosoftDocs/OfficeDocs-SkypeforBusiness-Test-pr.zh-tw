---
title: New-CsClientPolicyEntry
TOCTitle: New-CsClientPolicyEntry
ms:assetid: e975d048-4911-4ae6-9446-2a6363726a4a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399046(v=OCS.15)
ms:contentKeyID: 49292686
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientPolicyEntry

 

_**上次修改主題的時間：** 2015-03-09_

新增選項至 Lync Server 用戶端原則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsClientPolicyEntry -Name <String> -Value <String>

## 範例

## 範例 1

範例 1 所示的命令會示範如何將新的原則項目新增至全域用戶端原則。範例會將新的意見反應選項新增至 Lync。請注意，此範例僅供示範。您不應預期可以執行這些命令，並將類似的意見回應選項新增至您的 Lync 複本。

為了新增原則項目，範例中的第一個命令會使用 **New-CsClientPolicyEntry** Cmdlet，來建立 Name 為 OnlineFeedbackURL 且 Value 為 http://www.litwareinc.com/feedback 的項目。產生的原則項目物件會儲存於名為 $x 的變數中。

第二個命令會使用 **Get-CsClientPolicy** Cmdlet 來建立全域用戶端原則的物件參照 ($y)。建立物件參照之後，會使用 Add 方法，將新的原則項目新增至 PolicyEntry 屬性。如果 PolicyEntry 已有一或多個項目，則新值將只會附加至該集合的尾端。

最後，範例中的最後一個命令會使用 **Set-CsClientPolicy** Cmdlet，將變更寫入實際的全域原則。如果未呼叫 **Set-CsClientPolicy** Cmdlet，則您的變更只會存在記憶體中，在終止 Windows PowerShell 工作階段或刪除變數 $x 時便會立即消失。

    $x = New-CsClientPolicyEntry -Name "OnlineFeedbackURL" -Value "http://www.litwareinc.com/feedback"
    
    $y = Get-CsClientPolicy -Identity global
    $y.PolicyEntry.Add($x)
    
    Set-CsClientPolicy -Instance $y

## 範例 2

範例 2 是範例 1 所示之命令的變化。但在此案例中，新的原則項目會取代目前位於全域原則之 PolicyEntry 屬性中的所有項目。為達成此目的，範例中的第一個命令會建立新的原則項目，並將其儲存於名為 $x 的變數中。接著，第二個命令會使用 **Set-CsClientPolicy** Cmdlet，將 PolicyEntry 屬性值設定為 $x。當命令完成執行之後，PolicyEntry 屬性就只會包含新項目。所有在呼叫 **Set-CsClientPolicy** Cmdlet 之前就已包含於該屬性中的項目，都會被新項目所取代。

    $x = New-CsClientPolicyEntry -Name "OnlineFeedbackURL" -Value "http://www.litwareinc.com/feedback"
    Set-CsClientPolicy -Identity global -PolicyEntry $x

## 範例 3

範例 3 會示範如何從全域原則移除用戶端原則項目。為達此目的，範例中的第一個命令會擷取全域用戶端原則，並將資訊儲存在變數 $y 中。

擷取該全域原則後，範例中的第二個命令會使用 RemoveAt() 方法刪除該原則中的第一個原則項目。要移除的原則項目以其索引號碼表示：第一個原則項目的索引號碼為 0，第二個原則項目的索引號碼為 1，依此類推。語法 RemoveAt(0) 代表第一個原則項目會被移除。

一旦從全域原則的記憶體中的執行個體移除原則項目，系統會呼叫 **Set-CsClientPolicy** Cmdlet，將這些變更寫入全域用戶端原則的實際執行個體。

    $y = Get-CsClientPolicy -Identity global
    $y.PolicyEntry.RemoveAt(0)
    
    Set-CsClientPolicy -Instance $y 

## 範例 4

範例 4 所示的命令會移除為全域原則設定的所有用戶端原則項目。作法是使用 PolicyEntry 參數，並將參數值設為 Null ($Null)。

    Set-CsClientPolicy -Identity global -PolicyEntry $Null

## 詳細描述

用戶端原則是 Lync Server 所使用的主要機制，可管理 Lync 之類的用戶端軟體。建立或設定用戶端原則時，您有多個選項可以使用；例如，您可指定是否應在 Lync 中使用相片；立即訊息中是否可以使用表情符號；以及 Lync 是否自動儲存立即訊息工作階段的記錄等。這些選項涵蓋系統管理員需要管理之多種與用戶端相關的設定。

但是，可能並未涵蓋系統管理員需要管理的所有用戶端設定。為了增加管理彈性與擴充性，用戶端原則會包含名為 PolicyEntry 的屬性。這個多值屬性可讓系統管理員增加用戶端原則中未明確呼叫的新管理選項。例如，在推出 Lync Server 之前，讓 Beta 版測試者能夠將意見回應選項新增至 Lync。將此選項新增為新的原則項目，並使用 **New-CsClientPolicyEntry** Cmdlet 來建立。

請注意，您無法任意地建立新的原則項目，並預期這些項目可以管理 Lync 或一些其他的用戶端應用程式。而是，您將需要等候 Microsoft 通知有關可用來建構新用戶端原則項目的名稱與值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsClientPolicyEntry** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientPolicyEntry"}

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
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>新原則項目的名稱。例如：-Name &quot;OnlineFeedbackURL&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Value</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派給新原則項目的值。例如：-Value http://www.litwareinc.com/feedback。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。New-CsClientPolicyEntry Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsClientPolicyEntry** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Policy.Client.PolicyEntryType 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsClientPolicy](new-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

