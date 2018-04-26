---
title: Disable-CsAdDomain
TOCTitle: Disable-CsAdDomain
ms:assetid: 98a4982c-7d8d-460d-bff9-243373b20290
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398785(v=OCS.15)
ms:contentKeyID: 49291768
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsAdDomain

 

_**上次修改主題的時間：** 2015-03-09_

復原 **Enable-CsAdDomain** Cmdlet 所執行的的網域準備工作。一般只有在解除安裝網域中的 Lync Server 時，才會使用此 Cmdlet。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Disable-CsAdDomain [-Confirm [<SwitchParameter>]] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會回復本機網域中的網域準備程序。因為未加上 Force 參數，所以如果 **Disable-CsAdDomain** Cmdlet 判斷網域中至少有一個前端伺服器、A/V 會議伺服器或 Web 服務伺服器仍在作用中，則命令會失敗。

    Disable-CsAdDomain

## 範例 2

範例 2 會回復 asia.litwareinc.com 網域的網域準備程序。

    Disable-CsAdDomain -Domain asia.litwareinc.com

## 範例 3

範例 3 所示的命令會使用 Force 參數，強制復原本機網域中的網域準備程序。這表示，即使 **Disable-CsAdDomain** Cmdlet 判斷網域中至少有一個前端伺服器、A/V 會議伺服器或 Web 服務伺服器仍在作用中，系統還是會進行復原。

    Disable-CsAdDomain -Force

## 詳細描述

當您在網域中安裝 Lync Server 時，必須已正確準備好該網域，包括擴充 Active Directory 架構以便新增 Lync Server 特有的屬性，以及將必要的存取控制項目指派給管理及操作 Lync Server 時所需的萬用群組。如果您稍後決定要解除安裝 Lync Server (或如果在安裝過程中發現問題)，則可能需要回復這些網域層級變更。**Disable-CsAdDomain** Cmdlet 提供一種方法，可讓您復原 **Enable-CsAdDomain** Cmdlet 所進行的一切網域層級修改。

請注意，**Disable-CsAdDomain** Cmdlet 執行的工作與下列 Microsoft Office Communications Server 2007 R2 命令執行的工作類似：

Lcscmd.exe /domain /action:DomainUnprep

誰可以執行這個 Cmdlet：您必須是網域系統管理員才能在本機執行 **Disable-CsAdDomain** Cmdlet。

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
<td><p><em>Domain</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>應復原網域準備作業之網域的完整網域名稱 (FQDN) (例如 -Domain asia.litwareinc.com)。如果未加上此參數，則將在本機網域上進行復原。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓系統管理員指定要在執行 <strong>Disable-CsAdDomain</strong> 時使用之網域控制站的 FQDN。若未指定，Cmdlet 會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果使用此參數，則即使 <strong>Disable-CsAdDomain</strong> Cmdlet 判斷網域中至少有一個前端、會議或 Web 服務伺服器仍在作用中，系統還是會進行復原。如果未使用此參數，則當網域中有前端、會議或 Web 服務伺服器仍在作用中時，命令會失敗。</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>網域中通用類別目錄伺服器的 FQDN。如果您執行 <strong>Disable-CsAdDomain</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
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
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\DisableDomain.html&quot;</p></td>
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

無。**Disable-CsAdDomain** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Enable-CsAdDomain](enable-csaddomain.md)  
[Get-CsAdDomain](get-csaddomain.md)

