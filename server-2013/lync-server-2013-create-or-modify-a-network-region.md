---
title: Lync Server 2013：建立或修改網路地區
TOCTitle: 建立或修改網路地區
ms:assetid: bf7a3dc4-71a2-4559-a547-d90305d4f904
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412933(v=OCS.15)
ms:contentKeyID: 49292184
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立或修改網路地區

 

_**上次修改主題的時間：** 2012-10-19_

「網路地區」 是用於通話許可控制服務、E9-1-1 及媒體旁路設定的網路集線器或骨幹。使用下列程序可以建立或修改網路地區。例如，您已為一個語音功能建立網路地區，便不需要建立新的網路地區；其他的進階 Enterprise Voice 功能會使用那些相同的網路地區。不過，您必須修改現有的網路地區定義，以套用功能專用的設定。例如，您已為 E9-1-1 (其不需要相關的中央網站) 建立網路地區，而您接著要部署通話許可控制服務，您便必須修改網路地區定義來指定中央網站。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中設定 CAC 的網路區域](lync-server-2013-configure-network-regions-for-cac.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>網路地區定義的任何功能特定需求都記載在功能的部署主題中。</td>
</tr>
</tbody>
</table>


如需使用網路地區的詳細資訊，請參閱 Lync Server 管理命令介面文件中的下列 Cmdlet：

  - [New-CsNetworkRegion](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkRegion)

  - [Get-CsNetworkRegion](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkRegionLink)

  - [Set-CsNetworkRegion](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkRegion)

  - [Remove-CsNetworkRegion](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkRegion)

## 建立網路地區

建立網路地區，以便提供給通話許可控制、E9-1-1 或媒體旁路使用。

## 若要使用 Lync Server 管理命令介面建立網路地區

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 New-CsNetworkRegion Cmdlet 以建立網路地區：
    
        New-CsNetworkRegion -Identity <String> -CentralSite <String>
    
    例如：
    
        New-CsNetworkRegion -Identity NorthAmerica -CentralSite CHICAGO -Description "All North America Locations"
    
    在此範例中，您會建立一個稱為 "NorthAmerica" 的網路地區，該地區與網站 ID 為 CHICAGO 的中央網站相關聯。

3.  若要完成建立拓撲的網路地區，請使用每個網路地區的設定重複步驟 2。

## 若要使用 Lync Server 控制台建立網路地區

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  在左導覽列中，按一下 **\[網路組態\]** 。

3.  按一下 **\[地區\]** 。

4.  按一下 **\[新增\]** 。

5.  在 **\[新增地區\]** 頁面上，按一下 **\[名稱\]** ，然後輸入網路地區的名稱。

6.  按一下 **\[中央站台\]** ，然後按一下清單中的中央網站。

7.  (選用) 按一下 **\[描述\]** ，然後輸入用來描述此網站的其他資訊。

8.  按一下 \[認可\] 。

9.  若要完成建立拓撲的網路地區，請使用其他地區的設定重複步驟 4 到 8。

## 修改網路地區

修改現有網路地區的設定，以配合基本地區資訊的變更或新功能所需的變更。

## 若要使用 Lync Server 管理命令介面修改網路地區

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 Set-CsNetworkRegion Cmdlet 以修改現有的網路地區：
    
        Set-CsNetworkRegion -Identity <String> -CentralSite <String>
    
    例如：
    
        Set-CsNetworkRegion -Identity NorthAmerica -CentralSite CHICAGO -Description "North American Region"
    
    在此範例中，您會透過變更描述的方式修改稱為 "NorthAmerica" (使用本主題稍早所述的程序建立) 的現有網路地區。如已存在 "NorthAmerica" 地區的描述，此命令會使用此值予以覆寫；若尚未設定任何描述，則此命令會進行設定。

3.  若要修改其他網路地區，請使用其他地區的設定重複步驟 2。

## 若要使用 Lync Server 控制台修改網路地區

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  在左導覽列中，按一下 **\[網路組態\]** 。

3.  按一下 **\[地區\]** 導覽按鈕。

4.  在表格中，按一下您要修改的網路地區。

5.  按一下 **\[編輯\]** ，然後按一下 **\[顯示詳細資料...\]** 。

6.  在 **\[編輯地區\]** 頁面上，適當地變更這個網路地區的設定值。

7.  按一下 \[認可\] 。

8.  若要完成修改網路地區，請使用其他地區的設定重複步驟 4 到 7。

