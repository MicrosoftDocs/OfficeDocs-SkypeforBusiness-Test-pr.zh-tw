---
title: Test-CsExStorageConnectivity
TOCTitle: Test-CsExStorageConnectivity
ms:assetid: 20fda110-5e09-4453-bb7b-a062abaab87f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204740(v=OCS.15)
ms:contentKeyID: 49290322
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsExStorageConnectivity

 

_**上次修改主題的時間：** 2015-03-09_

驗證 Lync Server 儲存體服務是否在前端伺服器上運作。作法是在指定的 Exchange 信箱中建立測試電子郵件訊息，然後選擇性地刪除文字結尾的訊息。**Test-CsExStorageConnectivity** 也會確認 Exchange 封存如預期般運作。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsExStorageConnectivity -SipUri <String> [-Binding <String>] [-DeleteItem <SwitchParameter>] [-Folder <ConversationHistory | Inbox | Dumpster>] [-Force <SwitchParameter>] [-HostNameStorageService <String>] [-UseCache <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會測試 Lync Server 存放裝置服務是否能夠連接至 sip:kenmyer@litwareinc.com 使用者的 Exchange 信箱。在此範例中，NetNamedPipe 用作為 WCF 繫結。

    Test-CsExStorageConnectivity -SipUri "sip:kenmyer@litwareinc.com" -Binding "NetNamedPipe"

## 範例 2

範例 2 會驗證 Lync Server 存放服務是否可以連線到 Exchange 2013 的封存存放區 (請注意，若指定的使用者無法執行 Exchange 封存功能，此命令將會失敗)。此範例會連線到「暫放」資料夾 (也就是存放刪除項目的「可復原的項目」資料夾，使用者看不到此資料夾)。

    Test-CsExStorageConnectivity -SipUri "sip:kenmyer@litwareinc.com" -Binding "NetNamedPipe" -Folder Dumpster

## 詳細描述

**Test-CsExStorageConnectivity** Cmdlet 可用於驗證 Lync Server 2013 與 Exchange 2013 之間的伺服器對伺服器驗證是否可以運作。為驗證伺服器對伺服器的驗證，此 Cmdlet 會登入 Exchange 2013，將項目寫入指定信箱的「交談記錄」資料夾，然後刪除該項目。

**Test-CsExStorageConnectivity** Cmdlet 也可用於確認是否可以連線到 Exchange 2013 的封存存放區。

如果在執行此 Cmdlet 時收到「拒絕存取」訊息，通常表示您並非本機群組 RTC Local User Administrators 的成員。您可加入該群組或 Active Directory 群組 RTCUniversalUserAdmins (此為 RTC Local User Administrators 的成員) 以取得執行 **Test-CsExStorageConnectivity** Cmdlet 之所需的權限。

若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsExStorageConnectivity"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Test-CsExStorageConnectivity** Cmdlet 所執行的功能。

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>SipUri</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>應建立測試項目之 Exchange 2013 信箱的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>Binding</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>Windows Communication Foundation (WCF) 繫結。WCF 繫結可判斷讓用戶端與服務彼此通訊所需的傳輸、編碼及通訊協定詳細資料。有效值為：</p>
<p>* NetNamedPipe</p>
<p>* NetTCP</p></td>
</tr>
<tr class="odd">
<td><p><em>DeleteItem</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，將會從文字最後的 Exchange 2013 信箱中刪除測試項目。</p></td>
</tr>
<tr class="even">
<td><p><em>Folder</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Lyss.Cmdlets.ExchFolder</p></td>
<td><p>指定 Cmdlet 所要連線的 Exchange 2013封存資料夾。</p>
<p>* ConversationHistory</p>
<p>* Inbox</p>
<p>* Dumpster</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>HostNameStorageService</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>執行 Lync Server 存放裝置服務之伺服器的完整網域名稱 (FQDN)。如果 Binding 設為 NetTCP，則此為必要參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseCache</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有設定，會指示 Cmdlet 在連線到 Exchange 時使用快取的自動探索結果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。Test-CsExStorageConnectivity Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsExStorageConnectivity** Cmdlet 會傳回 Microsoft.Rtc.Management.ResourceData 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsExStorageNotification](test-csexstoragenotification.md)

