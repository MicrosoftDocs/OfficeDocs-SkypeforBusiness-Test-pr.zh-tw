---
title: 使用 Config.xml 執行安裝工作
TOCTitle: 使用 Config.xml 執行安裝工作
ms:assetid: 0813184a-ab40-417c-b3a3-c2090766b831
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204651(v=OCS.15)
ms:contentKeyID: 49290002
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 Config.xml 執行安裝工作

 

_**上次修改主題的時間：** 2015-03-09_

雖然 Office 自訂工具 (OCT) 是自訂安裝的主要工具，但是系統管理員可以使用 Config.xml 檔案來指定 OCT 中所沒有的其他安裝指示。下列自訂只能使用 Config.xml 檔案來進行：

  - 指定網路安裝點的路徑。

  - 選取所要安裝的產品。

  - 設定安裝程式自訂檔案和軟體更新的記錄及位置。

  - 指定安裝選項，例如使用者名稱。

  - 將本機安裝來源 (LIS) 複製到使用者的電腦，而不安裝 Office。

  - 在安裝中新增或移除語言。

建議您使用 Config.xml 檔案來設定 Lync 2013 無訊息安裝。

依預設，儲存在核心產品資料夾 (例如 \\*產品*.WW) 中的 Config.xml 檔案，會引導安裝程式安裝該產品。例如，下列資料夾中的 Config.xml 檔案會安裝 Lync 2013：

  - \\\\server\\share\\Lync15\\Lync.WW \\Config.xml

下表列出最常用於 Lync 2013 安裝的 Config.xml 元素。

### Config.xml 元素

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>設定</p></td>
<td><p>最上層元素 (必要)。包含 Product 屬性，例如：Product=Lync</p></td>
</tr>
<tr class="even">
<td><p>OptionState</p></td>
<td><p>指定在安裝期間如何處理特定的產品功能。請使用下列屬性，以防止安裝 Business Connectivity Services，因為其中包含會干擾 Outlook 2010 的共用元件：</p>
<ul>
<li><p>Id=&quot;LOBiMain&quot;</p></li>
<li><p>State=&quot;Absent&quot;</p></li>
<li><p>Children=&quot;Force&quot;</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>顯示</p>
<p></p></td>
<td><p>安裝程式向使用者顯示的 UI 層級。一般屬性包括：</p>
<ul>
<li><p>CompletionNotice=&quot;Yes&quot; | &quot;No&quot;(預設值)</p></li>
<li><p>AcceptEula=&quot;Yes&quot; | &quot;No&quot;(預設值)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>記錄</p></td>
<td><p>安裝程式執行之記錄類型的選項。一般屬性包括：</p>
<ul>
<li><p>Type =&quot;Off&quot; | &quot;Standard&quot;(預設值) | &quot;Verbose&quot;</p></li>
<li><p>Template=”<em>檔案名稱</em>.txt” (記錄檔名稱)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>設定</p></td>
<td><p>指定 Windows Installer 內容的值。一般屬性包括：</p>
<ul>
<li><p>設定 Id=&quot;<em>名稱</em>&quot; (Windows Installer 內容的名稱)</p></li>
<li><p>Value=&quot;<em>值</em>&quot; (指定給內容的值)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>發佈點</p></td>
<td><p>要執行安裝之網路安裝點的完整路徑。包括 Location 屬性：</p>
<ul>
<li><p>Location=”<em>路徑</em>”</p></li>
</ul></td>
</tr>
</tbody>
</table>


下列範例顯示用於一般 Lync 2013 無訊息安裝的 Config.xml 檔案。

    <Configuration Product="Lync">
      <OptionState Id="LOBiMain" State="Absent" Children="Force" />
      <Display Level="None" CompletionNotice="No" AcceptEula="Yes" />
      <Logging Type="verbose" Path="%temp%" Template="LyncSetupVerbose(*).log" />
      <Setting Id="SETUP_REBOOT" Value="Never" />
      <DistributionPoint Location="\\server\share\Lync15" />
    </Configuration>

如需使用 Config.xml 檔案來執行 Office 安裝及維護工作的詳細資訊，請參閱 [http://go.microsoft.com/fwlink/?linkid=267514\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=267514%26clcid=0x404)。

## 自訂 Config.xml 檔案

1.  使用文字編輯器工具來開啟 Config.xml 檔案，例如 \[記事本\]。

2.  找到包含您要變更之元素的那幾行。

3.  以您要使用的無訊息選項來修改元素項目。請務必移除註解分隔符號 "\<\!--" 和 "--\>"。例如，使用下列語法：
    
        < DistributionPoint Location="\\server\share\Lync15" />

4.  儲存 Config.xml 檔案。

