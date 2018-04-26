---
title: 啟用遠端呼叫控制
TOCTitle: 啟用遠端呼叫控制
ms:assetid: 0b91d418-e6ed-4556-97af-e8523e01f249
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204664(v=OCS.15)
ms:contentKeyID: 49290048
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用遠端呼叫控制

 

_**上次修改主題的時間：** 2012-10-02_

遠端呼叫控制可以讓使用者透過 Lync Server 2013 控制其桌上的專用交換機 (PBX) 電話。若您在舊版環境中部署了遠端呼叫控制，並要將其移轉到 Lync Server 2013，必須執行下列工作：

1.  安裝 SIP/CSTA 閘道，並將其通訊對象設定成您的 PBX。當您部署 Lync Server 2013 整合通訊試驗集區時，需要執行此步驟。

2.  合併拓撲並移轉了原則及設定之後，請將 Lync Server 2013 設定成將 CSTA 要求路由到 SIP/CSTA 閘道。此步驟必須在自動化移轉作業之後手動執行。若要設定 CSTA 要求的路由，請執行下列動作：
    
      - 移除舊版的授權主機項目 (在 Lync Server 2013 中稱為「信任的伺服器項目」 )。若要移轉舊版部署的使用者，請務必先移除現存您為 SIP/CSTA 閘道所建立的所有授權主機項目，然後再於 Lync Server 2013 試驗集區中設定新信任的應用程式項目。如需如何移除舊版授權主機項目的詳細資訊，請參閱＜ [移除已獲授權的主機項目](remove-an-authorized-host-entry.md)＞。
    
      - 設定遠端呼叫控制的靜態路由。您可以為要支援遠端呼叫控制功能的各集區設定靜態路由，或是設定全域靜態路由，以便於未設定集區等級之靜態路由的各集區可以使用全域靜態路由。如需如何設定靜態路由的詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中設定遠端呼叫控制的靜態路由](lync-server-2013-configure-a-static-route-for-remote-call-control.md)＞。
    
      - 為每個想要支援遠端呼叫控制之集區上的遠端呼叫控制，設定信任的應用程式項目。如需如何設定信任應用程式項目的詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中為遠端呼叫控制設定信任的應用程式項目](lync-server-2013-configure-a-trusted-application-entry-for-remote-call-control.md)＞。

3.  若您部署了使用傳輸控制通訊協定 (TCP) 的 SIP/CSTA 閘道連線至 Lync Server 2013，請在拓撲產生器中定義閘道的 IP 位址。如需定義 IP 位址的詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中定義 SIP/CSTA 閘道 IP 位址](lync-server-2013-define-a-sip-csta-gateway-ip-address.md)＞。

4.  啟用遠端呼叫控制，並指派線路伺服器的統一資源識別項 (URI) 及線路 URI，為 Lync 2013 使用者設定遠端呼叫控制功能。當您將舊版部署的使用者移轉到 Lync Server 2013 時，遠端呼叫控制設定會隨其他使用者設定一併移轉。

5.  若您的舊版部署中自訂有通訊錄電話號碼正規化規則，必須在自動化移轉原則及設定的作業完成之後，執行一些手動工作，才可移轉自訂的正規化規則。若您未自訂任何正規化規則，通訊錄將會隨拓撲的剩餘部分一併移轉。如需手動移轉自訂正規化規則的詳細資訊，請參閱＜ [移轉通訊錄](migrate-address-book_1.md)＞。

