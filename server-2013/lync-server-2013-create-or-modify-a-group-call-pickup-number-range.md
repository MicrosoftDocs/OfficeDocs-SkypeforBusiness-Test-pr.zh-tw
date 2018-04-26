---
title: 建立或修改群組來電接聽號碼範圍
TOCTitle: 建立或修改群組來電接聽號碼範圍
ms:assetid: 4b442b98-df6b-4e50-8254-b3be9cde21dd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945627(v=OCS.15)
ms:contentKeyID: 52056105
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改群組來電接聽號碼範圍

 

_**上次修改主題的時間：** 2013-01-30_

您可使用下列程序在通話駐留範圍表中建立或修改來電接聽群組號碼範圍。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須使用 Lync Server 管理命令介面才能在通話駐留範圍表中建立、修改、移除及檢視群組來電接聽號碼範圍。Lync Server 控制台無法使用群組來電接聽號碼範圍。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>來電接聽群組號碼範圍必須指派為 GroupPickup 類型。只有指派給使用者的群組號碼為 GroupPickup 類型，使用者才可啟用於群組來電接聽。</td>
</tr>
</tbody>
</table>


來電接聽群組號碼範圍必須符合下列規則︰

  - 該範圍的起始號碼必須小於或等於範圍的結束號碼。

  - 該範圍的起始號碼值的長度必須等於範圍的結束號碼值長度。

  - 號碼範圍必須是唯一的。此範圍不得與其他任何範圍重疊。

  - 如果號碼範圍開頭為字元 \* 或 \#，則範圍必須大於 100。

  - 有效值：必須符合規則運算式字串 (\[\\\*|\#\]?\[1-9\]\\d{0,7})|(\[1-9\]\\d{0,8})。這表示值必須是開頭為字元 \* 或 \# 或數字 1 至 9 的字串 (第一個字元不得為零)。如果第一個字元是 \* 或 \#，則後續一個字元必須是數字 1 至 9 (不得為零)。之後的後續字元可以是 0 至 9 的任何數字，且最多再加上七個字元 (例如，"\#6000"、"\*92000"、"\*95551212" 及 "915551212")。如果第一個字元不是 \* 或 \#，則第一個字元必須是數字 1 至 9 (不得為零)，後面最多可接著八個字元，且每個字元都是數字 0 至 9 (例如，"915551212"、"41212"、"300")。

## 建立或修改來電接聽群組範圍

1.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  使用 **New-CsCallParkOrbit** 來建立新的來電接聽群組號碼範圍。使用 **Set-CsCallParkOrbit** 來修改現有的來電接聽號碼範圍。
    
    請在命令列執行：
    
        New-CsCallParkOrbit -Identity <name of call pickup group range> -NumberRangeStart <first number in range> -NumberRangeEnd <last number in range> -CallParkService <FQDN or service ID of the Application service that hosts the Call Park application> -Type GroupPickup
    
    例如︰
    
        New-CsCallParkOrbit -Identity "Redmond call pickup" -NumberRangeStart 100 -NumberRangeEnd 199 -CallParkService redmond-applicationserver-1 -Type GroupPickup
    
    下列範例顯示如何將號碼範圍從通話駐留範圍變更為來電接聽群組。
    
        Set-CsCallParkOrbit -Identity "Redmond call pickup" -Type GroupPickup
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>只有在一開始指定錯誤的類型，且群組範圍尚未在使用中，才可使用此 Cmdlet 來變更指派給號碼範圍的類型。如果將號碼範圍從 CallPark 變更為 GroupPickup，或從 GroupPickup 變更為 CallPark，但號碼範圍已在使用中，則該號碼範圍的「通話駐留」或群組來電接聽將會停止運作。例如，如果將號碼範圍從 CallPark 變更為 GroupPickup，則通話駐留應用程式將無法使用該範圍範圍來駐留通話。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 工作

[刪除通話保留範圍](lync-server-2013-delete-a-call-park-orbit-range.md)  

#### 其他資源

[New-CsCallParkOrbit](new-cscallparkorbit.md)  
[Set-CsCallParkOrbit](set-cscallparkorbit.md)

