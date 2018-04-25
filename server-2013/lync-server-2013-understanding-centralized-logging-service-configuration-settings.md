---
title: 瞭解集中式記錄服務組態設定
TOCTitle: 瞭解集中式記錄服務組態設定
ms:assetid: 3c34e600-0b91-43dc-b4cc-90b6a70ee12e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688029(v=OCS.15)
ms:contentKeyID: 49890026
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 瞭解集中式記錄服務組態設定

 

_**上次修改主題的時間：** 2015-03-09_

集中記錄服務的設定是定義記錄服務要收集什麼、如何收集、收集的來源以及記錄設定為何。可以將設定定義為全域 (亦即整個部署) 或網站 (亦即部署中指定的網站)。任何您定義的記錄都會依據您在進行開始、停止、清除及搜尋記錄命令時所使用的身分，而使用適當的設定。

## 顯示目前的集中記錄服務組態

啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

在命令列提示輸入下列命令：

    Get-CsClsConfiguration

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以定義 <code>-Identity</code> 與範圍來縮小或擴大組態設定的範圍，例如 &quot;Site:Redmond&quot; 只傳回網站 Redmond 的 CsClsConfiguration。如果要組態指定部分的詳細資料，可以將輸出輸送到另一個 Windows PowerShell Cmdlet。例如，要取得網站 &quot;Redmond&quot; 組態中定義之案例的詳細資訊，請輸入：<code>Get-CsClsConfiguration -Identity &quot;site:Redmond&quot; | Select-Object -ExpandPropery Scenarios</code></td>
</tr>
</tbody>
</table>


![Get-CsClsConfiguration 輸出範例。](images/JJ688029.23f98ddc-fc48-499a-b6c5-752611f2a0b0(OCS.15).jpg "Get-CsClsConfiguration 輸出範例。")

Cmdlet 的結果會顯示集中記錄服務目前的組態。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>組態設定</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Identity</strong></p></td>
<td><p>識別此組態的範圍及名稱。只有一個全域組態，而每個網站有一個組態。</p></td>
</tr>
<tr class="even">
<td><p><strong>Scenarios</strong></p></td>
<td><p>列出針對此組態定義的所有案例。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SearchTerms</strong></p></td>
<td><p>定義組態的搜尋字詞。Office 365，非內部部署。</p></td>
</tr>
<tr class="even">
<td><p><strong>SecurityGroups</strong></p></td>
<td><p>定義安全性群組，根據其所在的網站，控制誰 (亦即安全性群組的成員) 可以看到電腦。此處網站指的是定義於拓撲產生器的網站。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Regions</strong></p></td>
<td><p>定義地區，用於將 SecurityGroups 集合至地區，例如 EMEA。</p></td>
</tr>
<tr class="even">
<td><p><strong>EtlFileFolder</strong></p></td>
<td><p>定義將記錄檔寫入電腦所在位置的路徑。CLSAgent 寫入記錄檔並在網路服務環境下執行。在此情況下，%TEMP% 會展開為 %WINDIR%\ServiceProfiles\NetworkService\AppData\Local</p></td>
</tr>
<tr class="odd">
<td><p><strong>EtlFileRolloverSizeMB</strong></p></td>
<td><p>此參數指示在建立新的事件追蹤記錄 (.etl) 檔之前，記錄檔的大小上限。達到定義的大小時，即使還未達到 EtlFileRolloverMinutes 中設定的時間上限，還是會建立新的記錄檔。</p></td>
</tr>
<tr class="even">
<td><p><strong>EtlFileRolloverMinutes</strong></p></td>
<td><p>定義在建立新的 .etl 檔之前，記錄檔可以存在的時間上限 (分)。計時器逾期時，即使還未達到 EtlFileRolloverSizeMB 中設定的大小上限，還是會建立新的記錄檔。</p></td>
</tr>
<tr class="odd">
<td><p><strong>TmfFileSearchPath</strong></p></td>
<td><p>搜尋追蹤訊息格式檔的位置。追蹤訊息格式檔是用於將二進位檔案轉換為人類看得懂的格式。</p></td>
</tr>
<tr class="even">
<td><p><strong>CacheFileLocalFolders</strong></p></td>
<td><p>定義將快取檔案寫入電腦所在位置的路徑。CLSAgent 寫入快取檔案並在網路服務環境下執行。在此情況下，%TEMP% 會展開為 %WINDIR%\ServiceProfiles\NetworkService\AppData\Local。依據預設，快取檔案及記錄檔會寫入相同的目錄。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CacheFileNetworkFolder</strong></p></td>
<td><p>您可以定義通用命名慣例 (UNC) 路徑，以在記錄作業時接收快取檔案。</p></td>
</tr>
<tr class="even">
<td><p><strong>CacheFileLocalRetentionPeriod</strong></p></td>
<td><p>定義快取檔案保留的時間上限 (天)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CacheFileMaxDiskUsage</strong></p></td>
<td><p>定義快取檔案可使用的磁碟空間百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>ComponentThrottleLimit</strong></p></td>
<td><p>定義在觸發自動節流限制器之前，元件每秒可以產生的追蹤上限。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ComponentThrottleSample</strong></p></td>
<td><p>60 秒內可超過 ComponentThrottleLimit 的次數。</p></td>
</tr>
<tr class="even">
<td><p><strong>MinimumClsAgentServiceVersion</strong></p></td>
<td><p>允許執行的 CLSAgent 最小版本。此元素是針對 Office 365。</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[集中式記錄服務概觀](lync-server-2013-overview-of-the-centralized-logging-service.md)  

#### 其他資源

[Set-CsClsConfiguration](set-csclsconfiguration.md)  
[Remove-CsClsConfiguration](remove-csclsconfiguration.md)  
[New-CsClsConfiguration](new-csclsconfiguration.md)  
[Get-CsClsConfiguration](get-csclsconfiguration.md)

