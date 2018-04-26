---
title: Disable-CsAdForest
TOCTitle: Disable-CsAdForest
ms:assetid: 06a6117c-27da-400f-8db9-eb28fe353aae
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398122(v=OCS.15)
ms:contentKeyID: 49289976
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsAdForest

 

_**上次修改主題的時間：** 2015-03-09_

復原 **Enable-CsAdForest** Cmdlet 所執行的樹系準備工作。一般只有在解除安裝 Lync Server 時，才會使用此 Cmdlet。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Disable-CsAdForest [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-GroupDomain <Fqdn>] [-GroupDomainController <Fqdn>] [-Report <String>] [-RootDomainController <Fqdn>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會回復由 **Enable-CsAdForest** Cmdlet 執行的樹系準備工作。由於未加入 Force 參數，因此當 **Disable-CsAdForest** Cmdlet 偵測到樹系中至少有一個網域仍針對 Lync Server 準備時，該命令將會失敗。在此情況下，您需要執行 **Disable-CsAdDomain** Cmdlet 來回復網域準備。

    Disable-CsAdForest

## 範例 2

在範例 2 中，即使 **Disable-CsAdForest** Cmdlet 偵測到樹系中至少有一個網域仍針對 Lync Server 準備，仍會回復樹系準備。透過加入 Force 參數，會強制執行回復。

    Disable-CsAdForest -Force

## 詳細描述

當您安裝 Lync Server 時，您會對 Active Directory 網域服務 進行許多樹系層級的變更。這些變更 (可使用 **Enable-CsAdForest** Cmdlet 來進行) 包括建立 Lync Server 特定的物件和顯示指定元、建立管理 Lync Server 所需的萬用安全性群組，以及授予全域設定物件存取管理權限給這些群組。如果您稍後決定要解除安裝 Lync Server (或如果在安裝過程中發現問題)，則可能需要回復這些樹系層級變更。 **Disable-CsAdForest** Cmdlet 提供一種方法，可讓您復原 **Enable-CsAdForest** Cmdlet 所進行的所有樹系層級修改。

**Disable-CsAdForest** Cmdlet 完成的工作與下列 Microsoft Office Communications Server 2007 R2 命令完成的工作類似：

Lcscmd.exe /forest /action:ForestUnprep

誰可以執行這個 Cmdlet：您必須具有企業系統管理員身分才能在本機執行 **Disable-CsAdForest** Cmdlet。

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
<td><p>如果此參數存在，會強制回復樹系準備步驟，即使 <strong>Disable-CsAdForest</strong> Cmdlet 偵測到樹系中至少有一個網域仍為 Lync Server 準備。如果不存在，當 <strong>Disable-CsAdForest</strong> Cmdlet 偵測到樹系中至少有一個網域仍為 Lync Server 做準備時，命令會失敗。</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的 FQDN。如果是在電腦上以您網域中的帳戶執行 <strong>Disable-CsComputer</strong> Cmdlet，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制站的 FQDN。如果全域設定是儲存在 Active Directory 網域服務 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在組態容器中，則會使用任何一個網域控制站，且會省略此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>GroupDomain</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>已建立 Lync Server 萬用群組之所在網域的完整網域名稱 (FQDN) (例如 -GroupDomain asia.litwareinc.com)。如果未加上此參數，<strong>Disable-CsAdForest</strong> Cmdlet 將在本機網域中尋找萬用群組。</p></td>
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
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\DisableForest.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>RootDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>根網域控制站的 FQDN，針對需要存取本身以外網域中之資源的用戶端，用來建立信任路徑。</p></td>
</tr>
<tr class="odd">
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

