---
title: Lync Server 2013：定義 SIP/CSTA 閘道 IP 位址
TOCTitle: 定義 SIP/CSTA 閘道 IP 位址
ms:assetid: ae944057-3ad6-4474-a09b-81a3d27bd50f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg602125(v=OCS.15)
ms:contentKeyID: 49292009
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中定義 SIP/CSTA 閘道 IP 位址

 

_**上次修改主題的時間：** 2012-09-21_

如果 Lync Server 將連接到 SIP/CSTA 閘道，而該閘道是您使用傳輸控制通訊協定 (TCP) 連線為遠端呼叫控制所部署，則您必須在 拓撲產生器中定義閘道的 IP 位址。如果是支援傳輸層安全性 (TLS) 連線的閘道，則不需要此步驟。針對支援 TLS 連線的所有閘道，您可以略過此程序，並依照 [在 Lync Server 2013 中允許 Lync 使用者進行遠端呼叫控制](lync-server-2013-enable-lync-users-for-remote-call-control.md)中的步驟，繼續部署遠端呼叫控制。

## 若要使用拓撲產生器定義 SIP/CSTA 閘道 IP 位址

1.  以 Domain Admins 群組與 RTCUniversalServerAdmins 群組成員的身分，登入安裝了拓撲產生器的電腦。

2.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

3.  選擇下載現有拓撲的選項。

4.  展開 **\[信任的應用程式伺服器\]** 節點。

5.  在您依照 [在 Lync Server 2013 中為遠端呼叫控制設定信任的應用程式項目](lync-server-2013-configure-a-trusted-application-entry-for-remote-call-control.md)所述而建立的信任應用程式集區上按一下滑鼠右鍵，然後按一下 \[編輯內容\] 。

6.  清除 **\[對此集區啟用組態資料的複寫\]** 核取方塊。

7.  按一下 **\[將服務使用方式限制為選取的 IP 位址\]** 。預設設定為 **\[使用所有設定的 IP 位址\]** 。

8.  在 **\[主要 IP 位址\]** 文字方塊中，輸入 SIP/CSTA 閘道的 IP 位址。

9.  若要更新中央管理存放區中的拓撲，請在主控台樹狀目錄中，按一下 \[Lync Server\] ，然後從 \[動作\] 窗格中，按一下 \[發行\] 。

## 請參閱

#### 工作

[在 Lync Server 2013 中設定遠端呼叫控制的靜態路由](lync-server-2013-configure-a-static-route-for-remote-call-control.md)  
[在 Lync Server 2013 中為遠端呼叫控制設定信任的應用程式項目](lync-server-2013-configure-a-trusted-application-entry-for-remote-call-control.md)

