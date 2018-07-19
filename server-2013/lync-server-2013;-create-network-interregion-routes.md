---
title: 在 Lync Server 2013 中建立網路區間路由
TOCTitle: 在 Lync Server 2013 中建立網路區間路由
ms:assetid: 5555262a-a502-4b01-9593-836dd30064f5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398368(v=OCS.15)
ms:contentKeyID: 49290956
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立網路區間路由

 

_**上次修改主題的時間：** 2012-10-20_

*網路區間路由*定義了一組網路地區之間的路由。在您的通話許可控制部署中，每一組網路地區都需要搭配一個網路區間路由，以便讓部署內的每個網路地區都能互相存取。

地區連結會設定地區間連線的頻寬限制，而區間路由會決定從甲地連線到乙地時要採取的連結路徑。

如需使用網路區間路由的詳細資訊，請參閱 Lync Server 管理命令介面文件以了解下列 Cmdlet：

  - [New-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkInterRegionRoute)

  - [Get-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkInterRegionRoute)

  - [Set-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkInterRegionRoute)

  - [Remove-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkInterRegionRoute)

在範例拓撲當中，下列三組地區每一組都需要定義網路區間路由：North America/EMEA、EMEA/APAC，以及 North America/APAC。

## 使用 Lync Server 管理命令介面建立網路區間路由

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 **New-CsNetworkInterRegionRoute** Cmdlet 以定義所需的路由。例如，執行：
    
        New-CsNetworkInterRegionRoute -Identity NorthAmerica_EMEA_Route -NetworkRegionID1 NorthAmerica -NetworkRegionID2 EMEA -NetworkRegionLinkIDs "NA-EMEA-LINK"
    
        New-CsNetworkInterRegionRoute -Identity NorthAmerica_APAC_Route -NetworkRegionID1 NorthAmerica -NetworkRegionID2 APAC -NetworkRegionLinkIDs "NA-EMEA-LINK, EMEA-APAC-LINK"
    
        New-CsNetworkInterRegionRoute -Identity EMEA_APAC_Route -NetworkRegionID1 EMEA -NetworkRegionID2 APAC -NetworkRegionLinkIDs "EMEA-APAC-LINK"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>由於 North America/APAC 網路區間路由之間沒有直接的網路地區連結，因此需要用到兩個網路地區連結。</td>
    </tr>
    </tbody>
    </table>


## 使用 Lync Server 控制台建立網路區間路由

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  在左導覽列中，按一下 **\[網路組態\]**。

3.  按一下 **\[地區路由\]** 導覽按鈕。

4.  按一下 **\[新增\]**。

5.  按一下 **\[新的地區路由\]** 頁面上的 **\[名稱\]**，然後輸入網路區間路由的名稱。

6.  按一下 **\[網路地區 \#1\]**，再從您要路由轉送至網路地區 \#2 的清單中，按一下網路地區。

7.  按一下 **\[網路地區 \#2\]**，再從您要路由轉送至網路地區 \#1 的清單中，按一下網路地區。

8.  按一下 **\[網路地區連結\]** 欄位旁邊的 **\[新增\]**，接著新增將用於網路區間路由的網路地區連結。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您即將為尚未擁有直接網路地區連結的兩個網路地區建立路由，請新增所有必要的連結以便完成該路由。例如，由於 North America/APAC 網路區間路由之間沒有直接的網路地區連結，因此需要用到兩個網路地區連結。</td>
    </tr>
    </tbody>
    </table>


9.  按一下 **\[認可\]**。

10. 若要為您的拓撲完成建立網路區間路由，使用其他網路區間路由的設定並重複步驟 4 到 9。

