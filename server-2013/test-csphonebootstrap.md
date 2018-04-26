---
title: Test-CsPhoneBootstrap
TOCTitle: Test-CsPhoneBootstrap
ms:assetid: b132446b-f264-405e-8e3a-971ab1c37694
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412852(v=OCS.15)
ms:contentKeyID: 49292029
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPhoneBootstrap

 

_**上次修改主題的時間：** 2015-03-09_

驗證使用者是否可以使用 Lync Server 的相容裝置登入 Lync Phone Edition。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsPhoneBootstrap -PhoneOrExt <String> -PIN <String> [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] [-TargetUri <String>] [-UserSipAddress <String>]

## 範例

## 範例 1

範例 1 所示的命令會驗證擁有指定電話號碼和 PIN 的使用者可使用 Lync Phone Edition 相容裝置連線到 Lync Server。為了執行測試，必須提供使用者的電話號碼 (+14255551219) 和使用者的 PIN 號碼 (0712)。

    Test-CsPhoneBootstrap -PhoneOrExt "+14255551219" -Pin "0712"

## 範例 2

範例 2 會驗證擁有指定電話號碼和 PIN 的使用者是否可以使用 Lync Phone Edition 相容裝置連線到 Lync Server。在此範例中，已加上 UserSipAddress 參數來進行額外檢查：如果擁有該 SIP 位址的使用者和擁有指定電話號碼和 PIN 的使用者不同，則測試將會失敗。

    Test-CsPhoneBootstrap -PhoneOrExt "+14255551219" -Pin "0712" -UserSipAddress "sip:kenmyer@litwareinc.com"

## 詳細描述

為了連線到 Lync Server， Lync Phone Edition 相容裝置必須使用動態主機設定通訊協定 (DHCP) 擷取 Lync Server 登錄器的位址；這些裝置也必須提供有效的電話號碼和關聯的個人識別碼 (PIN) 讓系統驗證 (此程序稱為「啟動載入」)。 **Test-CsPhoneBootstrap** Cmdlet 讓系統管理員可以驗證指定的使用者 (使用指派給使用者的電話號碼和 PIN) 是否能從 Lync Phone Edition 相容裝置登入系統 (執行此測試實際上不需要任何裝置)。

為了讓 **Test-CsPhoneBootstrap** Cmdlet 可以進行檢查，要測試的使用者帳戶所屬之登錄器集區必須可以使用 DHCP 進行探索。若要判斷是否可以使用此方法探索登錄器，可以使用 [Get-CsRegistrarConfiguration](get-csregistrarconfiguration.md) Cmdlet 並檢查 EnableDHCPServer 屬性的值。如果此屬性設為 False，就必須使用 [Set-CsRegistrarConfiguration](set-csregistrarconfiguration.md) Cmdlet 來將屬性值設為 True，並設定成可使用 DHCP 來探索登錄器。使用企業 DHCP 伺服器並設定 Lync Server 特有的選項，也可以達成此目的。

誰可以執行這個 Cmdlet：若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPhoneBootstrap"}

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
<td><p><em>PhoneOrExt</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要測試的使用帳戶之電話號碼或分機號碼。例如：-PhoneOrExt &quot;+14255551219&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>PIN</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要測試的使用者帳戶之 PIN。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。此變數包含兩個方法 (ToHTML 和 ToXML)，可用於將輸出儲存為 HTML 或 XML 檔案。</p>
<p>若要將輸出儲存在名為 $TestOutput 的記錄器變數中，請使用下列語法：</p>
<p>-OutLoggerVariable TestOutput</p>
<p>附註：指定變數名稱時，請勿在前面加上 $ 字元。若要將儲存在記錄器變數中的資訊儲存為 HTML 檔案，請使用類似下列的命令：</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>若要將儲存在記錄器變數中的資訊儲存為 XML 檔案，請使用類似下列的命令：</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如有指定此參數，會將執行 Cmdlet 的詳細輸出儲存在指定的變數中。例如，若要將輸出儲存在名為 $TestOutput 的變數中，請使用下列語法：</p>
<p>-OutVerboseVariable TestOutput</p>
<p>指定變數名稱時，請勿在前面加上 $ 字元。</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>登錄器服務所使用的 SIP 連接埠。如果登錄器使用預設連接埠 5061，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要測試的使用者帳戶所屬之登錄器集區的完整網域名稱 (FQDN)。若未指定，則將會使用 DHCP 探索來尋找登錄器集區。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>憑證佈建服務的 URL。如果未包含此參數，則將使用 DHCP 探索來尋找目標 URI。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>文字中所使用之使用者帳戶的 SIP 位址；例如：-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。UserSipAddress 參數必須參考所提供的電話號碼和 PIN；如果所含的電話號碼和 PIN 不屬於 UserSipAddress 參數指定的使用者，則測試將會失敗。請注意，SIP 位址必須包含 &quot;sip:&quot; 首碼。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Test-CsPhoneBootstrap** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsPhoneBootstrap** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsRegistration](test-csregistration.md)

