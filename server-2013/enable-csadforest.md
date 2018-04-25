---
title: Enable-CsAdForest
TOCTitle: Enable-CsAdForest
ms:assetid: 2381fca7-294b-486d-919d-e8626cef6fea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425713(v=OCS.15)
ms:contentKeyID: 49290339
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsAdForest

 

_**上次修改主題的時間：** 2015-03-09_

您必須先修改 Active Directory，才可安裝 Lync Server，包括全面變更組態或系統容器、建立萬用群組，以及建立 Lync Server 的專用屬性集與顯示規範。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Enable-CsAdForest [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-GroupDomain <Fqdn>] [-GroupDomainController <Fqdn>] [-Report <String>] [-RootDomainController <Fqdn>] [-SkipPrepareCheck <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此命令可將 Active Directory 樹系準備妥當，以便安裝 Lync Server。由於未使用 GroupDomain 參數，所以會在本機網域中建立執行 **Enable-CsAdForest** Cmdlet 時所產生的萬用安全性群組。

    Enable-CsAdForest

## 範例 2

此命令可將 Active Directory 樹系準備妥當，以便安裝 Lync Server。GroupDomain 參數可用來確定在 northamerica.litwareinc.com 網域中，會建立透過執行 **Enable-CsAdForest** Cmdlet 所建立的萬用安全性群組。

    Enable-CsAdForest -GroupDomain northamerica.litwareinc.com

## 詳細描述

在安裝 Lync Server 之前，您必須對 Active Directory 網域服務 進行一些樹系層級的變更。包括建立顯示指定元和 Lync Server 特有的物件、建立管理 Lync Server 所需的萬用資訊安全群組，以及將全域設定物件的存取權限授與這些群組。樹系準備通常是透過 Lync Server 安裝精靈來進行。不過，企業系統管理員也可以透過執行 **Enable-CsAdForest** Cmdlet，隨時執行樹系準備。

**Enable-CsAdForest** Cmdlet 完成執行之後，您可以使用 **Get-CsAdForest** Cmdlet 來確認樹系已準備就緒以進行安裝程序的下一個步驟。

請注意，這個 Cmdlet 執行工作的方式和透過下列 Microsoft Office Communications Server 2007 R2 命令執行工作的 Cmdlet 相似：

Lcscmd.exe /forest /action:ForestPrep

誰可以執行這個 Cmdlet：您必須具有企業系統管理員身分才能在本機執行 **Enable-CsAdForest** Cmdlet。

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的 FQDN。如果您使用網域中的帳戶在電腦上執行 <strong>Enable-CsAdForest</strong> Cmdlet，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制站的 FQDN。如果全域設定是儲存在 Active Directory 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在組態容器中，則會使用任何一個網域控制站，且會省略此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>GroupDomain</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>應建立新萬用安全性群組之網域的完整網域名稱 (FQDN)。若未加入此參數，便會在本機網域中建立群組。</p></td>
</tr>
<tr class="even">
<td><p><em>GroupDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存萬用群組資訊之網域控制站的 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\ForestPrep.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>RootDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>根網域控制站的 FQDN，針對需要存取本身以外網域中之資源的用戶端，用來建立信任路徑。</p></td>
</tr>
<tr class="odd">
<td><p><em>SkipPrepareCheck</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True ($True)，則 Enable-CsAdForest 會略過其初始準備檢查作業。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

無。

