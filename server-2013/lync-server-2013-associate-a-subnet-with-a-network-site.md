---
title: Lync Server 2013：建立子網路與網路站台的關聯
TOCTitle: 建立子網路與網路站台的關聯
ms:assetid: aa69e3ac-542a-4ba1-9582-2e6bee29f633
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412804(v=OCS.15)
ms:contentKeyID: 49291975
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立子網路與網路站台的關聯

 

_**上次修改主題的時間：** 2014-10-20_

網路中的每個子網路都必須與特定網路網站關聯，這是因為在初始新的工作階段時，會使用子網路資訊來確定端點所在的網站。當已知工作階段中每一方的位置時，進階 企業語音功能可套用該資訊，以決定如何處理撥號設定或路由。

> [!IMPORTANT]  
> 在您的部署中，Audio/Video Edge Server 的所有已設定公用 IP 位址都必須新增至網路組態設定。這些 IP 位址會新增為遮罩值 32 的子網路。相關聯的網站應該對應至適當的已設定網站。例如，對應至中央網站 Chicago 中 A/V Edge Server 的公用 IP 位址會是 NetworkSiteID Chicago。如需公用 IP 位址的詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md">決定 Lync Server 2013 的外部 A/V 防火牆和連接埠需求</a>＞。



<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>會引發重要狀態指示器 (KHI) 通知，指定存在於您的網路中，但未與子網路相關聯，或包含 IP 位址的子網路未與網站相關聯的 IP 位址清單。此通知在 8 小時內不會多次引發。以下是相關的通知資訊與範例：<br />
<strong>來源 ：</strong>CS 頻寬原則服務 (核心)<br />
<strong>事件號碼 ：</strong>36034<br />
<strong>層級 ：</strong>2<br />
<strong>描述 ：</strong>下列 IP 位址的子網路：未設定 &lt;IP 位址清單&gt;，或是子網路未與網站相關聯。<br />
<strong>原因 ：</strong>網路組態設定中遺漏對應 IP 位址的子網路，或是子網路未與網站相關聯。<br />
<strong>解決方法 ：</strong>將對應至 IP 位址清單的子網路新增到網路組態設定中，並將每個子網路與網站產生關聯。<br />
例如，如果通知中的 IP 位址清單指定了 10.121.248.226 與 10.121.249.20，表示這些 IP 位址未與子網路相關聯，或是與這些位址相關聯的子網路不屬於任何網站。如果 10.121.248.0/24 與 10.121.249.0/24 是這些位址的對應子網路，您可以透過下列方式解決此問題：
<ol>
<li><p>確定 IP 位址 10.121.248.226 與 10.121.248.0/24 子網路相關聯，而 IP 位址 10.121.249.20 與 10.121.249.0/24 子網路相關聯。</p></li>
<li><p>確定 10.121.248.0/24 與 10.121.249.0/24 兩個子網路分別與一個網站相關聯。</p></li>
</ol></td>
</tr>
</tbody>
</table>


如需使用網路子網路的詳細資訊，請參閱 Lync Server 管理命令介面文件中的下列 Cmdlet：

  - [New-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkSubnet)

  - [Get-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkSubnet)

  - [Set-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkSubnet)

  - [Remove-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkSubnet)

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用大量的子網路，建議您使用逗號分隔值 (CSV) 檔案，將子網路與網站產生關聯。CSV 檔案必須有下列四欄： <strong>IPAddress</strong>、 <strong>mask</strong>、 <strong>description</strong> 和 <strong>NetworkSiteID</strong>。</td>
</tr>
</tbody>
</table>


## 使用管理命令介面將子網路與網站產生關聯

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 **New-CsNetworkSubnet** Cmdlet 以將子網路與網站產生關聯：
    
        New-CsNetworkSubnet -SubnetID <String> -MaskBits <Int32> -NetworkSiteID <String>
    
    例如：
    
        New-CsNetworkSubnet -SubnetID 172.11.12.13 - MaskBits 20 -NetworkSiteID Chicago
    
    在此範例中，您會建立子網路 172.11.12.13 與網路站台 "Chicago" 之間的關聯。

3.  針對拓撲中的所有子網路重複步驟 2。

## 若要透過匯入 CSV 檔案將子網路與網站產生關聯

1.  建立 CSV 檔案，其中包含您要新增的所有子網路。例如，使用下列內容建立名為 **subnet.csv** 的檔案：
    
    `IPAddress, mask, description, NetworkSiteID`
    
    `172.11.12.0, 24, "NA:Subnet in Portland", Portland`
    
    `172.11.13.0, 24, "NA:Subnet in Reno", Reno`
    
    `172.11.14.0, 25, "EMEA:Subnet in Warsaw", Warsaw`
    
    `172.11.15.0, 31, "EMEA:Subnet in Paris", Paris`

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行下列 Cmdlet 以匯入 **subnet.csv**，然後將其內容儲存在 Lync Server 管理存放區中：
    
        import-csv subnet.csv | foreach {New-CsNetworkSubnet $_IPAddress -MaskBits $_.mask -Description $_.description -NetworkSiteID $_.NetworkSiteID}

## 使用 Lync Server 控制台將子網路與網站產生關聯

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  在左導覽列中，按一下 **\[網路組態\]** 。

3.  按一下 **\[子網路\]** 導覽按鈕。

4.  按一下 **\[新增\]** 。

5.  在 **\[新增子網路\]** 頁面上，按一下 **\[子網路 ID\]** ，然後在您要與網站產生關聯的子網路所定義的 IP 位址範圍中，輸入第一個位址。

6.  按一下 **\[遮罩\]** ，然後輸入位元遮罩以套用至子網路。

7.  按一下 **\[網站 ID\]** ，然後選取您要新增此子網路之網站的網站 ID。
    
    > [!NOTE]  
    > 如果您尚未建立網站，此清單將是空的。如需相關程序的詳細資訊，請參閱 <a href="lync-server-2013-create-or-modify-a-network-site.md">在 Lync Server 2013 中建立或修改網站</a>。您也可以執行 <strong>Get-CsNetworkSite</strong> Cmdlet 來擷取部署的網站 ID。如需詳細資訊，請參閱 Lync Server 管理命令介面文件。
    


8.  或者，按一下 **\[描述\]** ，然後輸入描述此子網路的其他資訊。

9.  按一下 \[認可\] 。

重複這些步驟以將其他子網路新增至網站。

