---
title: Lync Server 2013：容錯回復 Lync Server 同盟或 XMPP 同盟使用的 Edge 集區
TOCTitle: 容錯回復 Lync Server 同盟或 XMPP 同盟使用的 Edge 集區
ms:assetid: d40097a1-1bed-44dc-aeb6-0871927ab2b9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721897(v=OCS.15)
ms:contentKeyID: 49890331
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中容錯回復 Lync Server 同盟或 XMPP 同盟使用的 Edge 集區

 

_**上次修改主題的時間：** 2012-11-01_

在用來裝載同盟的失敗 Edge 集區恢復連線之後，請使用此程序容錯回復 Lync Server 同盟路由及 (或) 讓 XMPP 同盟路由再次使用此還原的 Edge 集區。

## 將同盟容錯回復至還原的 Edge 集區

1.  在再次可用的 Edge 集區上，啟動 Edge Services。

2.  如果您想要容錯回復 Lync Server 同盟路由以使用還原的 Edge Server，請執行下列動作：
    
      - 在前端伺服器上，開啟 \[拓撲建置器\]。展開 \[Edge 集區\] ，然後以滑鼠右鍵按一下 Edge Server 或目前為同盟設定的 Edge Server 集區。選取 \[編輯內容\] 。
    
      - 在 \[一般\] 底下的 \[編輯內容\] 中，清除 \[啟用此 Edge 集區的同盟 (連接埠 5061)\] 。按一下 \[確定\] 。
    
      - 展開 \[Edge 集區\] ，然後以滑鼠右鍵按一下原始的 Edge Server 或想要再次使用的 Edge Server 集區。選取 \[編輯內容\] 。
    
      - 在 \[一般\] 底下的 \[編輯內容\] 中，選取 \[啟用此 Edge 集區的同盟 (連接埠 5061)\] 。按一下 \[確定\] 。
    
      - 按一下 \[動作\] ，選取 \[拓撲\] ，再選取 \[發行\] 。在 \[發行拓撲\] 上看見提示時，按 \[下一步\] 。完成發行時，按一下 \[完成\] 。
    
      - 在 Edge Server 上，開啟 Lync Server 部署精靈。按一下 \[安裝或更新 Lync Server 系統\] ，然後按一下 \[安裝或移除 Lync Server 元件\] 。按一下 \[再執行一次\] 。
    
      - 在 \[安裝 Lync Server 元件\] 按 \[下一步\] 。摘要畫面將顯示執行完成的動作。在部署完成之後，按一下 \[檢視記錄檔\] 以檢視可用的記錄檔。按一下 \[完成\] 完成部署。

3.  如果您想要容錯回復 XMPP 同盟路由以使用還原的 Edge Server，請執行下列動作：
    
      - 執行下列 Cmdlet 將 XMPP 同盟路由重新指向即將裝載 XMPP 同盟的Edge 集區 (在此範例中為 EdgeServer1)：
        
            Set-CsSite Site1 -XmppExternalFederationRoute EdgeServer1.contoso.com
        
        在此範例中，Site1 網站包含即將裝載 XMPP 同盟路由的 Edge 集區，而 EdgeServer1.contoso.com 是該集區中 Edge Server 的 FQDN。
    
      - XMPP 同盟的 DNS SRV 記錄可解析成即將裝載 XMPP 同盟的 Edge 集區，如果您尚無此記錄，請依照下列範例予以新增。此 SRV 記錄的連接埠值必須是 5269。
        
            _xmpp-server._tcp.contoso.com
    
      - 在外部 DNS 伺服器上，將 XMPP 同盟的 DNS A 記錄變成指向 EdgeServer2.contoso.com。
    
      - 確認即將裝載 XMPP 同盟的 Edge 集區已對外開啟連接埠 5269。

4.  如果包含曾失敗但已還原的 Edge 集區的網站仍持續執行前端集區，您應該更新這些前端集區上的 Web 會議服務與 A/V 會議服務，才能再次使用其本機網站的 Edge 集區。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中變更與前端集區相關聯的 Edge 集區](lync-server-2013-changing-the-edge-pool-associated-with-a-front-end-pool.md)＞。

5.  如果和失敗的 Edge 集區位在同一網站的前端集區也失敗，您可以使用 Invoke–CsPoolFailback 以容錯回復前端集區。

## 請參閱

#### 工作

[在 Lync Server 2013 中容錯移轉用於 Lync Server 同盟的 Edge 集區](lync-server-2013-failing-over-the-edge-pool-used-for-lync-server-federation.md)  
[在 Lync Server 2013 中容錯移轉用於 XMPP 同盟的 Edge 集區](lync-server-2013-failing-over-the-edge-pool-used-for-xmpp-federation.md)  

#### 概念

[Lync Server 2013 中的 Edge Server 災害復原](lync-server-2013-edge-server-disaster-recovery.md)

