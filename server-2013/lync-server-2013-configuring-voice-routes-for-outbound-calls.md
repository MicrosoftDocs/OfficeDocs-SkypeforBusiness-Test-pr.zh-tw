---
title: Lync Server 2013：設定撥出電話的語音路由
TOCTitle: 設定撥出電話的語音路由
ms:assetid: 3c182cdd-7a4a-4a9d-bdac-4199f0abd947
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425890(v=OCS.15)
ms:contentKeyID: 49290653
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中設定撥出電話的語音路由

 

_**上次修改主題的時間：** 2012-11-01_

Lync Server 2013 語音路由會將目的地電話號碼與一個或多個公用交換電話網路 (PSTN) 閘道或 SIP 主幹，以及一個或多個 PSTN 使用方式記錄產生關聯。

**若要使用 Lync Server 控制台 檢視語音路由**

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  按一下 **\[語音路由\]** 。

3.  按一下 \[路由\] 。

4.  從語音路由清單中按兩下語音路由，即可檢視其他屬性，或選取路由，按一下 **\[編輯\]** ，然後按一下 **\[顯示詳細資料\]** 。
    
    > [!NOTE]  
    > 每次僅可檢視單一路由的詳細資訊。
    


**若要使用 Windows PowerShell 檢視語音路由**

  - 啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。 可使用 Windows PowerShell 及 **Get-CsVoiceRoute** Cmdlet 來檢視語音路由。可從 Lync Server 2013 管理命令介面 或從 Windows PowerShell 的遠端工作階段來執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。
    
    如要檢視所有語音路由的資訊，在 Lync Server 管理命令介面中輸入下列命令，然後按 ENTER 鍵：
    
        Get-CsVoiceRoute
    
    這樣將傳回類似下列的資訊：
    
        Identity          : global
        Priority          : -1
        Description       :
        NumberPattern     : ^(\+1[0-9]{10})$
        PstnUsages        : {}
        PstnGatewayList   : {}
        Name              : global
        SuppressCallerId  :
        AlternateCallerId :

> [!NOTE]  
> 如需詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-voice-routes.md">Lync Server 2013 中的語音路由</a>＞。



## 本章節內容

  - [在 Lync Server 2013 中建立語音路由](lync-server-2013-create-a-voice-route.md)

  - [在 Lync Server 2013 中修改語音路由](lync-server-2013-modify-a-voice-route.md)

## 請參閱

#### 其他資源

[在 Lync Server 2013 中管理語音路由](lync-server-2013-managing-voice-routing.md)

