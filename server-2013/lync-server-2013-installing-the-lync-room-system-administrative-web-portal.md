---
title: 安裝 Lync Room System 管理入口網站
TOCTitle: 安裝 Lync Room System 管理入口網站
ms:assetid: dd19e368-c338-4e21-a40d-6439d46a9748
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn436326(v=OCS.15)
ms:contentKeyID: 59602860
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝 Lync Room System 管理入口網站

 

_**上次修改主題的時間：** 2015-04-09_

您可以透過 Microsoft 下載中心下載 Microsoft Lync Room System 管理入口網站：[http://go.microsoft.com/fwlink/p/?LinkId=324044](http://go.microsoft.com/fwlink/p/?linkid=324044)。

若要安裝 Lync Room System 管理入口網站，請執行下列步驟：

1.  在 Lync Server 管理命令介面中執行下列 Cmdlet 以設定信任的應用程式連接埠：
    
        Set-CsWebServer -Identity POOLFQDN -MeetingRoomAdminPortalInternalListeningPort 4456 -MeetingRoomAdminPortalExternalListeningPort 4457

2.  若要安裝 Meeting Room 入口網站，請下載 **LyncRoomAdminPortal.exe** 並以系統管理員身分執行該檔案。

3.  從下列位置開啟 Web.config 檔：
    
    %Program Files%\\Microsoft Lync Server 2013\\Web Components\\Meeting Room Portal\\Int\\Handler\\

4.  在 Web.Config 檔中，將 PortalUserName 變更為＜設定 Lync Room System 管理入口網站的必要條件＞一節中由步驟 2 所建立的使用者名稱 (該步驟的建議名稱為 LRSApp)：
    
        <add key="PortalUserName" value="sip:LRSApp@domain.com" />

5.  由於 LRS 管理入口網站屬於信任的應用程式，因此您在入口網站設定中無需提供密碼。如果使用者使用的登錄器並非本機登錄器，您需要在 Web.Config 檔中新增下行，藉此為其指定登錄器：
    
        <add key="PortalUserRegistrarFQDN" value="pool-xxxx.domain.com" />

6.  若是使用的連接埠並非 5061，請在 Web.Config 檔中新增下行：
    
        <add key="PortalUserRegistrarPort" value="5061" />

## 確認安裝 Lync Room System 系統管理入口網站

若要確認安裝 Lync Room System 系統管理入口網站，請執行下列操作：


1.  在前端伺服器中，瀏覽至下列 URL：
    
    https://\<fe-server\>/lrs
    
    畫面不應出現任何錯誤，如下圖所示：
    
    ![\[Lync Room System 管理入口網站登入\] 畫面](images/Dn436326.050bcf70-2f3b-46b2-9b96-ebd12679b713(OCS.15).png "[Lync Room System 管理入口網站登入] 畫面")

2.  如果並未顯示任何錯誤，請利用拓撲中的任何其他電腦存取下列 URL：
    
    https://\<fe-server\>/lrs
    
    若要存取頁面，您必須按照＜自動用戶端登入的所需 DNS 記錄＞中所述新增 DNS 記錄：[http://go.microsoft.com/fwlink/p/?LinkId=318056](http://go.microsoft.com/fwlink/p/?linkid=318056)。

