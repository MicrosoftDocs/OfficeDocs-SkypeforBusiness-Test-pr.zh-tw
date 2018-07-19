---
title: 修改裝置更新記錄檔的設定
TOCTitle: 修改裝置更新記錄檔的設定
ms:assetid: 9b57f126-1853-43b3-bbd4-06401e6498bd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182554(v=OCS.15)
ms:contentKeyID: 49291796
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 修改裝置更新記錄檔的設定

 

_**上次修改主題的時間：** 2015-03-09_

您可以使用 Lync Server 控制台或 Lync Server 管理命令介面，針對組織中記錄裝置更新資訊的方式來變更設定。下表顯示哪些設定是可以修改的，以及您可以使用哪些工具修改設定。

您可以變更並套用全域的記錄檔設定，或針對個別網站進行變更與套用。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>若要變更</th>
<th>請使用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>記錄檔的大小上限 (以位元組計)</p></td>
<td><p>Lync Server 控制台</p>
<p>- 或者 -</p>
<p>Lync Server 管理命令介面</p></td>
</tr>
<tr class="even">
<td><p>快取中可保留的資訊量上限 (以位元組計)</p></td>
<td><p>Lync Server 控制台</p>
<p>- 或者 -</p>
<p>Lync Server 管理命令介面</p></td>
</tr>
<tr class="odd">
<td><p>將快取資訊寫入記錄檔的頻率 (以分鐘計)</p></td>
<td><p>Lync Server 控制台</p>
<p>- 或者 -</p>
<p>Lync Server 管理命令介面</p></td>
</tr>
<tr class="even">
<td><p>保留記錄檔的期限 (以天數計)</p></td>
<td><p>Lync Server 控制台</p>
<p>- 或者 -</p>
<p>Lync Server 管理命令介面</p></td>
</tr>
<tr class="odd">
<td><p>檢查應該刪除之到期檔案的時機 (一天內的時間)</p></td>
<td><p>Lync Server 管理命令介面</p></td>
</tr>
<tr class="even">
<td><p>允許的記錄檔副檔名</p></td>
<td><p>Lync Server 管理命令介面</p></td>
</tr>
<tr class="odd">
<td><p>保留的記錄檔類型</p></td>
<td><p>Lync Server 管理命令介面</p></td>
</tr>
</tbody>
</table>


## 使用 Lync Server 控制台變更記錄設定

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  按一下左側導覽列中的 **\[用戶端\]**，然後再按一下 **\[裝置記錄檔設定\]**。

3.  在 **\[裝置記錄檔設定\]** 頁面中，按兩下要變更的設定。

4.  在 \[編輯記錄檔設定\] 對話方塊中，變更以下任一設定：
    
      - **最大檔案大小 (位元組)**   指定記錄檔在遭到清除前允許的最大檔案大小。預設值為 1,024,000 位元組 (1 MB)。
    
      - **最大快取大小 (位元組)**   指定在必須清除快取並將資料寫入記錄檔之前，可保存在記錄檔快取中的資訊數量上限 (以位元組為單位)。預設值為 512,000 位元組 (0.5 MB)。
    
      - **快取清除分鐘數 (1-60)**   表示將儲存在記錄檔快取中的資訊寫入實際記錄檔的頻率。當資料記錄之後，快取便會遭到清除。預設值為 5 分鐘。
    
      - **記錄檔保留天數 (1-365)**   指定記錄檔在清除之前要保留的天數。預設值為 10 天。

5.  按一下 **\[認可\]**。

## 使用 Windows PowerShell Cmdlet 變更記錄設定

裝置更新記錄檔設定可使用 Windows PowerShell 和 **Set-CsDeviceUpdateConfiguration** Cmdlet 來修改。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</a>。</td>
</tr>
</tbody>
</table>


以下範例顯示您可以使用 **Set-CsDeviceUpdateConfiguration** 修改設定的幾種方式。

## 修改記錄檔大小上限與記錄清除間隔

  - 下列命令會修改套用至 Redmond 網站的裝置更新記錄檔設定。在此範例中，記錄檔大小上限設為 204800 位元組，而記錄清除間隔設為 14 天。
    
        Set-CsDeviceUpdateConfiguration -Identity "site:Redmond" -MaxLogFileSize 204800 -LogCleanUpInterval 14.00:00:00

## 修改記錄清除時間

  - 此命令會將 Redmond 網站的記錄清除時間設為 3:00 AM。
    
        Set-CsDeviceUpdateConfiguration -Identity "site:Redmond" -LogCleanupTimeOfDay 03:00

如需詳細資訊，請參閱＜[Set-CsDeviceUpdateConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsDeviceUpdateConfiguration)＞ Cmdlet 的說明主題。

