---
title: Lync Server 2013：將 Lync Server 2013 Survivable Branch Appliance 分支網站新增至您的拓撲
TOCTitle: 將 Lync Server 2013 Survivable Branch Appliance 分支網站新增至您的拓撲
ms:assetid: d3142a37-4606-456d-8ea9-6cc0e51e55f3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721896(v=OCS.15)
ms:contentKeyID: 49890327
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將 Lync Server 2013 Survivable Branch Appliance 分支網站新增至您的拓撲

 

_**上次修改主題的時間：** 2012-10-07_

Microsoft Lync Server 2013Survivable Branch Appliance (SBA) 無法做為備份登錄器與 Microsoft Lync Server 2010前端集區產生關聯。SBA 必須與 Microsoft Lync Server 2013前端集區產生關聯。以下步驟假設採用 Microsoft Lync Server 2013 SBA。請在中央網站執行此程序。

## 將採用 Microsoft Lync Server 2013 SBA 的分支網站新增至拓撲

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  在主控台樹狀目錄中，展開中央網站、展開 \[分支網站\] ，然後按一下 \[新增分支網站\] 。

3.  在 \[定義新的分支網站\] 對話方塊中，按一下 \[名稱\] ，然後輸入新分支網站的名稱。

4.  (選用) 按一下 \[描述\] ，然後為分支網站輸入有意義的描述。

5.  按 **\[下一步\]** 。

6.  (選用) 在下一個 \[定義新的分支網站\] 對話方塊中，執行下列任一項：
    
      - 按一下 \[城市\]，然後輸入分支網站所在之城市的名稱。
    
      - 按一下 \[省/地區\]，然後輸入分支網站所在之省或地區的名稱。
    
      - 按一下 \[國碼\]，然後輸入分支網站所在之國家/地區的兩位數撥號碼。

7.  按 \[下一步\]，然後執行下列作業：
    
      - 如果您在此網站使用 Survivable Branch Appliance 或 Survivable Branch 伺服器，請務必選取 \[當這個精靈關閉時，開啟新的 Survivable Branch Appliance 精靈\] 核取方塊。
    
      - 如果您未在此網站使用 Survivable Branch Appliance 或 Survivable Branch 伺服器，請清除 \[當這個精靈關閉時，開啟新的 Survivable Branch Appliance 精靈\] 核取方塊。
    
      - 按一下 \[完成\] ，然後依照所開啟精靈中的指示執行。如需有關精靈項目的詳細資訊，請參閱＜ [在 Lync Server 2013 中定義 Survivable Branch Appliance 或 Survivable Branch Server](lync-server-2013-define-a-survivable-branch-appliance-or-server.md)＞。

8.  針對您要新增至拓撲的每一個分支網站重複上述步驟。

## 請參閱

#### 工作

[在 Lync Server 2013 中定義 Survivable Branch Appliance 或 Survivable Branch Server](lync-server-2013-define-a-survivable-branch-appliance-or-server.md)  
[在 Lync Server 2013 中定義分支網站的 PSTN 閘道](lync-server-2013-define-a-pstn-gateway-for-a-branch-site.md)  
[在 Lync Server 2013 中設定含媒體旁路的主幹](lync-server-2013-configure-a-trunk-with-media-bypass.md)  
[在 Lync Server 2013 中設定無媒體旁路的主幹](lync-server-2013-configure-a-trunk-without-media-bypass.md)

