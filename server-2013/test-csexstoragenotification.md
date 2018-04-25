---
title: Test-CsExStorageNotification
TOCTitle: Test-CsExStorageNotification
ms:assetid: d8fe3b22-7a76-4d70-9bc1-b54b37f68449
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205331(v=OCS.15)
ms:contentKeyID: 49292499
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsExStorageNotification

 

_**上次修改主題的時間：** 2015-03-09_

確認前端伺服器上執行的 Lync Server 存放服務可以訂閱 Microsoft Exchange Server 2013信箱通知服務。作法是使用此 Cmdlet 訂閱該服務、建立項目、確認收到新項目的通知，然後視情況從服務刪除取消訂閱的項目。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsExStorageNotification -SipUri <String> [-Binding <String>] [-DeleteItem <SwitchParameter>] [-Force <SwitchParameter>] [-HostNameStorageService <String>]

## 範例

## 範例 1

範例 1 所示的命令會針對使用者 sip:kenmyer@litwareinc.com 測試 Lync Server Storage Service 是否可以連線至 Exchange Server 信箱通知服務。此範例會將 NetNamedPipe 用為 WCF 繫結。

    Test-CsExStorageNotification -SipUri "sip:kenmyer@litwareinc.com" -Binding "NetNamedPipe"

## 詳細描述

**Test-CsExStorageNotification** Cmdlet 可用於確認 Microsoft Exchange Server 2013 通知服務能否在使用者的連絡人清單有所更新時隨時通知 Lync Server 2013。只有使用統一連絡人存放區的使用者才可使用此 Cmdlet。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsExStorageNotification"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Test-CsExStorageNotification** Cmdlet 所執行的功能。

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
<td><p>應建立測試項目之 Exchange Server 信箱的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>Binding</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>Windows Communication Foundation (WCF) 繫結。WCF 繫結決定用戶端和服務彼此通訊所需的傳輸、編碼及通訊協定詳細資料。有效值為：</p>
<p>* NetNamedPipe</p>
<p>* NetTCP</p></td>
</tr>
<tr class="odd">
<td><p><em>DeleteItem</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會從 Exchange 信箱刪除文字結尾的測試項目。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>HostNameStorageService</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>執行 Lync Server Storage Service 之伺服器的完整網域名稱。如果 Binding 設為 NetTCP，則需要此參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsExStorageNotification** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsExStorageNotification** Cmdlet 會傳回 Microsoft.Rtc.Management.ResourceData 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsExStorageConnectivity](test-csexstorageconnectivity.md)

