---
title: 設定自訂顯示狀態
TOCTitle: 設定自訂顯示狀態
ms:assetid: e17364a8-8b93-45fc-a614-c80e45435d42
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398997(v=OCS.15)
ms:contentKeyID: 52056243
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定自訂顯示狀態

 

_**上次修改主題的時間：** 2013-01-10_

若要在 Lync 2013 中定義自訂目前狀態，請建立 XML 自訂目前狀態設定檔，然後使用 Lync Server 管理命令介面 Cmdlet **New-CSClientPolicy** 或 **Set-CSClientPolicy** 搭配參數 CustomStateURL 來指定其位置。

設定檔包含下列屬性：

  - 自訂目前狀態可以使用「線上」、「忙碌」和「請勿打擾」目前狀態指示器來設定。

  - 可用性屬性會判斷哪個目前狀態指示器與自訂狀態的狀態文字相關聯。在本主題稍後的範例中，「在家工作」狀態文字會顯示在綠色 (線上) 目前狀態指示器的右側。

  - 狀態文字的長度上限為 64 個字元。

  - 最多可以新增四個自訂目前狀態。

  - CustomStateURL 參數可指定設定檔的位置。在 Lync 2013 中會預設為啟用 SIP 高安全性模式，因此，您必須在啟用 HTTPS 的 Web 伺服器上儲存自訂目前狀態設定檔，否則 Lync 2013 用戶端會無法連線至自訂目前狀態設定檔。例如，有效的位址可能為 `https://lspool.corp.contoso.com/ClientConfigFolder/CustomPresence.xml`。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然其不適合在生產環境中，您可以使用 EnableSIPHighSecurityMode 登錄設定停用用戶端上的 SIP 高安全性模式來測試位於非 HTTPS 檔案共用的設定檔。接著您可以使用 CustomStateURL 登錄設定為設定檔指定一個非 HTTPS 的位置。請注意，Lync 2013 可接受 Lync 2010 登錄設定，但是登錄區現已更新。可以下列方式建立登錄設定：
<ul>
<li><p>HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Office\15.0\Lync\EnableSIPHighSecurityMode</p>
<p>類型：DWORD</p>
<p>數值資料：0</p></li>
<li><p>HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Office\15.0\Lync\CustomStateURL</p>
<p>類型：String (REG_SZ)</p>
<p>數值資料 (範例)：file://\\lspool.corp.contoso.com\LSFileShare\ClientConfigFolder\Presence.xml or file:///c:/LSFileShare/ClientConfigFolder/Group_1_Pres.xml</p></li>
</ul></td>
</tr>
</tbody>
</table>


在 XML 設定檔中指定一或多個地區設定識別碼 (LCID) 架構，以當地語系化您的自訂目前狀態。本主題稍後的範例顯示當地語系化為「英文 - 美國」(1033)、「挪威文 - 巴克摩」(1044)、「法文 - 法國」(1036) 和「土耳其文」(1055)。如需 LCID 的清單，請參閱＜由 Microsoft 指派的地區設定識別碼＞，網址為 <http://go.microsoft.com/fwlink/?linkid=157331>。

## 將自訂目前狀態新增至 Lync 2013

1.  建立使用下列範例格式的 XML 設定檔：
    
        <?xml version="1.0"?>
        <customStates xmlns="http://schemas.microsoft.com/09/2009/communicator/customStates">
          <customState ID="1" availability="online">
            <activity LCID="1033">Working from Home</activity>
            <activity LCID="1044">activity 2 for 1044</activity>
            <activity LCID="1055">activity 3 for 1055</activity>
          </customState>
          <customState ID="2" availability="busy">
            <activity LCID="1033">In a Live Meeting</activity>
            <activity LCID="1036">Equivalent French String for - In a Live Meeting </activity>
          </customState>
          <customState ID="3" availability="busy">
            <activity LCID="1033">Meeting with Customer</activity>
            <activity LCID="1055">meeting with client</activity>
            <activity LCID="1036">Equivalent French String for - Meeting with Customer</activity>
          </customState>
          <customState ID="4" availability="do-not-disturb">
            <activity LCID="1033">Interviewing</activity>
          </customState>
        </customStates>

2.  將 XML 設定檔儲存至啟用 HTTPS 的 Web 伺服器。在此範例中，檔案會命名為 Presence.xml 並儲存至 https://lspool.corp.contoso.com/ClientConfigFolder/CustomPresence.xml。

3.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

4.  在 Lync Server 管理命令介面中，使用類似以下所示的命令，定義您的 XML 設定檔位置：
    
        New-CsClientPolicy -Identity ContosoCustomStates 
        -CustomStateURL "https://lspool.corp.contoso.com/ClientConfigFolder/CustomPresence.xml"

5.  使用 **Grant-CSClientPolicy** Cmdlet，將此新原則指派給使用者。

如需詳細資訊，請參閱 Lync Server 管理命令介面文件中的 [New-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientPolicy) 和 [Grant-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsClientPolicy)。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>根據預設，Lync Server 2013 會每三個小時更新用戶端原則和設定。</p></li>
<li><p>如果您要繼續從舊版本使用 CustomStateURL 等「群組原則」設定，Lync 2013 會辨識設定是否位於新原則的登錄區 (HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Office\15.0\Lync)。但是，會以伺服器用戶端原則為優先。</p></li>
</ul></td>
</tr>
</tbody>
</table>

