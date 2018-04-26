---
title: 整合協力廠商共同作業應用程式與 Lync
TOCTitle: 整合協力廠商共同作業應用程式與 Lync
ms:assetid: 00b9312c-b0c8-4f79-8b76-05b2d820e197
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398068(v=OCS.15)
ms:contentKeyID: 52056040
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 整合協力廠商共同作業應用程式與 Lync

 

_**上次修改主題的時間：** 2015-03-09_

您可將 Lync 2013 與任何協力廠商線上共同作業應用程式進行整合，方法是將該應用程式的資訊新增至登錄。使用 Lync 2013 即可啟動裝載於內部伺服器、網際網路服務或以上兩者的資料會議工作階段。您可以從連絡人清單或從現有的立即訊息、語音或視訊工作階段，啟動共同作業或資料會議工作階段。Lync 2013 僅是啟動應用程式的工具而已。啟動線上共同作業工作階段之後，任何現有的 Lync 2013 交談仍會維持作用中。

下列章節說明 Lync 2013 如何與網際網路和伺服器的共同作業應用程式整合。

## 整合網際網路共同作業應用程式與 Lync 2013

基本上，與協力廠商共同作業應用程式整合相關的步驟如下：

1.  應用程式的相關資訊會新增到登錄中。

2.  召集人會登入 Lync 2013，然後選取資料共用與共同作業的連絡人。或者，召集人可能已經在交談中，並決定新增資料會議。

3.  Lync 2013 讀取登錄、啟動共同作業應用程式，然後傳送自訂 SIP 訊息 (appINVITE) 給選取的參與者。

4.  參與者會接受邀請，並在每個人的電腦上啟動共同作業應用程式。Lync 2013 使用登錄來決定要使用的共同作業應用程式，然後使用包含在 appINVITE 訊息中的參數啟動該應用程式。

下表說明整合網際網路共同作業應用程式與 Lync 2013 所需的登錄項目。這些項目位於登錄的下列位置中：

  - HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\Office\\15.0\\Lync\\SessionManager\\Apps\\Parameters

### 網際網路共同作業應用程式的登錄項目

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
<td><p>Lync 2013 功能表的應用程式名稱。</p></td>
</tr>
<tr class="even">
<td><p>SmallIcon</p></td>
<td><p>REG_SZ</p></td>
<td><p>16 像素 x 16 像素圖示 (BMP 或 PNG) 的路徑。</p></td>
</tr>
<tr class="odd">
<td><p>Path</p></td>
<td><p>REG_SZ</p></td>
<td><p>啟動線上共同作業應用程式的參與者路徑。</p></td>
</tr>
<tr class="even">
<td><p>OriginatorPath</p></td>
<td><p>REG_SZ</p></td>
<td><p>啟動線上共同作業應用程式的召集人路徑。這個路徑可以包含一或多個自訂參數，做為 Parameters 子機碼中定義的參數。例如：<code>https://meetserv.adatum.com/cc/%param1%/join?id=%param2%&amp;role=present&amp;pw=%param3%</code></p></td>
</tr>
<tr class="odd">
<td><p>SessionType</p></td>
<td><p>DWORD</p></td>
<td><p>0 = 本機工作階段。在本機電腦上啟動應用程式。</p>
<p>1 = 雙方工作階段 (預設)。Lync 2013 在本機啟動應用程式，然後將系統通知傳送給另一位使用者。另一位使用者按一下通知並在他們的電腦上啟動指定的應用程式。</p>
<p>2 = 多方工作階段。Lync 2013 在本機啟動應用程式，然後將系統通知傳送給其他使用者，提示他們在所屬電腦上啟動指定的應用程式。</p></td>
</tr>
<tr class="even">
<td><p>ExensibleMenu</p></td>
<td><p>REG_SZ</p></td>
<td><p>會出現這個命令的功能表清單 (以分號分隔)。可能的值有：</p>
<ul>
<li><p>MainWindowActions</p></li>
<li><p>MainWindowRightClick</p></li>
<li><p>ConversationWindowActions</p></li>
<li><p>ConversationWindowButton</p></li>
<li><p>ConversationWindowRightClick</p></li>
</ul>
<p>如果沒有定義 ExtensibleMenu ，會使用 MainWindowRightClick 和 ConversationWindowActions 的預設值。</p></td>
</tr>
</tbody>
</table>


下表說明參數的登錄項目。這些項目位於 HKEY\_CURRENT\_USER\\Software\\Microsoft\\Office\\15.0\\Lync\\SessionManager\\Apps\\Parameters。

