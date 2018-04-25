---
title: Get-CsServerVersion
TOCTitle: Get-CsServerVersion
ms:assetid: 66af07c0-fdfe-491a-ad48-b8821fb58904
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398470(v=OCS.15)
ms:contentKeyID: 49291158
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsServerVersion

 

_**上次修改主題的時間：** 2015-03-09_

傳回執行 Lync Server 之電腦的伺服器授權資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsServerVersion

## 範例

## 範例 1

範例 1 所示的命令會傳回本機電腦的授權資訊。這是可以使用 **Get-CsServerVersion** Cmdlet 的唯一方式。

    Get-CsServerVersion

## 詳細描述

Lync Server 有兩種不同版本：試用版 (最後會到期) 和完整授權版。**Get-CsServerVersion** Cmdlet 可協助系統管理員判斷電腦上所執行的 Lync Server 版本。**Get-CsServerVersion** Cmdlet 的設計上只能在本機電腦上執行，而且沒有其他參數，會嘗試讀取登錄值 HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Real-Time Communications\\{A593FD00-64F1-4288-A6F4-E699ED9DCA35}\\Type。接著，Cmdlet 會根據該登錄值回報軟體的版本號碼和 Lync Server 授權資訊。該授權資訊會告知您下列其中一項：

已安裝試用授權金鑰。

已安裝大量授權金鑰。

安裝在本機電腦上的元件不需授權金鑰 (只有以 前端伺服器、Director 或 Edge Server 身分運作的電腦才需要授權)。

如果發生錯誤，**Get-CsServerVersion** Cmdlet 會報告無法擷取授權類型和版本資訊，並建議您重新安裝 Lync Server 元件。

請注意，Get-CsServerVersion 只會傳回基礎版本號碼。例如，Get-CsServerVersion 將會傳回例如 5.0.8308 的值，即使更新已正式將版本號碼變更為 5.0.8308.291 也是如此。如果您需要一個非常特定的版本號碼，應使用 Windows \[控制台\]。

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsServerVersion** Cmdlet 不支援管線傳送的輸入。

## 傳回類型

**Get-CsServerVersion** Cmdlet 會傳回字串值。

