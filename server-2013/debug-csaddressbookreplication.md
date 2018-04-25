---
title: Debug-CsAddressBookReplication
TOCTitle: Debug-CsAddressBookReplication
ms:assetid: c138f274-7a1f-4074-b6a2-548274af5199
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205232(v=OCS.15)
ms:contentKeyID: 49292212
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Debug-CsAddressBookReplication

 

_**上次修改主題的時間：** 2015-03-09_

驗證 Active Directory 與 Lync Server 2013 通訊錄服務之間的複寫狀態。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Debug-CsAddressBookReplication [-DomainController <String>] [-User <String>] [-VerifyReplication <SwitchParameter>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-PoolFqdn <Fqdn>] [-VerifyNormalization <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會驗證目前集區的通訊錄複寫。若要驗證指定集區的複寫，請加入 PoolFqdn 參數，再緊接著輸入要驗證之集區的完整網域名稱。

    Debug-CsAddressBookReplication

## 範例 2

範例 2 會在驗證目前集區的通訊錄複寫時加入 User 參數。加入 User 參數可傳回指定使用者的其他相關資訊。

    Debug-CsAddressBookReplication -User "sip:kenmyer@litwareinc.com"

## 範例 3

範例 3 會使用 VerifyReplication 參數變更指定的使用者帳戶，然後驗證此變更是否可以成功地複寫到通訊錄。

    Debug-CsAddressBookReplication -User "sip:kenmyer@litwareinc.com" -VerifyReplication 

## 範例 4

範例 4 所示的命令會使用 VerifyNormalization 參數傳回無法套用通訊錄正規化挸則之使用者帳戶的資訊。

    Debug-CsAddressBookReplication -VerifyNormalization

## 詳細描述

Address Book Server 是 Active Directory 網域服務 (AD DS) 與 Microsoft Lync Server 之間的中繼伺服器。Address Book Server 可確保 Lync Server 與 Active Directory 上所儲存的使用者資訊相同。作法是定期同步通訊錄檔案與使用者資料庫中所儲存的資訊。

**Debug-CsAddressBookReplication** Cmdlet 可讓系統管理員驗證 Active Directory 與 Lync Server 之間所要複寫的資料。全面測試 Active Directory 與 Address Book Server 之間的複寫狀態可能很耗時，也可能會耗費大量的資源，因此建議只在疑難排解時使用 **Debug-CsAddressBookReplication**。若要定期抽檢 Address Book Server 的功能，應改用 **Test-CsAddressBookService** Cmdlet 及/或 **Test-CsAddressBookWebQuery** Cmdlet。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Debug-CsAddressBookReplication"}

**Lync Server 控制台：**Lync Server 控制台不提供 D**ebug-CsAddressBookReplication** Cmdlet 所執行的功能。

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
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您指定驗證通訊錄複寫時連線的網域控制站。若未加入此參數，Cmdlet 會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注意：指定變數名稱時，請勿在前面加上 $ 字元。</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>所檢查之集區的完整網域名稱。若未加入此參數， <strong>Debug-CsAddressBookReplication</strong> Cmdlet 會驗證目前集區。</p></td>
</tr>
<tr class="even">
<td><p><em>User</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>加入此參數後，會傳回指定使用者帳戶的詳細複寫資訊。您可以利用使用者的 SIP 位址、電子郵件地址或 SamAccountName 來指定要驗證的使用者帳戶。</p></td>
</tr>
<tr class="odd">
<td><p><em>VerifyNormalization</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果指定此參數，則會傳回通訊錄正規化失敗之任何使用者帳戶的詳細資訊。正規化規則可用來將電話號碼轉換為 Lync Server 2013所使用的 E.164 格式。</p></td>
</tr>
<tr class="even">
<td><p><em>VerifyReplication</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定此參數時， <strong>Debug-CsAddressBookReplication</strong> Cmdlet 會修改 Active Directory 中的指定使用者帳戶，然後確認已將變更複寫到通訊錄。請注意，使用者帳戶修改僅供測試之用，不會實際變更該帳戶的屬性值。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Debug-CsAddressBookReplication** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Debug-CsAddressBookReplication** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.Activities.Database.AddressBookReplicationTaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsAddressBookService](test-csaddressbookservice.md)  
[Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

