---
title: Test-CsTopology
TOCTitle: Test-CsTopology
ms:assetid: 06ffa245-f1c7-46b7-9be6-5b291deda5c1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398127(v=OCS.15)
ms:contentKeyID: 49289980
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsTopology

 

_**上次修改主題的時間：** 2015-03-09_

驗證 Lync Server 安裝的服務啟用和群組權限。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsTopology [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-Service <String>]

## 範例

## 範例 1

範例 1 會驗證整個 Lync Server 拓撲。

    Test-CsTopology

## 範例 2

範例 2 所示的命令是範例 1 所示命令的變化。但此範例加入了 Report 參數以指定應該寫入輸出檔案的位置 (C:\\Logs\\Topology.xml)。

    Test-CsTopology -Report "C:\Logs\Topology.xml"

## 範例 3

在範例 3 中，**Test-CsTopology** Cmdlet 用來驗證單一服務：Registrar:atl-cs-001.litwareinc.com。

    Test-CsTopology -Service "Registrar:atl-cs-001.litwareinc.com"

## 詳細描述

**Test-CsTopology** Cmdlet 可您驗證 Lync Server 是否在全域層級運作正常。根據預設，此 Cmdlet 會檢查整個 Lync Server 基礎結構，以驗證必要的服務都在執行，而且已針對這些服務及安裝 Lync Server 時建立之萬用安全性群組設定適當的權限。

除了完整驗證 Lync Server 的有效性以外，**Test-CsTopology** Cmdlet 也可讓您檢查特定服務的有效性。例如，以下命令會檢查 atl-cs-001.litwareinc.com 集區上的 A/V 會議伺服器狀態：

Test-CsTopology –Service "ConferencingServer:atl-cs-001.litwareinc.com".

誰可以執行這個 Cmdlet：若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsTopology"}

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
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的完整網域名稱 (FQDN)。如果您要在電腦上使用網域中的帳戶執行 <strong>Test-CsTopology</strong> Cmdlet ，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制站的 FQDN。如果全域設定是儲存在 Active Directory 網域服務 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在組態容器中，則會使用任何一個網域控制站，且會省略此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\Topology.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Service</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如有指定此參數，<strong>Test-CsTopology</strong> Cmdlet 會將其驗證檢查限制為指定的服務。(請注意，使用 Service 參數時，一次只能指定一個服務)。您應該使用適當的服務 ID 來指定服務；例如，下列語法會參考 atl-cs-001.litwareinc.com 集區上的登錄器服務：-Service &quot;Registrar:atl-cs-001.litwareinc.com&quot;。</p>
<p>若未加入此參數，則會驗證整個拓撲。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsTopology** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsTopology** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

## 請參閱

#### 其他資源

[Enable-CsTopology](enable-cstopology.md)  
[Get-CsTopology](get-cstopology.md)  
[Publish-CsTopology](publish-cstopology.md)

