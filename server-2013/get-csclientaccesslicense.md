---
title: Get-CsClientAccessLicense
TOCTitle: Get-CsClientAccessLicense
ms:assetid: 435062d3-b7f9-400c-9ce7-fb6b6ffce44a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204853(v=OCS.15)
ms:contentKeyID: 49290746
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientAccessLicense

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織中的用戶端授權使用方式的資訊。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsClientAccessLicense -LicenseBasedType <String> -LicenseName <String> -MonitoringDatabase <String> -StartDate <DateTime> [-DailyUsage <SwitchParameter>] [-EndDate <DateTime>] <COMMON PARAMETERS>

    Get-CsClientAccessLicense -License <SwitchParameter> <COMMON PARAMETERS>

    COMMON PARAMETERS:

## 範例

## 範例 1

範例 1 所示的命令會傳回使用者型授權 (如 atl-sql-001\\Archinst 監控資料庫中所記錄) 的標準授權使用量。此範例會傳回從 2012 年 6 月 1 日 (6/1/2012) 開始，一直到目前日期這段時間的授權使用量資訊。

    Get-CsClientAccessLicense -MonitoringDatabase "atl-sql-001\Archinst" -LicenseName "Standard" -LicenseBasedType "UserBased" -StartDate "6/1/2012"

## 詳細描述

**Get-CsClientAccessLicense** Cmdlet 可讓系統管理員監控 Lync 用戶端授權的使用方式。作法是顯示用戶端授權在指定期間的使用方式 (根據使用者登錄)。請注意，此 Cmdlet 不會為您管理用戶端授權。例如，其不會在需要額外的授權時通知您，而只會傳回指定期間內所使用的授權數資訊。

除非您啟用監視服務及詳細通話記錄，否則無法使用 **Get-CsClientAccessLicense** Cmdlet；這是因為註冊資訊存放在詳細通話記錄資料庫中。另外也請注意， **Get-CsClientAccessLicense** Cmdlet 名副其實，只會傳回與用戶端授權有關的資訊。如果您需要與伺服器授權相關的資訊，則可以使用 [Get-CsService](get-csservice.md) Cmdlet 傳回所有 Lync Server 2013 資料庫的完整網域名稱 (FQDN)。如果前端伺服器的 FQDN 與後端資料庫的 FQDN 相符，表示您擁有的是標準版授權。如果這兩個 FQDN 不相符，表示您擁有的是企業版授權。

您也可能會遇到 **Get-CsClientAccessLicense** Cmdlet 傳回不正確授權計數的狀況。例如：

\* 如果行動使用者透過桌面用戶端從多個位置登入，則有可能超計授權。

\* 如果使用者透過行動用戶端連線，則可能會因為無法判斷裝置的 IP 位址而少計授權。此外，如果行動裝置在工作階段期間變更其 IP 位址，則可能超計授權。

\* 如果是從 PSTN 到 Lync 用戶端的通話或是從 Lync 用戶端到 PSTN 電話的通話，則有可能計算兩次授權。這是由於在判定工作階段中使用的授權數目時，同時使用了 Lync 使用者帳戶及 PSTN 電話號碼。

\* 如果在您執行授權使用量查詢之前，電話便已登入系統，則可能不會計算 Lync 電話的授權。

\* 如果使用者使用 PSTN 電話加入會議，則會為該次通話記錄一次授權使用量；然而，使用 PSTN 電話加入會議時，實際上並不需要授權。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需詳細資訊以及解決這些問題的方法，請參閱＜ <a href="lync-server-2013-release-notes.md">Lync Server 2013 的版本資訊</a>＞。</td>
</tr>
</tbody>
</table>


若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientAccessLicense"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsClientAccessLicense** Cmdlet 所執行的功能。

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
<td><p><em>License</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回可用的授權名稱。此參數無法與任何其他參數搭配使用；下列是唯一有效的語法：</p>
<p>Get-CsClientAccessLicense -License</p></td>
</tr>
<tr class="even">
<td><p><em>LicenseBasedType</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>指出授權是 UserBased 或 DeviceBased。若為 UserBased 授權，無論用來存取 Lync Server 的裝置數量多寡，存取 Lync Server 的每位使用者都需要有用戶端存取授權。若為 DeviceBased 授權，則用來存取 Lync Server 的每個裝置都需要有個別的授權。</p>
<p>針對不是一直在站上的使用者，以及可能會使用任何數量之不同裝置來存取 Lync Server 的使用者，通常會建議使用者型授權。裝置型授權的目標，是通常只透過共用服務 (例如桌上型電腦) 來存取 Lync Server 的站上使用者。</p></td>
</tr>
<tr class="odd">
<td><p><em>LicenseName</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>指出所擷取的授權種類。有效值為：</p>
<p>* Standard</p>
<p>* Enterprise</p>
<p>* Plus</p></td>
</tr>
<tr class="even">
<td><p><em>MonitoringDatabase</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>監控資料庫的 SQL Server 執行個體。這通常是用監控資料庫的 SQL Server 電腦及 SQL Server 執行個體完整網域名稱來指定。例如：</p>
<p>-MonitoringDatabase &quot;atl-sql-001.litwareinc.com\archinst&quot;</p>
<p>若監控資料庫是預設的 SQL Server 執行個體，將只須指定 SQL Server 電腦的 FQDN：</p>
<p>-MonitoringDatabase &quot;atl-sql-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>StartDate</em></p></td>
<td><p>必要</p></td>
<td><p>System.DateTime</p></td>
<td><p>開始檢查用戶端授權使用量的日期。例如，使用美國英文格式時，StartDate 參數可能看起來如下：</p>
<p>-StartDate &quot;1/1/2012&quot;</p>
<p>StartDate 必須早於 EndDate。</p></td>
</tr>
<tr class="even">
<td><p><em>DailyUsage</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>若指定此參數，授權使用量會依指定時段內的的每一天分開。若未指定，則會摘要指定時段內的授權使用量。</p></td>
</tr>
<tr class="odd">
<td><p><em>EndDate</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>檢查用戶端授權使用量的結束日期。例如：</p>
<p>-EndDate &quot;2/1/2012&quot;</p>
<p>結束日期必須晚於開始日期。請注意，當您呼叫 <strong>Get-CsClientAccessLicense</strong> Cmdlet 時，結束日期不會出現在輸出中。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsClientAccessLicense** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsClientAccessLicense** Cmdlet 會傳回授權資訊。

## 請參閱

#### 其他資源

[Get-CsUser](get-csuser.md)

