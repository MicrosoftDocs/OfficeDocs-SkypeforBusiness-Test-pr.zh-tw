---
title: 在 Lync Server 2013 中建立網路區域連結
TOCTitle: 在 Lync Server 2013 中建立網路區域連結
ms:assetid: f8163910-8935-475d-88a2-3aa44feb9dbe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413047(v=OCS.15)
ms:contentKeyID: 49292858
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立網路區域連結

 

_**上次修改主題的時間：** 2012-10-19_

網路之中的地區是透過實體 WAN 連線相連結。*「網路地區連結」*(Network Region Link) 會在為通話許可控制 (CAC) 設定的兩個地區之間建立連結，並且設定這些地區之間音訊和視訊流量的頻寬限制。

如需使用網路地區連結的詳細資訊，請參閱 Lync Server 管理命令介面文件中的下列 Cmdlet：

  - [New-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkRegionLink)

  - [Get-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkRegionLink)

  - [Set-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkRegionLink)

  - [Remove-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkRegionLink)

範例拓撲中包含北美和 APAC 地區之間的連結，以及 EMEA 和 APAC 地區之間的連結。這些地區連結都會受限於 WAN 頻寬，如規劃文件中＜[範例：在 Lync Server 2013 中收集通話許可控制服務需求](lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md)＞一節的＜地區連結頻寬資訊表＞中所述。

## 若要使用 Lync Server 管理命令介面建立網路地區連結

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 New-CsNetworkRegionLink Cmdlet 建立地區連結，並且套用適當的頻寬原則設定檔。例如，執行：
    
    ```
    New-CsNetworkRegionLink -NetworkRegionLinkID NA-EMEA-LINK -NetworkRegionID1 NorthAmerica -NetworkRegionID2 EMEA -BWPolicyProfileID 50Mb_Link
    ```
    ```
    New-CsNetworkRegionLink -NetworkRegionLinkID EMEA-APAC-LINK -NetworkRegionID1 EMEA -NetworkRegionID2 APAC -BWPolicyProfileID 25Mb_Link
    ```

## 若要使用 Lync Server 控制台建立網路地區連結

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  在左導覽列中，按一下 **\[網路組態\]**。

3.  按一下 **\[地區連結\]** 導覽按鈕。

4.  按一下 **\[新增\]**。

5.  在 **\[新增地區連結\]** 頁面上，按一下 **\[名稱\]**，然後輸入網路地區連結的名稱。

6.  按一下 **\[網路地區 \#1\]**，然後按一下清單中要連結至 \[網路地區 \#2\] 的網路地區。

7.  按一下 **\[網路地區 \#2\]**，然後按一下清單中要連結至 \[網路地區 \#1\] 的網路地區。

8.  (選用) 按一下 **\[頻寬原則\]**，然後選取您要套用至網路地區連結的頻寬原則設定檔。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>只有在網路地區連結受限於頻寬，而且您想要在該連結上使用 CAC 控制媒體流量時，才套用頻寬原則。</td>
    </tr>
    </tbody>
    </table>


9.  按一下 **\[認可\]**。

10. 若要完成建立拓撲的網路地區連結，請使用其他地區的設定重複步驟 4 到 9。

