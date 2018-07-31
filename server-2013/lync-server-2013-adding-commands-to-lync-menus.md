---
title: 將命令新增到 Lync 功能表
TOCTitle: 將命令新增到 Lync 功能表
ms:assetid: a8443bc2-e234-4022-870a-00700f38b1ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412788(v=OCS.15)
ms:contentKeyID: 52056204
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將命令新增到 Lync 功能表

 

_**上次修改主題的時間：** 2015-03-09_

您可以將自訂命令新增至 Lync 2013 功能表，並將目前使用者和所選連絡人的 SIP 統一資源識別元 (URI)，傳遞至自訂命令啟動的應用程式。

您新增的自訂命令可能會出現在下列其中一個或多個功能表上：

  - \[工具\] 功能表，位在 Lync 主視窗中的功能表列上

  - \[連絡人\] 清單中連絡人的捷徑功能表

  - \[交談\] 視窗中的 \[更多選項\] 功能表

  - \[交談\] 視窗參與者清單中所列人員的捷徑功能表

  - 連絡人卡片中的選項功能表

您可以為兩種類型的應用程式 (執行下列任一項的應用程式) 定義自訂命令：

  - 只套用到目前使用者且在本機電腦上啟動。

  - 包含其他使用者 (例如線上共同作業程式)，且必須在每個使用者的電腦上啟動。

自訂命令可採取下列方式來叫用：

  - 選取一或多個使用者，然後選擇自訂命令。

  - 啟動雙方或多方交談，然後選擇自訂命令。

## 若要新增自訂命令

使用下表中的登錄設定，將命令新增至功能表。這些項目會放在登錄中的下列位置：

HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Office\\15.0\\Lync\\CustomCommands

### 自訂命令登錄項目

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>類型</th>
<th>資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Name</p></td>
<td><p>REG_SZ</p></td>
<td><p>顯示在功能表上的應用程式名稱。</p></td>
</tr>
<tr class="even">
<td><p>ApplicationType</p></td>
<td><p>DWORD</p></td>
<td><p>0 = 可執行檔 (預設)</p>
<div class="alert">

> [!NOTE]  
> 需要 ApplicationInstallPath。


</div>
<p>1 = 通訊協定</p></td>
</tr>
<tr class="odd">
<td><p>ApplicationInstallPath</p></td>
<td><p>REG_SZ</p></td>
<td><p>可執行檔的完整路徑。</p>
<div class="alert">

> [!NOTE]  
> 如果 ApplicationType 為 0 (可執行檔)，則必須指定。


</div></td>
</tr>
<tr class="even">
<td><p>Path</p></td>
<td><p>REG_SZ</p></td>
<td><p>要與任何參數一起啟動的完整路徑，包括預設參數 <em>%user-id%</em> 和 <em>%contact-id%</em>。</p></td>
</tr>
<tr class="odd">
<td><p>SessionType</p></td>
<td><p>DWORD</p></td>
<td><p>0 = 本機工作階段。在本機電腦上啟動應用程式。</p>
<p>1 = 雙方工作階段 (預設)。Lync 2013 在本機啟動應用程式，然後將桌面通知傳送給其他使用者。其他使用者按一下通知，以在其電腦上啟動應用程式。</p>
<p>2 = 多方工作階段。Lync 2013 在本機啟動應用程式，然後將桌面通知傳送給其他使用者。其他使用者按一下通知，以在其電腦上啟動指定的應用程式。</p></td>
</tr>
<tr class="even">
<td><p>ExtensibleMenu</p></td>
<td><p>REG_SZ</p></td>
<td><p>隨即出現這個命令的功能表清單 (以分號分隔)。可能的值有：</p>
<p>MainWindowActions</p>
<p>MainWindowRightClick</p>
<p>ConversationWindowActions</p>
<p>ConversationWindowRightClick</p>
<p>ContactCardMenu</p>
<p>如果沒有定義 ExtensibleMenu ，會使用 MainWindowRightClick 和 ConversationWindowActions 的預設值。</p></td>
</tr>
</tbody>
</table>


例如，下列登錄編輯程式 (.REG) 檔案中，會顯示將 Contoso Sales Contact Manager 功能表項目新增至 \[交談\] 視窗中 \[動作\] 功能表的結果：

    Windows Registry Editor Version 5.00
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\CustomCommands\{1F9F07C6-7E0B-462B-AAD7-98C6DBEA8F69}]
    "Name"="Contoso Sales Contact Manager"
    "HelpMessage"="The Contoso Sales Contact Manager is not installed. Contact the Help Desk for more information."
    "ApplicationType"=dword:00000000
    "ApplicationInstallPath"="C:\\cscm.exe"
    "Path"="C:\\cscm.exe %user-id% %contact-id%"
    "SessionType"=dword:00000001
    "ExtensibleMenu"="ConversationWindowActions;MainWindowRightClick"

## 若要存取自訂命令

若要在新增自訂命令後存取它，請根據您定義的 ExtensibleMenu 值，執行下列其中一項作業：

  - **MainWindowActions**   在 Lync 主視窗中，按一下 \[工具\]，然後按一下您的自訂命令。

  - **MainWindowRightClick**   在 Lync 主視窗中，以滑鼠右鍵按一下連絡人，然後按一下您的自訂命令。

  - **ConversationWindowActions**   在 \[交談\] 視窗中，按一下 \[更多選項\] 圖示，然後按一下您的自訂命令。

  - **ConversationWindowRightClick**   在 \[交談\] 視窗中，以滑鼠右鍵按一下連絡人名稱，然後按一下您的自訂命令。

  - **ContactCardMenu**   在人員的連絡人卡片中，按一下選項圖示，然後按一下自訂命令。

