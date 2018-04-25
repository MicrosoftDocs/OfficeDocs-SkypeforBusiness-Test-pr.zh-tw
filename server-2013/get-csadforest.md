---
title: Get-CsAdForest
TOCTitle: Get-CsAdForest
ms:assetid: f063df2f-fdb2-4599-bfb0-fb4ba3584e3b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412995(v=OCS.15)
ms:contentKeyID: 49292765
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdForest

 

_**上次修改主題的時間：** 2015-03-09_

傳回表示 Active Directory 樹系設定是否正確，以便於安裝 Lync Server 的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAdForest [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-RootDomainController <Fqdn>] [-SkipPrepareCheck <$true | $false>]

## 範例

## 範例 1

範例 1 會傳回表示 Active Directory 樹系是否已正確設定以允許安裝 Lync Server 的資訊。

    Get-CsAdForest

## 範例 2

範例 2 會傳回樹系狀態資訊，並在螢幕上顯示樹系已就緒。除此之外，關於判斷樹系狀態所採取步驟的詳細資訊會寫入名為 C:\\Logs\\ForestState.html 的檔案中。此檔案包括驗證權限的所有 Active Directory 群組和 Active Directory 容器的詳細清單。

    Get-CsAdForest -Report C:\Logs\ForestState.html

## 詳細描述

在安裝 Lync Server 之前，您必須對 Active Directory 網域服務進行一些樹系層級的變更。包括建立顯示指定名稱和 Lync Server 特有的物件、建立管理 Lync Server 所需的萬用安全性群組，以及將全域設定物件的存取權限授予這些群組。**Get-CsAdForest** Cmdlet 會傳回單一值，以告訴您是否可在樹系中安裝 Lync Server。如果 **Get-CsAdForest** Cmdlet 傳回值 LC\_FORESTSETTINGS\_STATE\_READY，則您可在樹系中安裝 Lync Server。如果 Cmdlet 傳回 LC\_FORESTSETTINGS\_STATE\_NOT\_READY，則您必須先正確地準備好樹系，再嘗試安裝 Lync Server。

**Get-CsAdForest** Cmdlet 會在設定精靈中執行；如果精靈判斷樹系並未正確準備，則您將收到錯誤訊息且安裝將停止。不過，在嘗試安裝 Lync Server 之前，您也可以單獨執行安裝精靈的 **Get-CsAdForest** Cmdlet，以確認樹系的狀態。

**Get-CsAdForest** Cmdlet 執行的功能與下列 Microsoft Office Communications Server 2007 R2 命令相同：

Lcscmd.exe /forest /action:CheckForestPrepState

誰可以執行這個 Cmdlet：根據預設，擁有 Active Directory 讀取權限的使用者可在本機執行 **Get-CsAdForest** Cmdlet。一般來說，所有網域成員均擁有此權限。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdForest"}

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
<td><p>網域中通用類別目錄伺服器的完整網域名稱 (FQDN)。如您正在網域內的電腦上，以帳戶執行 <strong>Get-CsAdForest</strong> Cmdlet，則不需要此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制站的 FQDN。如果全域設定是儲存在 AD DS 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在組態容器中，則會使用任何一個網域控制站，且會省略此參數。</p></td>
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
<td><p>設為 True ($True) 時，可讓 Get-CsAdForest 執行，而不需要先執行初始準備檢查作業。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsAdForest** Cmdlet 會傳回 Microsoft.Rtc.Management.Deployment.LcForestSettingsState 物件的執行個體。

