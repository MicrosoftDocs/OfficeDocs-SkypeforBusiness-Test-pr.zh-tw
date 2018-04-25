---
title: 部署試驗 Edge Server
TOCTitle: 部署試驗 Edge Server
ms:assetid: dab345c0-8577-4c11-ac73-fe8b2a75f4cf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205306(v=OCS.15)
ms:contentKeyID: 49292510
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 部署試驗 Edge Server

 

_**上次修改主題的時間：** 2012-10-19_

本主題著重於您在部署 Lync Server 2013  Edge Server 之前應注意的設定程序。 Lync Server 2013 的部署與設定程序和 Lync Server 2010 十分類似。本節只著重在部署試驗集區時應該考量的要點。如需詳細步驟，請參閱部署文件中的＜ [在 Lync Server 2013 中部署外部使用者存取](lync-server-2013-deploying-external-user-access.md)＞，其中說明了部署的程序，並提供外部使用者存取的組態資訊。

啟動 \[定義新 Edge 集區精靈\] 一步步完成設定，配合參考下列步驟的重要設定項目。請注意，下面只列出了 \[定義新 Edge 集區精靈\] 部分頁面而已。

**定義 Edge 集區**

1.  以 Domain Admins 群組與 RTCUniversalServerAdmins 群組成員的身分，登入安裝了拓撲產生器的電腦。

2.  瀏覽至 Lync Server 2013 節點。以滑鼠右鍵按一下 \[Edge 集區\] ，然後按一下 \[新增 Edge 集區\] 。
    
    ![\[定義新的 Edge 集區\] 對話方塊](images/JJ205306.a90d388c-49ff-4620-a19d-42e2f1bb559c(OCS.15).jpg "[定義新的 Edge 集區] 對話方塊")

3.  Edge 集區可以是 \[多部電腦集區\] 或 \[單一電腦集區\] 。
    
    ![\[定義 Edge 集區 FQDN\] 對話方塊](images/JJ205306.4904fe8f-537c-4e66-a399-1bd8a316dc10(OCS.15).jpg "[定義 Edge 集區 FQDN] 對話方塊")

4.  不要啟用 \[選取功能\] 頁面上的同盟或 XMPP 同盟。同盟與 XMPP 同盟目前都是透過舊版 Lync Server 2010Edge Server 進行路由。這些功能到了移轉的後面階段還會再調整。
    
    ![\[選取功能\] 對話方塊](images/JJ205306.cb0b45a4-2856-45ba-bd97-e49fafbb077e(OCS.15).jpg "[選取功能] 對話方塊")

5.  接下來，請繼續完成下列精靈頁面：\[外部 FQDN\] 、\[定義內部 IP 位址\] 、以及 \[定義外部 IP 位址\] 。

6.  在 \[定義下一個躍點\] 頁面上，選取 Director 做為 Lync Server 2010  Edge 集區的下一個躍點。
    
    ![\[定義下一個躍點\] 對話方塊](images/JJ205306.11baf3ea-74f5-4eb7-8650-b03b3b190416(OCS.15).jpg "[定義下一個躍點] 對話方塊")

7.  在 \[建立前端或中繼集區的關聯\] 頁面上，暫時不要建立集區與此 Edge 集區的關聯。外部媒體的傳輸目前透過舊版 Lync Server 2010  Edge Server 進行路由傳送。這項設定到了移轉的後面階段還會再調整。
    
    ![\[建立前端集區的關聯\] 對話方塊](images/JJ205306.fe0da887-7b51-4564-afc5-d57da95a2eb6(OCS.15).jpg "[建立前端集區的關聯] 對話方塊")

8.  按一下 \[完成\] ，然後 \[發行\] 拓撲。

9.  執行部署文件中之＜ [安裝 Lync Server 2013 的 Edge Server](lync-server-2013-install-edge-servers.md)＞所述之步驟，在新的 Edge Server 上安裝檔案、設定憑證及啟動服務。

請您務必遵照部署文件中＜ [在 Lync Server 2013 中部署外部使用者存取](lync-server-2013-deploying-external-user-access.md)＞主題的指示。本節只提供了安裝這些伺服器角色時部分組態設定的指示

您現在應該已並行部署舊版 Lync Server 2010 Edge Server 和 Lync Server 2013 Edge Server 部署。確認部署雙方皆可正常運作，服務已啟用，且您也能管理每個部署。接著，就可以前往下一個階段。

