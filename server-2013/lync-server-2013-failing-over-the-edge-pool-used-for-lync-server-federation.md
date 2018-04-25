---
title: Lync Server 2013：容錯移轉用於 Lync Server 同盟的 Edge 集區
TOCTitle: 容錯移轉用於 Lync Server 同盟的 Edge 集區
ms:assetid: 5c9da0f2-7429-40bb-bb3c-5cc4ecb5a13d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688071(v=OCS.15)
ms:contentKeyID: 49890087
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中容錯移轉用於 Lync Server 同盟的 Edge 集區

 

_**上次修改主題的時間：** 2012-09-17_

如果在設定 Lync Server 同盟的 Edge 集區發生問題，則必須變更同盟使用不同的 Edge 集區，同盟才能運作。

## 容錯移轉用於 Lync Server 同盟的 Edge 集區

1.  在前端伺服器上，開啟 \[拓撲建置器\]。展開 \[Edge 集區\] ，然後以滑鼠右鍵按一下 Edge Server 或目前為同盟設定的 Edge Server 集區。選取 \[編輯內容\] 。

2.  在 \[一般\] 底下的 \[編輯內容\] 中，清除 \[啟用此 Edge 集區的同盟 (連接埠 5061)\] 。按一下 \[確定\] 。

3.  展開 \[Edge 集區\] ，然後在現在要用於同盟的 Edge Server 或 Edge Server 集區上按一下滑鼠右鍵。選取 \[編輯內容\] 。

4.  在 \[一般\] 底下的 \[編輯內容\] 中，選取 \[啟用此 Edge 集區的同盟 (連接埠 5061)\] 。按一下 \[確定\] 。

5.  按一下 \[動作\] ，選取 \[拓撲\] ，再選取 \[發行\] 。在 \[發行拓撲\] 上看見提示時，按 \[下一步\] 。完成發行時，按一下 \[完成\] 。

6.  在 Edge Server 上，開啟 Lync Server 部署精靈。按一下 \[安裝或更新 Lync Server 系統\] ，然後按一下 \[安裝或移除 Lync Server 元件\] 。按一下 \[再執行一次\] 。

7.  在 \[安裝 Lync Server 元件\] 按 \[下一步\] 。摘要畫面將顯示執行完成的動作。在部署完成之後，按一下 \[檢視記錄檔\] 以檢視可用的記錄檔。按一下 \[完成\] 完成部署。
    
    如果失敗 Edge 集區所在的網站包含仍在執行的前端伺服器，則必須更新在這些前端集區上的 Web 會議服務及 A/V 會議服務，以使用遠端網站上仍在執行的 Edge 集區。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中變更與前端集區相關聯的 Edge 集區](lync-server-2013-changing-the-edge-pool-associated-with-a-front-end-pool.md)＞。

## 請參閱

#### 工作

[在 Lync Server 2013 中容錯移轉用於 XMPP 同盟的 Edge 集區](lync-server-2013-failing-over-the-edge-pool-used-for-xmpp-federation.md)  
[在 Lync Server 2013 中容錯回復 Lync Server 同盟或 XMPP 同盟使用的 Edge 集區](lync-server-2013-failing-back-the-edge-pool-used-for-lync-server-federation-or-xmpp-federation.md)  

#### 概念

[Lync Server 2013 中的 Edge Server 災害復原](lync-server-2013-edge-server-disaster-recovery.md)

