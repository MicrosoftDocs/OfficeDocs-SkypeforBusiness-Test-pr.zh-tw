---
title: Debug-CsUnifiedContactStore
TOCTitle: Debug-CsUnifiedContactStore
ms:assetid: 8e92d262-604d-41b1-9530-947765025a79
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994054(v=OCS.15)
ms:contentKeyID: 52056169
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Debug-CsUnifiedContactStore

 

_**上次修改主題的時間：** 2015-03-09_

驗證某位使用者 (或一群使用者) 的連絡人是否儲存在統一連絡人存放區中。

此 Cmdlet 是在 2013 年 2 月 Lync Server 2013 的累計更新中導入。

## 語法

    Debug-CsUnifiedContactStore -Identity <UserIdParameter> [-ContactDataExportFileName <String>] <COMMON PARAMETERS>

    Debug-CsUnifiedContactStore -PoolFqdn <Fqdn> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會驗證所有在 atl-cs-001.litwareinc.com 集區上擁有帳戶之使用者的統一連絡人存放區狀態。

    Debug-CsUnifiedContactStore -PoolFqdn "atl-cs-001.litwareinc.com"

## 範例 2

範例 2 會驗證單一使用者 (SIP 位址為 "kenmyer@litwareinc.com" 的使用者) 的統一連絡人存放區狀態。

    Debug-CsUnifiedContactStore -Identity "kenmyer@litwareinc.com"

## 詳細描述

統一連絡人存放區 (於 Lync Server 2013 中導入) 可讓使用者從多個應用程式存取連絡人清單；這些應用程式包括 Microsoft Lync 2013、Outlook 2013 及 Outlook Web App。藉由將連絡人資訊儲存在單一位置便可採用這種方式存取︰Microsoft Exchange Server 2013。

**Debug-CsUnifiedContactStore** Cmdlet 可讓系統管理員驗證某位特定使用者或特定的一組使用者 (亦即所有在某特定集區上擁有帳戶的使用者)，是否將連絡人清單儲存在統一連絡人存放區中。如果您針對某個使用者帳戶執行 **Debug-CsUnifiedContactStore** Cmdlet，此 Cmdlet 會指出該使用者的連絡人是否已為了統一連絡人存放區而移動、為了移動這些連絡人所嘗試的次數，以及 Lync Server 最後嘗試移轉連絡人清單的日期和時間。如果是針對集區執行呼叫，則 **Debug-CsUnifiedContactStore** Cmdlet 會傳回類似下列的資料︰

FrontEnd: atl-cs-001.litwareinc.com  
UcsDisabledCount: 44  
UcsAllowedCount: 129  
UcsMigratingCount: 11  
UcsMigratedCount:  
FailedUserData:

**Debug-CsUnifiedContactStore** Cmdlet 和 ContactDataExportFileName 參數也可用於將使用者的連絡人資訊匯出至 XML 檔案。

若要傳回所有獲指派此 Cmdlet 之角色型存取控制 (RBAC) 角色的清單 (包括您建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Debug-CsUnifiedContactStore"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Debug-CsUnifiedContactStore** Cmdlet 所執行的功能。

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>要驗證統一連絡人存放區狀態之個別使用者的 SIP 位址 (每個命令您只可以指定一位使用者)。例如︰</p>
<p>-Identity &quot;kenmyer@litwareinc.com&quot;</p>
<p>指定 SIP 位址時，sip: 首碼可選用。您也可使用下列語法︰</p>
<p>-Identity &quot;sip:kenmyer@litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>PoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>正在驗證統一連絡人存放區狀態之登錄器集區的完整網域名稱。所有位於指定集區的使用者帳戶都會經過檢查。例如︰</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ContactDataExportFileName</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>當那些連絡人從統一連絡人存放區匯出時，將包含指定使用者之連絡人的 XML 檔案的檔案路徑。例如︰</p>
<p>-ContactDataExportFileName &quot;C:\Exports\KenMyer.xml&quot;</p>
<p>請注意，您必須加入 Identity 參數和您要匯出連絡人之使用者的 SIP 位址。如果尚未針對統一連絡人存放區啟用該使用者，則命令會終止，且不會匯出任何連絡人。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Debug-CsUnifiedContactStore** Cmdlet 不接受管線傳送的資料。

## 傳回類型

**Debug-CsUnifiedContactStore** Cmdlet 會傳回 Microsoft.Rtc.Management.Presence.Cmdlets.GetUcsFrontEndData 物件的執行個體。

## 請參閱

#### 其他資源

[Test-CsUnifiedContactStore](test-csunifiedcontactstore.md)