### 網際網路共同作業應用程式的登錄項目

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
<td><p>Param1</p></td>
<td><p>REG_SZ</p></td>
<td><p>使用記號化的格式 (<code>%Parm1%</code>)，將使用者特定的值新增到 OriginatorPath 登錄機碼中。</p></td>
</tr>
<tr class="even">
<td><p>Param2</p></td>
<td><p>REG_SZ</p></td>
<td><p>請參閱 Param1。</p></td>
</tr>
<tr class="odd">
<td><p>Param3</p></td>
<td><p>REG_SZ</p></td>
<td><p>請參閱 Param1。</p></td>
</tr>
</tbody>
</table>


下列範例登錄設定會將 ADatum Collaboration Client 與 Lync 2013 整合：

    Windows Registry Editor Version 5.00
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\SessionManager]
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\SessionManager\Apps]
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\SessionManager\Apps\{C3F6E17A-855F-44a0-B90D-C0B92D38E5F1}]
    "Path"="https://meetingservice.adatum.com/cc/%param1%/meet/%param2%"
    "OriginatorPath"="https://meetserv.adatum.com/cc/%param1%/join?id=%param2%&role=present&pw=%param3%"
    "SessionType"=dword:00000002
    "ApplicationType"=dword:00000001
    "LiveServerIntegration"=dword:00000000
    "Name"="ADatum Online Collaboration Service"
    "Extensiblemenu"="MainWindowActions;MainWindowRightClick;ConversationWindowActions;ConversationWindowRightClick"
    
    [HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Lync\SessionManager]
    [HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Lync\SessionManager\Apps]
    [HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Lync\SessionManager\Apps\Parameters]
    [HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Lync\SessionManager\Apps\Parameters\{C3F6E17A-855F-44a0-B90D-C0B92D38E5F1}]
    "Param1"="meetserv"
    "Param2"="admin"
    "Param3"="abcdefg123"

## 整合伺服器共同作業應用程式與 Lync 2013

為了從 Lync 2013 內啟動伺服器共同作業應用程式，而新增命令的設定，類似上一節＜整合網際網路共同作業應用程式與 Lync 2013＞中說明的設定。不過不需要 OriginatorPath，而且某些值有所變更。登錄項目位於下列位置：

  - HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\Office\\15.0\\Lync\\SessionManager\\Apps\\Parameters

### 伺服器共同作業應用程式的登錄項目

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
<td><p>值 = 1。將應用程式類型設定成通訊協定。其他可能的值則在這個情況不適用。如果沒有出現，ApplicationType 會設定為 0 (可執行)。</p></td>
</tr>
<tr class="odd">
<td><p>Path</p></td>
<td><p>REG_SZ</p></td>
<td><p>用來啟動共同作業應用程式的通訊協定。若為 Live Meeting 2007，Path 的值會設定為 <code>meet:%conf-uri%</code>。</p></td>
</tr>
<tr class="even">
<td><p>SessionType</p></td>
<td><p>DWORD</p></td>
<td><p>0 = 本機工作階段。在本機電腦上啟動應用程式。</p>
<p>1 = 雙方工作階段 (預設)。Lync 2013 在本機啟動應用程式，然後將系統通知傳送給另一位使用者。另一位使用者按一下通知並在他們的電腦上啟動指定的應用程式。</p>
<p>2 = 多方工作階段。Lync 2013 在本機啟動應用程式，然後將系統通知傳送給其他使用者，提示他們在其電腦上啟動指定的應用程式。</p></td>
</tr>
<tr class="odd">
<td><p>MCUType</p></td>
<td><p>REG_SZ</p></td>
<td><p>DATA = 伺服器的類型。</p></td>
</tr>
<tr class="even">
<td><p>ExtensibleMenu</p></td>
<td><p>REG_SZ</p></td>
<td><p>隨即出現這個命令的功能表清單 (以分號分隔)。可能的值有：</p>
<ul>
<li><p>MainWindowActions</p></li>
<li><p>MainWindowRightClick</p></li>
<li><p>ConversationWindowActions</p></li>
<li><p>ConversationWindowButton</p></li>
<li><p>ConversationWindowRightClick</p></li>
</ul>
<p>如果沒有定義 ExtensibleMenu ，會使用 MainWindowRightClick 和 ConversationWindowActions 的預設值。</p></td>
</tr>
</tbody>
</table>


下列範例會新增從 Lync 2013 內啟動 ADatum Collaboration Client 的命令：

    Windows Registry Editor Version 5.00
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\SessionManager]
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\SessionManager\Apps]
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Lync\SessionManager\Apps\{27877e66-615c-4582-ab88-0cb2ca05d951}]
    "Path"="meet:%conf-uri%"
    "SessionType"=dword:00000002
    "LiveServerIntegration"=dword:00000001
    "ApplicationType"=dword:00000001
    "Name"="ADatum Collaboration Client"
    "MCUType"="Data"
    "Extensiblemenu"="MainWindowActions;MainWindowRightClick;ConversationWindowActions;ConversationWindowRightClick"

