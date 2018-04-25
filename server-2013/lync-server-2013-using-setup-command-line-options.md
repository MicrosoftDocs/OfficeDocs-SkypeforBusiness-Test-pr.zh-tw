---
title: 使用安裝程式命令列選項
TOCTitle: 使用安裝程式命令列選項
ms:assetid: 99878c3c-ff31-48e2-8424-580d7b07a7bf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205129(v=OCS.15)
ms:contentKeyID: 49291778
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用安裝程式命令列選項

 

_**上次修改主題的時間：** 2015-03-09_

在 Office 安裝期間僅有很少的作業會用到 Setup.exe 命令列。您通常會使用 Office 自訂工具和 Config.xml 檔進行產品安裝和功能自訂，而不是使用 Setup 命令列選項。

Office Setup.exe 命令列可辨識下表所述的命令列選項。

### Office Setup 命令列選項

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Setup 命令列選項</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>/admin</p></td>
<td><p>執行 Office 自訂工具以建立安裝程式自訂檔案 (.msp 檔)。</p></td>
</tr>
<tr class="even">
<td><p>/adminfile [路徑]</p></td>
<td><p>將指定的安裝程式自訂檔案套用至安裝。您可以指定特定自訂檔案 (.msp 檔) 的路徑，或是指定儲存了自訂檔案的資料夾路徑。</p></td>
</tr>
<tr class="odd">
<td><p>/config [路徑]</p></td>
<td><p>指定 Setup 在安裝期間使用的 Config.xml 檔。使用 /config 選項指定您已為 Lync 2013 安裝自訂的 Config.xml 檔，例如：<code>/config \\server\share\Lync15\Lync.WW\Config.xml</code></p></td>
</tr>
<tr class="even">
<td><p>/modify Lync</p></td>
<td><p>與修改過的 Config.xml 檔搭配使用，以在維護模式中執行 Setup，並且對現有的 Office 安裝進行變更。例如，您可以使用 /modify 選項新增或移除 Lync 功能。</p></td>
</tr>
<tr class="odd">
<td><p>/repair Lync</p></td>
<td><p>從使用者的電腦執行 Setup 以修復 Lync。</p></td>
</tr>
<tr class="even">
<td><p>/uninstall Lync</p></td>
<td><p>從使用者的電腦執行 Setup 以移除 Lync。</p></td>
</tr>
</tbody>
</table>


如需關於使用 Setup 命令列選項的詳細資訊，請參閱 [http://go.microsoft.com/fwlink/?linkid=267515\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=267515%26clcid=0x404)。

