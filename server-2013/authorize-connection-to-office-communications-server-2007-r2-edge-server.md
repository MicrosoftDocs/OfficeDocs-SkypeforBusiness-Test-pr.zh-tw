---
title: 授權連線至 Office Communications Server 2007 R2 Edge Server
TOCTitle: 授權連線至 Office Communications Server 2007 R2 Edge Server
ms:assetid: 14f6798a-28d6-4b3d-8734-942192e1bbf5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204702(v=OCS.15)
ms:contentKeyID: 49290183
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 授權連線至 Office Communications Server 2007 R2 Edge Server

 

_**上次修改主題的時間：** 2012-09-28_

針對試驗集區中的每個 Lync Server 2013 前端伺服器或 Standard Edition Server，您必須更新經授權連線至 Office Communications Server 2007 R2 Edge Server 的內部伺服器清單。若沒有這些更新，使用舊版 Edge Server 來參與外部音訊/視訊 (A/V) 會議的使用者就不會成功。

## 授權連線至 Office Communications Server 2007 R2 Edge Server

1.  在 Office Communications Server 2007 R2 Edge Server 上，從 \[系統管理工具\] 群組中，開啟 \[電腦管理\] 嵌入式管理單元。

2.  在主控台樹狀目錄中，展開 \[服務和應用程式\] 。

3.  用滑鼠右鍵按一下 \[ Office Communications Server 2007 R2\] ，然後按一下 \[內容\] 。

4.  按一下 \[內部\] 索引標籤。

5.  在 \[新增伺服器\] 下，按一下 \[新增\] 。

6.  在 \[新增 Office Communications Server\] 對話方塊中，輸入適當資訊：
    
      - 指定每個 Lync Server 2013 前端伺服器或 Standard Edition Server 以及 Lync Server 2013 集區的完整網域名稱 (FQDN)。
    
      - 指定 Lync Server 2013 Director 的 FQDN (若是在依其 FQDN 指定下一個躍點電腦的集區上設定靜態路由的話)。

7.  為每個 Lync Server 2013、前端伺服器、Standard Edition Server、集區和 Director 新增項目之後，按一下 \[套用\] ，然後按一下 \[確定\] 以關閉「內容」頁面。

