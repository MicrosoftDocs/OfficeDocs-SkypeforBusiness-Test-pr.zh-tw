---
title: Publish-CsTopology
TOCTitle: Publish-CsTopology
ms:assetid: d8f5dfd9-0ab6-4703-9d50-2fa50b3fd58b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398953(v=OCS.15)
ms:contentKeyID: 49292480
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Publish-CsTopology

 

_**上次修改主題的時間：** 2015-03-09_

發佈 **Get-CsTopology** Cmdlet 所擷取的 Lync Server 拓撲。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Publish-CsTopology -FileName <String> <COMMON PARAMETERS>

    Publish-CsTopology -Document <XElement> <COMMON PARAMETERS>

    Publish-CsTopology -FinalizeUninstall <SwitchParameter> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BackupFileName <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會擷取目前的拓撲，然後重新發佈。為了執行這些工作，範例中的第一個命令會使用 **Get-CsTopology** Cmdlet 搭配 AsXml 參數來擷取目前的拓撲；然後使用 Windows PowerShell 重新導向符號 (\>)，將擷取的資料儲存至名為 C:\\Topologies\\Topology.xml 的檔案中 (請注意，也可以使用 ToString 方法，將擷取的拓撲轉換成字串值)。範例中的第二個命令接著會使用 **Publish-CsTopology** Cmdlet，重新發佈新擷取的拓撲。

    (Get-CsTopology -AsXml).ToString() > C:\Topologies\Topology.xml 
    Publish-CsTopology -FileName "C:\Topologies\Topology.xml"

## 詳細描述

安裝 Lync Server 之後，您終將需要變更 Lync Server 基礎結構；例如，可能需要新增網站、刪除現有的登錄器集區或新增其他 封存伺服器。您必須使用 拓撲產生器完成這些基礎結構變更。在 拓撲產生器 中完成變更後，接下來便能使用相同的工具來發佈及啟用變更。後面兩個步驟非常重要：儘管您可以使用 拓撲產生器 視需求做出修改，不過在發佈及啟用新拓撲之前這些修改並不會生效，而您的 Lync Server 基礎結構也不會變更。

雖然在發佈變更時，系統會將新資訊 (例如，新網站或新伺服器角色) 寫入 中央管理存放區。不過這些新物件 (或新修改的物件) 並不會立即加入您的拓撲中，而是必須等到更新過的拓撲啟用後才會加入。當您在 拓撲產生器 中選取 \[發佈\] 選項時，以下兩個步驟都會發生：發佈變更 (寫入 中央管理存放區)，然後再啟用新拓撲。

**Publish-CsTopology** Cmdlet 不再是發佈使用 拓撲產生器建立之拓撲的建議方法；而應改用上一段中概述的步驟，在 拓撲產生器內完成發佈。這是因為 拓撲產生器現在會使用 拓撲產生器 XML 檔案格式 (.tbxml)；此檔案格式無法使用 **Publish-CsTopology** Cmdlet 來發佈。您唯一需要利用 **Publish-CsTopology** Cmdlet 來做的是重新發佈使用 **Get-CsTopology** Cmdlet 擷取的拓撲。以此方式發佈拓撲之後，接著需重新設定簡易 URL。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Publish-CsTopology** Cmdlet：RTCUniversalServerAdmins。但是，如果尚未指派設定權限，則您必須是網域系統管理員，才能執行 **Publish-CsTopology** Cmdlet。若要給予 RTCUniversalServerAdmins 實際使用 **Publish-CsTopology** Cmdlet 的權限，您必須在每個包含執行 Lync Server 服務之電腦的 Active Directory 容器上執行 **Grant-CsSetupPermission** Cmdlet。請注意，此限制也適用於透過 拓撲產生器啟用拓撲。如果尚未使用 **Set-CsSetupPermission** Cmdlet 來指派權限，則只有網域系統管理員能夠透過 拓撲產生器來發佈拓撲。

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
<td><p><em>Document</em></p></td>
<td><p>必要</p></td>
<td><p>System.Xml.Linq.XElement</p></td>
<td><p>可讓您發佈 XML 元素，而非 XML 檔案。這個 XML 元素必須以 System.XML.Linq.XElement 物件的形式加以設定。</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>含有新拓撲資訊之 XML 檔案的完整路徑。</p></td>
</tr>
<tr class="odd">
<td><p><em>FinalizeUninstall</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>只有在解除安裝 Lync Server 時才會使用。在移除中央管理伺服器之後，會使用 Publish-CsTopology 和 FinalizeUninstall 參數發行空白拓撲。此外這會移除中央管理伺服器的所有 Active Directory 項目。</p></td>
</tr>
<tr class="even">
<td><p><em>BackupFileName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>執行 <strong>Publish-CsTopology</strong> Cmdlet 時自動建立之備份檔案的完整路徑。如果沒有指定此參數，則 <strong>Publish-CsTopology</strong> Cmdlet 會在暫存資料夾 (%temp%) 中建立和以下範例相似的備份檔案：Publish-CsTopology-Backup-[2010_10_01][08_30_00]。在上述檔案名稱中，2010_10_01 代表發佈的日期：年 (2010)、月 (10) 及日 (01)。此外，08_30_00 代表發佈當日的時間：小時 (08)、分鐘 (30) 及秒 (00)。</p></td>
</tr>
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
<td><p>網域中通用類別目錄伺服器的完整網域名稱 (FQDN)。如果您執行 <strong>Publish-CsTopology</strong> Cmdlet 的電腦帳戶是在您的網域中，就不需要此參數。</p></td>
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
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\Publish_Topology.html&quot;</p></td>
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

無。 **Publish-CsTopology** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無，反之 **Publish-CsTopology** Cmdlet 會發佈 Microsoft.Rtc.Management.Deploy.Internal.DefaultTopology 物件的執行個體。

## 請參閱

#### 其他資源

[Enable-CsTopology](enable-cstopology.md)  
[Get-CsTopology](get-cstopology.md)  
[New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)  
[Test-CsTopology](test-cstopology.md)

