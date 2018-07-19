---
title: Lync Server 2013 中的 PurgeSettings 表
TOCTitle: Lync Server 2013 中的 PurgeSettings 表
ms:assetid: 9ff2c8fc-4ae8-4f22-96a8-1f4d5eecbf2d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205121(v=OCS.15)
ms:contentKeyID: 49291831
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 PurgeSettings 表

 

_**上次修改主題的時間：** 2015-03-09_

PurgeSettings 表格包含用於指定是否 (及何時) 會自動從 CDR 資料庫刪除過時詳細通話記錄的資訊。請注意，執行下列命令，也可以從 Microsoft Lync Server 2013 管理命令介面取得清除相關資訊：

    Get-CsCdrConfiguration

系統管理員應將 PurgeSettings 表格視為唯讀狀態：只能使用 [New-CsCdrConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsCdrConfiguration) 或 [Set-CsCdrConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCdrConfiguration) Cmdlet 變更詳細通話記錄清除設定。

本表已從 Microsoft Lync Server 2013 引進使用。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>資料類型</th>
<th>索引鍵/索引</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>識別碼</strong></p></td>
<td><p>int</p></td>
<td><p>主要</p></td>
<td><p>CDR 清除設定集合的唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>EnablePurge</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>若設定為 True (1)，Microsoft Lync Server 2013 會定期從 CDR 資料庫清除過時的記錄。系統會在 PurgeHour 設定指定的時間每天進行清除。若設定為 False (0)，就不會自動從資料庫清除記錄。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><strong>KeepCallDetailForDays</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>指定將從資料庫清除之 CDR 記錄的存留期 (天數)：如果已啟用清除功能，就會從資料庫移除存留期大於此值的 CDR 記錄。預設值是 60 天。</p></td>
</tr>
<tr class="even">
<td><p><strong>KeepErrorReportForDays</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>指定將從資料庫清除之錯誤報告記錄的存留期 (天數)：如果已啟用清除功能，就會從資料庫移除存留期大於此值的錯誤報告記錄。預設值是 60 天。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PurgeHour</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>指定一天中進行資料庫清除作業的當地時間。一天中的時間是以 24 小時制指定，其中 0 表示午夜 (12:00 AM)，而 23 表示 11:00 PM。請注意，您僅能指定一天中的小時數：允許值為 10 (表示 10:00 AM)，但不允許值為 10.5 (表示 10:30 AM)。預設值為 2 (2:00 AM)。</p></td>
</tr>
</tbody>
</table>

