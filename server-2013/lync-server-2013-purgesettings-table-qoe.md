---
title: PurgeSettings 表 (QoE)
TOCTitle: PurgeSettings 表 (QoE)
ms:assetid: 31b85d1c-3f32-4f67-94bf-9389cdd282c5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204788(v=OCS.15)
ms:contentKeyID: 49290511
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# PurgeSettings 表 (QoE)

 

_**上次修改主題的時間：** 2015-03-09_

PurgeSettings 資料表包含指定在經驗品質記錄過期時，會自動從 QoE 資料庫加以刪除的資訊。此外您也可透過執行下列命令，從 Microsoft Lync Server 2013 管理命令介面取得這些清除相關的資訊：

    Get-CsQoEConfiguration

Microsoft Lync Server 2013 中即引入了此資料表。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>欄</strong></th>
<th><strong>資料類型</strong></th>
<th><strong>索引鍵/索引</strong></th>
<th><strong>詳細資料</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>識別碼</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>QoE 清除設定集的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>EnablePurge</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>設為 True (1) 時，Microsoft Lync Server 2013 會定期從 QoE 資料庫清除過期的記錄。清除動作會每天在 PurgeHour 設定中指定的時間加以執行。若設為 False (0)，就不會從資料庫自動清除記錄。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><strong>KeepQoEDataForDays</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>指定要從資料庫清除之 QoE 記錄的存留期 (以天數為單位)：若啟用清除，就會從資料庫移除舊於此值的 QoE。預設值為 60 天。</p></td>
</tr>
<tr class="even">
<td><p><strong>PurgeHour</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>指定要執行資料庫清除的時間。時間是以 24 小時制指定，0 代表午夜 (上午 12:00)，而 23 則代表下午 11:00。請注意，您僅能指定時間的時數：允許將值設為 10 (代表上午 10:00)，但不允許設為 10:30 的 10.5 (代表上午 10:30)。預設值為 1 (上午 1:00)。指定要執行資料庫清除的時間。時間是以 24 小時制指定，0 代表午夜 (上午 12:00)，而 23 則代表下午 11:00。請注意，您僅能指定時間的時數：允許將值設為 10 (代表上午 10:00)，但不允許設為 10:30 的 10.5 (代表上午 10:30)。預設值為 1 (上午 1:00)。</p></td>
</tr>
</tbody>
</table>

