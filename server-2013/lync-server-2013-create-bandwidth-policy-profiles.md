---
title: 在 Lync Server 2013 中建立頻寬原則設定檔
TOCTitle: 在 Lync Server 2013 中建立頻寬原則設定檔
ms:assetid: a71881ef-b04a-465e-9abb-0577bfd182f3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412785(v=OCS.15)
ms:contentKeyID: 49291925
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立頻寬原則設定檔

 

_**上次修改主題的時間：** 2012-10-19_

*頻寬原則*會定義即時音訊和視訊形式的頻寬使用限制。頻寬原則適用於*「頻寬原則設定檔」*(Bandwidth Policy Profile)，可套用至多個通話許可控制的網站。

如需您應在 CAC 部署中設定之頻寬限制的指導方針，請參閱規劃文件中的＜[在 Lync Server 2013 中定義通話許可控制需求](lync-server-2013-defining-your-requirements-for-call-admission-control.md)＞。

如需使用頻寬原則和原則設定檔的詳細資訊，請參閱 Lync Server 管理命令介面文件中的下列 Cmdlet：

  - [New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)

  - [Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

  - [Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

  - [Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)

下列程序中建立的範例原則會針對整體音訊流量、個別音訊工作階段、整體視訊流量和個別視訊工作階段設定限制。例如，5Mb\_Link 頻寬原則設定檔會設定下列限制：

  - 音訊限制：2,000 kbps

  - 音訊工作階段限制：200 kbps

  - 視訊限制：1,400 kbps

  - 視訊工作階段限制：700 kbps

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>音訊工作階段限制的最小值為 40 kbps。視訊工作階段限制的最小值為 100 kbps。</td>
</tr>
</tbody>
</table>


## 若要使用管理命令介面建立頻寬原則設定檔

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  針對您要建立的每個頻寬原則設定檔，執行 New-CsNetworkBandwidthPolicyProfile Cmdlet。例如，執行：
    
        New-CsNetworkBandwidthPolicyProfile -Identity 5Mb_Link -Description "BW profile for 5Mb links" -AudioBWLimit 2000 -AudioBWSessionLimit 200 -VideoBWLimit 1400  -VideoBWSessionLimit 700
    
        New-CsNetworkBandwidthPolicyProfile -Identity 10Mb_Link -Description "BW profile for 10Mb links" -AudioBWLimit 4000 -AudioBWSessionLimit 200 -VideoBWLimit 2800 -VideoBWSessionLimit 700
    
        New-CsNetworkBandwidthPolicyProfile -Identity 50Mb_Link -Description "BW profile for 50Mb links" -AudioBWLimit 20000 -AudioBWSessionLimit 200 -VideoBWLimit 14000 -VideoBWSessionLimit 700
    
        New-CsNetworkBandwidthPolicyProfile -Identity 25Mb_Link -Description "BW profile for 25Mb links" -AudioBWLimit 10000 -AudioBWSessionLimit 200 -VideoBWLimit 7000 -VideoBWSessionLimit 700

## 若要使用 Lync Server 控制台建立頻寬原則設定檔

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  在左導覽列中，按一下 **\[網路組態\]**。

3.  按一下 **\[原則設定檔\]** 導覽按鈕。

4.  按一下 \[新增\]。

5.  在 **\[新增原則設定檔\]** 頁面上按一下 **\[名稱\]**，然後輸入頻寬原則設定檔的名稱。

6.  按一下 **\[音訊限制\]**，然後輸入針對所有音訊工作階段總共允許的最大 kbps 數。

7.  按一下 **\[音訊工作階段限制\]**，然後輸入針對各個音訊工作階段允許的最大 kbps 數。

8.  按一下 **\[視訊限制\]**，然後輸入針對所有視訊工作階段總共允許的最大 kbps 數。

9.  按一下 **\[視訊工作階段限制\]**，然後輸入針對各個視訊工作階段允許的最大 kbps 數。

10. (選用) 按一下 **\[描述\]**，然後輸入描述此頻寬原則設定檔的其他資訊。

11. 按一下 \[認可\]。

12. 若要完成建立您拓撲的頻寬原則設定檔，請對其他頻寬原則設定檔的設定重複步驟 4 到 11。

