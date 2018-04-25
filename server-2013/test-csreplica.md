---
title: Test-CsReplica
TOCTitle: Test-CsReplica
ms:assetid: cef1fcda-3292-411a-b3dd-7a8ef7935b20
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205289(v=OCS.15)
ms:contentKeyID: 49292369
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsReplica

 

_**上次修改主題的時間：** 2015-03-09_

驗證本機電腦上的複本服務狀態。此複本服務可將資訊複寫到拓撲中的所有 Lync Server 2013 電腦。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Test-CsReplica [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>]

## 範例

## 範例 1

範例 1 所示的命令會測試本機電腦上的 Lync Server 2013複本服務。在此範例中，使用 Verbose 參數來確定測試的資訊 (包括測試結果為失敗或成功及測試產生報告的位置) 顯示在螢幕上。

    Test-CsReplica -Verbose

## 範例 2

範例 2 是範例 1 所示命令的變化。但此範例會加入 Report 參數，以指定測試所產生之報告的資料夾路徑和名稱。若未指定報告路徑，會為報告指定類似下列之自動產生的名稱：

C:\\Users\\Administrator.Litwareinc\\AppData\\Local\\Temp\\1\\Test-Cs-Replica-3db40ee0-4b5d-4f58-8d3d-b1e61253129e.html

    Test-CsReplica -Verbose -Report C:\Logs\ReplicaTest.html

## 詳細描述

**Test-CsReplica** Cmdlet 可驗證本機電腦上有無執行 Lync Server 2013 複本服務。**Test-CsReplica** Cmdlet 執行的作業包括：檢查複寫器代理程式與集中式記錄代理程式服務的狀態、驗證 Windows 防火牆上已開啟所需的連接埠，以及確認所需的 Active Directory 與本機電腦安全性群組是否存在。

請注意，此 Cmdlet 必須在本機執行，亦即必須在執行複本服務的電腦上執行。您無法對遠端伺服器執行 **Test-CsReplica** Cmdlet。

**Lync Server 控制台：**Lync Server 控制台不提供 **Test-CsReplica** Cmdlet 所執行的功能。

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
<td><p>網域中通用類別目錄伺服器的完整網域名稱。如果您執行 <strong>Test-CsReplica</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中網域控制站的完整網域名稱。如果您執行 <strong>Test-CsReplica</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：</p>
<p>-Report &quot;C:\Logs\ReplicaTest.html&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsReplica** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsReplica** Cmdlet 會傳回 Microsoft.Rtc.SyntheticTransactions.TaskOutput 物件的執行個體。

