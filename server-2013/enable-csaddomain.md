---
title: Enable-CsAdDomain
TOCTitle: Enable-CsAdDomain
ms:assetid: a39768de-51ae-45e8-b6b7-441b5da0b3b2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412764(v=OCS.15)
ms:contentKeyID: 49291884
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsAdDomain

 

_**上次修改主題的時間：** 2015-03-09_

修改樹系準備期間所建立之萬用群組的安全性設定，以提供代管及管理網域中可使用 Lync Server 之使用者時所需的權限。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Enable-CsAdDomain [-Confirm [<SwitchParameter>]] [-CrossForest <SwitchParameter>] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-SkipPrepareCheck <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會準備本機網域來安裝 Lync Server。

    Enable-CsAdDomain

## 範例 2

範例 2 會準備網域 asia.litwareinc.com 來安裝 Lync Server。

    Enable-CsAdDomain -Domain asia.litwareinc.com

## 詳細描述

在網域中安裝 Lync Server 之前，必須已正確準備好該網域，包括擴充 Active Directory 架構以便新增 Lync Server 特有的屬性，以及將管理及操作 Lync Server 所需的存取控制項目指派給萬用群組。網域準備作業通常會利用 Lync Server 安裝精靈來完成。然而，系統管理員也可以執行 **Enable-CsAdDomain** Cmdlet 來執行網域準備作業。

在 **Enable-CsAdDomain** Cmdlet 完成執行之後，您可以使用 **Get-CsAdDomain** Cmdlet 確認網域是否已準備好用於安裝程序的下一個步驟。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在具有多個網域的單一樹系環境中執行其子網域的準備作業時，收到下列錯誤訊息：「在 Active Directory 中找不到物件 CrossRef」，可能需要手動將 RTCComponentUniversalServices 群組從父系網域新增至子網域的 Windows Authorization Access 群組。</td>
</tr>
</tbody>
</table>


這個 Cmdlet 執行工作的方式類似於透過下列 Microsoft Office Communications Server 2007 R2 命令來進行：

Lcscmd.exe /domain /action:DomainPrep

誰可以執行這個 Cmdlet：您必須是網域系統管理員才能本機執行 **Enable-CsAdDomain** Cmdlet。

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
<td><p><em>CrossForest</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，表示會在不同樹系的網域中進行網域準備作業。如果要啟用的網域與執行此命令的電腦位於同一個樹系，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Domain</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要進行網域準備作業之網域的完整網域名稱 (FQDN) (例如 -Domain asia.litwareinc.com)。如果未加上此參數，則將在本機網域上進行網域準備作業。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>讓系統管理員指定執行 <strong>Enable-CsAdDomain</strong> Cmdlet 時所使用之網域控制站的 FQDN。若未指定，該 Cmdlet 會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的 FQDN。如果是在電腦上以您網域中的帳戶執行 <strong>Enable-CsAdDomain</strong> Cmdlet，則不需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制站的 FQDN。如果全域設定是儲存在 Active Directory 網域服務 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在設定容器中，則可以使用任何網域控制站，而且可以省略此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\DomainPrep.html&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>SkipPrepareCheck</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True ($True)，則 <strong>Enable-CsAdDomain</strong> Cmdlet 會略過其初始準備檢查作業。</p></td>
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

無。 **Enable-CsAdDomain** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Disable-CsAdDomain](disable-csaddomain.md)  
[Get-CsAdDomain](get-csaddomain.md)

