---
title: Disable-CsComputer
TOCTitle: Disable-CsComputer
ms:assetid: e64128f1-2b53-4569-bf37-90cbbba01b36
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399023(v=OCS.15)
ms:contentKeyID: 49292640
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsComputer

 

_**上次修改主題的時間：** 2015-03-09_

停用已從 Lync Server 電腦移除之服務或伺服器角色。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Disable-CsComputer [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-Scorch <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會停用本機電腦。

    Disable-CsComputer 

## 範例 2

範例 2 所示的命令也會停用本機電腦。除了停用電腦外，此命令也會在 C:\\Logs\\Disable.html 檔案中記錄該工作是否成功的相關資料。您可以藉由新增 Report 參數加上要記錄資訊的記錄檔路徑產生這個記錄檔。

    Disable-CsComputer -Report C:\Logs\Disable.html

## 詳細描述

從電腦移除服務或伺服器角色不會自動更新 Lync Server 拓撲。而在拓撲中的變更全面更新之前，必須停用服務或角色。**Disable-CsComputer** Cmdlet 提供系統管理員停用已自本機電腦移除之任何服務或伺服器角色的方法。

除非您使用 Scorch 參數，否則 **Disable-CsComputer** Cmdlet 不會解除安裝 Lync Server 軟體；而是只會停止電腦，使其無法以其先前指派的角色運作。

誰可以執行這個 Cmdlet：您必須是本機系統管理員及網域成員才能在本機執行 **Disable-CsComputer** Cmdlet。

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
<td><p>網域中通用類別目錄伺服器的完整網域名稱 (FQDN)。如果是在電腦上以您網域中的帳戶執行 <strong>Disable-CsComputer</strong> Cmdlet，則不需要此參數。</p></td>
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
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\DisableComputer.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Scorch</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>解除安裝本機電腦的所有 Lync Server 服務與伺服器角色。</p></td>
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

無。**Disable-CsComputer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。反之，**Disable-CsComputer** Cmdlet 會停用 Microsoft.Rtc.Management.Deploy.Internal.Machine 物件的執行個體。

## 請參閱

#### 其他資源

[Enable-CsComputer](enable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

