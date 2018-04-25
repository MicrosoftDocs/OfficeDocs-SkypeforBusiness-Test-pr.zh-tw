---
title: Lync Server 2013 中的 Web 會議概觀
TOCTitle: Lync Server 2013 中的 Web 會議概觀
ms:assetid: 40616dc4-f705-4890-85bf-79f76a033a9b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425913(v=OCS.15)
ms:contentKeyID: 49290709
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Web 會議概觀

 

_**上次修改主題的時間：** 2012-09-30_

透過 Web 會議，使用者可以在會議期間共用文件 (例如 PowerPoint 簡報) 並以文件進行共同作業。此外，使用者也能與其他人即時共用自己整個或部分桌面，看起來就像所有會議參與者都聚集在同一張會議桌前。

## 白板和註釋

白板是空白的畫布，可以藉由文字、手寫、繪圖和影像來進行共同作業。在白板上所做的註釋，所有會議參與者都看得到。白板功能可讓會議參與者討論想法、腦力激盪、做註記等，而提升共同作業的效能。

## 投票功能

投票功能可讓簡報者快速確認參與者的偏好，進而提高共同作業的效能。在線上會議與交談期間，簡報者可使用投票功能收集參與者的匿名意見。所有簡報者皆可檢視結果，並可選擇隱藏結果或對所有出席者顯示結果。

## 應用程式共用和桌面共用

您可以在會議期間共用您整個桌面、個別應用程式，或者多重監視器環境下的個別監視器。除了單純檢視內容之外，其他會議參與者也可要求控制您的螢幕，並且在取得許可的情況下，與內容互動 (包括捲動及編輯)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>檢視會議的參與者也可取得控制，並在會議期間開始共用內容</td>
</tr>
</tbody>
</table>


## PowerPoint 共用

在 Lync 2010 中，檢視 PowerPoint 簡報的方式有兩種。對於執行 Lync 2010 的使用者，PowerPoint 簡報會使用 PowerPoint 97-2003 格式來顯示，並且以 PowerPoint Viewer 內嵌複本進行檢視。對於執行 Lync Web App 的使用者，PowerPoint 簡報會轉換為動態 HTML 檔案，然後使用那些自訂 DHTML 檔案及 Silverlight 的組合進行檢視。雖然一般而言效果不錯，此方法確實有些限制：

  - 內嵌式 PowerPoint Viewer (可提供最佳檢視體驗) 僅可用於 Windows 平台。

  - 許多行動裝置 (包括一些較熱門的行動電話) 不支援 Silverlight。

  - PowerPoint Viewer 及 DHTML/Silverlight 方法不支援 PowerPoint. 較新版本中的所有功能 (例如投影片切換及內嵌影片)。

為了解決這些問題，並且改善使用者展現或檢視 PowerPoint 簡報的全面體驗，Lync Server 2013 採用 Office Web Apps 及 Office Web Apps Server 來處理 PowerPoint 簡報。此新方法的主要優勢如下：

  - 更高的顯示解析度，更佳的 PowerPoint 功能支援，例如動畫、投影片切換及內嵌影片。

  - 更多行動裝置可存取這些簡報。這是因為 Lync Server 2013 使用標準 DHTML 和 JavaScript 來廣播 PowerPoint 簡報，而不使用自訂 DHTML 及 Silverlight。

  - 擁有適當權限的使用者可以不影響簡報本身，自行捲動 PowerPoint 簡報。例如，當 Ken Myer 在進行投影片放映時，Pilar Ackerman 可以檢視任何想看的投影片，而不會影響 Ken 的簡報。

