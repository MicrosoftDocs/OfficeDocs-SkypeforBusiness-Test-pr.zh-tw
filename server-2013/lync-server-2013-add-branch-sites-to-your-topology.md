---
title: Lync Server 2013：新增分支網站至拓撲
TOCTitle: 新增分支網站至拓撲
ms:assetid: b9c35fb0-0081-4aeb-8f95-ac2fcc6c3335
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412905(v=OCS.15)
ms:contentKeyID: 49292113
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中新增分支網站至拓撲

 

_**上次修改主題的時間：** 2012-10-05_

分支網站代表會透過 WAN 連結連線至您主要辦公室的實體分公司。若要新增分支網站至您的 Lync 拓撲，請在中央網站執行下列程序。

## 若要將分支網站新增至拓撲

1.  依序按一下 \[開始\] 、\[程式集\] 、\[Microsoft Lync Server\] 及 \[Lync Server 拓撲建置器\] 。

2.  在主控台樹狀目錄中，展開中央網站，以滑鼠右鍵按一下 \[分支網站\] ，然後按一下 \[新增分支網站\] 。

3.  在 \[定義新的分支網站\] 對話方塊中，按一下 \[名稱\]，然後輸入分支網站的名稱。

4.  (選用) 按一下 \[描述\] ，然後為分支網站輸入有意義的描述。

5.  按 **\[下一步\]** 。

6.  (選用) 在下一個 \[定義新的分支網站\] 對話方塊中，執行下列任一項：
    
      - 按一下 \[城市\]，然後輸入分支網站所在之城市的名稱。
    
      - 按一下 \[省/地區\]，然後輸入分支網站所在之省或地區的名稱。
    
      - 按一下 \[國碼\]，然後輸入分支網站所在之國家/地區的兩位數撥號碼。

7.  按 \[下一步\]，然後執行下列作業：
    
      - 如果您在此網站使用 Survivable Branch Appliance 或 Server，務必確定已選取 **\[當這個精靈關閉時，開啟新的 Survivable Branch Appliance 精靈\]** 核取方塊，按一下 **\[完成\]** ，然後依照開啟的精靈中的指示執行。如需有關精靈項目的詳細資訊，請參閱＜ [在 Lync Server 2013 中定義 Survivable Branch Appliance 或 Survivable Branch Server](lync-server-2013-define-a-survivable-branch-appliance-or-server.md)＞。
    
      - 如果您不在此網站使用 Survivable Branch Appliance 或 Server，請清除 \[當這個精靈關閉時，開啟新的 Survivable Branch Appliance 精靈\] 核取方塊，然後按一下 \[完成\] 。

8.  針對您要新增至拓撲的每一個分支網站重複上述步驟。

**下一步：**

針對 Survivable Branch Appliance 或 Survivable Branch 伺服器：＜ [在 Lync Server 2013 中定義 Survivable Branch Appliance 或 Survivable Branch Server](lync-server-2013-define-a-survivable-branch-appliance-or-server.md)＞

針對不具彈性的 PSTN 連線：＜ [在 Lync Server 2013 中定義分支網站的 PSTN 閘道](lync-server-2013-define-a-pstn-gateway-for-a-branch-site.md)＞、＜ [在 Lync Server 2013 中設定含媒體旁路的主幹](lync-server-2013-configure-a-trunk-with-media-bypass.md)＞或＜ [在 Lync Server 2013 中設定無媒體旁路的主幹](lync-server-2013-configure-a-trunk-without-media-bypass.md)＞

