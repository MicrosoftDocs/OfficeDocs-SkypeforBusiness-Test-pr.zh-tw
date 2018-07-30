---
title: Lync Server 2013：設定 Web 伺服陣列 FQDN
TOCTitle: 設定 Web 伺服陣列 FQDN
ms:assetid: cb25dbbd-dcea-4997-8e14-e5007dd7d3ca
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429722(v=OCS.15)
ms:contentKeyID: 49292325
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 設定 Web 伺服陣列 FQDN

 

_**上次修改主題的時間：** 2013-03-29_

當您在 拓撲產生器中定義了 Standard Edition 伺服器、 前端集區、 Director 或 Director 集區 的組態時，您會設定外部 Web 服務完整網域名稱 (FQDN)。在隸屬於 Standard Edition 伺服器或 前端集區的用戶端進行登入的期間，所設定的 Web 服務 FQDN 會藉由頻內佈建的方式傳送出去。如果您需要新增或變更外部 Web 服務 URL，請以本主題中的程序，使用 拓撲產生器來設定或重新設定 Web 服務組態。

## 設定 Web 服務的外部集區 FQDN

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  在 拓撲產生器的 \[Standard Edition 前端\] 、\[Enterprise Edition 前端\] 和 \[Director\] 下的主控台樹狀目錄中，以滑鼠右鍵按一下您需要編輯的集區名稱，然後按一下 \[編輯屬性\] 。

3.  在 \[Web 服務\] 區段中，新增或編輯 \[外部 Web 服務 FQDN\] 。

4.  檢閱並調整 HTTP 和 HTTPS 的 \[聆聽連接埠\] 。預設值將為：
    
      - **聆聽連接埠：** HTTP 8080、HTTPS 4443
    
      - **發行的連接埠：** HTTP 80、HTTPS 443
    
    其中 \[聆聽連接埠\] 是外部 Web 服務將被設來接收反向 Proxy 傳來之要求的連接埠，而 \[發行的連接埠\] 則是反向 Proxy 對外公佈且在頻內佈建期間傳達給用戶端的連接埠。

5.  當您完成新增和更新時，請按一下 \[確定\] 繼續。

6.  以滑鼠右鍵按一下 \[ Lync Server 2013\] ，然後按一下 \[發行\] 。
    
    > [!IMPORTANT]  
    > 發行順利完成之後，可能會出現一個連結，告知您需要採取額外的步驟。如果按一下此連結，便會開啟受 拓撲產生器中所做變更影響的伺服器清單，您會需要在每部列出的伺服器上重新執行 Lync Server 部署精靈，以更新所新增、移除或變更之元件的設定。
    


7.  針對組織中的每個 Standard Edition 伺服器、 前端集區、 Director 或 Director 集區，重複執行這些步驟。

