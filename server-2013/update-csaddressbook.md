---
title: Update-CsAddressBook
TOCTitle: Update-CsAddressBook
ms:assetid: 109c5fe7-0154-4161-b19f-01bab024bb3d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398194(v=OCS.15)
ms:contentKeyID: 49290121
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsAddressBook

 

_**上次修改主題的時間：** 2015-03-09_

強制指定的 Address Book Server 與使用者資料庫同步其內容。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Update-CsAddressBook [-Force <SwitchParameter>] [-Fqdn <Fqdn>]

## 範例

## 範例 1

範例 1 會先呼叫不含任何參數的 **Update-CsAddressBook** Cmdlet 以同步組織中所有的 Address Book Server。

    Update-CsAddressBook

## 範例 2

在範例 2 中，只會同步單一 Address Book Server：伺服器與 FQDN atl-abs-001.litwareinc.com。

    Update-CsAddressBook -Fqdn atl-abs-001.litwareinc.com

## 詳細描述

Address Book Server 是 Active Directory 與 Lync Server 之間的媒介。Address Book Server 可確保儲存在 Lync Server 的使用者資訊會與儲存在 Active Directory 的使用者資訊同步。作法是定期將通訊錄檔案與儲存在使用者資料庫中的資訊同步。根據預設，系統每五分鐘會進行一次同步化 (但是，您可以使用 **Set-CsAddressBookConfiguration** Cmdlet 修改時間間隔)。

如果您等不及進行同步，或因某種原因而未進行同步，您可以使用 **Update-CsAddressBook** Cmdlet 強制 Address Book Server 立即與儲存在 使用者資料庫 中的使用者資訊同步。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Update-CsAddressBook** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Update-CsAddressBook"}

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
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏當執行 Cmdlet 時可能發生的任何確認提示或非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Fqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您指定欲更新的個別通訊錄。如果未包含此參數，則全部的 Address Book Server 皆會與 使用者資料庫 同步。個別的 Address Book Server 可藉由完整網域名稱 (FQDN) 來識別，例如 atl-abs-001.litwareinc.com。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Update-CsAddressBook** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。反之， **Update-CsAddressBook** Cmdlet 會更新現有的 Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)  
[Test-CsAddressBookService](test-csaddressbookservice.md)  
[Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

