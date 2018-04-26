---
title: Get-CsTopology
TOCTitle: Get-CsTopology
ms:assetid: ad52f545-b8dd-411e-8584-b6e29fe8ef18
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412824(v=OCS.15)
ms:contentKeyID: 49292002
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTopology

 

_**上次修改主題的時間：** 2015-03-09_

傳回 Lync Server 基礎結構的資訊，包括內部網域、網站、叢集、電腦、服務及後端的 SQL Server 執行個體。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsTopology [-AsXml <SwitchParameter>] [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回您的 Lync Server 拓撲的完整詳細資訊。為達成此目的，會呼叫不含任何參數的 **Get-CsTopology** Cmdlet。

    Get-CsTopology

## 範例 2

範例 2 會傳回在您的 Lync Server 拓撲中找到的電腦相關資訊。為達成此目的，命令會先呼叫 **Get-CsTopology** Cmdlet 以傳回完整的 Lync Server 拓撲。然後再將此資訊管線傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 參數來擷取及顯示該拓撲中所包含之所有電腦的詳細資訊。

    Get-CsTopology | Select-Object -ExpandProperty Machines

## 範例 3

範例 3 所示的命令會傳回您的 Lync Server 拓撲的相關資訊，然後將該資訊儲存為 XML 檔。為了執行此工作，命令會先呼叫 **Get-CsTopology** Cmdlet 搭配 AsXml 參數，以傳回 XML 格式的資料。然後再將該格式化的資料管線傳送到 **Out-File** Cmdlet，以將資訊儲存到 C:\\Logs\\Topology.xml 檔案。

    Get-CsTopology -AsXML | Out-File C:\Logs\Topology.xml

## 詳細描述

**Get-CsTopology** Cmdlet 會傳回如何安裝與設定 Lync Server 的資訊。呼叫不含任何其他參數的 Cmdlet 時，Cmdlet 會為您提供 Lync Server 基礎結構的概觀；這個情況就像是 Cmdlet 為您提供諸如網域、網站及執行 Lync Server 服務和伺服器角色之電腦的整體概觀。或者，您可以將 **Get-CsTopology** Cmdlet 的輸出傳遞到 **Select-Object** Cmdlet；這麼做讓您可以存取部分拓撲的詳細資訊。例如，以下命令會提供關於 Lync Server 所使用之 SQL Server 執行個體的詳細資訊：

Get-CsTopology | Select-Object –ExpandProperty SqlInstances

您也可以使用 AsXml 參數以 XML 格式傳回有關整個拓撲的詳細資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsTopology** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。

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
<td><p><em>AsXml</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回 XML 格式的拓撲資訊。結合 <strong>Get-CsTopology</strong> Cmdlet、AsXml 參數及 <strong>Out-File</strong> Cmdlet，可將您的拓撲匯出到 .XML 檔案。</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取拓撲資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsTopology** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsTopology** Cmdlet 會傳回 Microsoft.Rtc.Management.Deploy.Internal.DefaultTopology 物件的執行個體。

## 請參閱

#### 其他資源

[Enable-CsTopology](enable-cstopology.md)  
[Publish-CsTopology](publish-cstopology.md)  
[Test-CsTopology](test-cstopology.md)

