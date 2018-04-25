---
title: Enable-CsComputer
TOCTitle: Enable-CsComputer
ms:assetid: ac014030-4cd0-4503-b70e-12ab5b0ec34b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412815(v=OCS.15)
ms:contentKeyID: 49291964
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsComputer

 

_**上次修改主題的時間：** 2015-03-09_

啟用 Lync Server 電腦上的新服務或剛更新的服務或伺服器角色。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Enable-CsComputer [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會啟動所有已安裝在本機電腦上的新 Lync Server 服務或伺服器角色。

    Enable-CsComputer

## 範例 2

範例 2 也會啟動所有已安裝在本機電腦上的新 Lync Server 服務或伺服器角色。但在此範例中，額外的 Verbose 參數會確保 **Enable-CsComputer** Cmdlet 執行的工作會逐項顯示在螢幕上。

    Enable-CsComputer -Verbose

## 詳細描述

安裝必要的軟體不會讓電腦自動接受新服務角色；而是必須先啟用該電腦，才可以讓電腦以其新角色運作。 **Enable-CsComputer** Cmdlet 提供方法，讓系統管理員可以在本機電腦上啟用剛更新的服務或伺服器角色。

誰可以執行這個 Cmdlet：您必須是本機系統管理員及網域成員才能在本機執行 **Enable-CsComputer** Cmdlet。

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
<td><p>網域中通用類別目錄伺服器的完整網域名稱 (FQDN)。如果您執行 <strong>Enable-CsComputer</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制站的 FQDN。如果全域設定是儲存在 Active Directory 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在組態容器中，則會使用任何一個網域控制站，且會省略此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\EnableComputer.html&quot;</p></td>
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

無。 **Enable-CsComputer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。反而 **Enable-CsComputer** Cmdlet 會啟用 Microsoft.Rtc.Management.Deploy.Internal.Machine 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsComputer](disable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

