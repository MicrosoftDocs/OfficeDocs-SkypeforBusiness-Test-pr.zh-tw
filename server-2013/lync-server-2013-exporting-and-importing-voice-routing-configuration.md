---
title: Lync Server 2013：匯出和匯入語音路由組態
TOCTitle: 匯出和匯入語音路由組態
ms:assetid: c9b78622-5725-43b0-9ee1-5b82b1e1c8eb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398836(v=OCS.15)
ms:contentKeyID: 49292296
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中匯出和匯入語音路由組態

 

_**上次修改主題的時間：** 2012-11-01_

如果您想要儲存語音路由設定但不要發佈該設定，請依照這些步驟，使用 Lync Server 控制台設定匯出和匯入命令來儲存並擷取語音路由設定的快照。當您匯入語音路由設定檔 (.vcfg) 時，如果伺服器上的語音路由設定同時有所變更，則 Lync Server 控制台中 \[語音路由\] 群組內的頁面上，會指出語音路由有未認可的變更。這些未認可的變更是指這兩個設定間需要協調的差異處。

> [!IMPORTANT]  
> 如果您在 [語音路由] 群組中的任何頁面上對設定進行了未認可的變更，這些變更會儲存在匯出的語音設定檔 (.vcfg) 中。這可讓您在發佈變更之前，在多個 Lync Server 控制台工作階段進行期間執行語音路由設定變更。



## 本章節內容

  - [在 Lync Server 2013 中匯出語音路由組態檔](lync-server-2013-export-a-voice-route-configuration-file.md)

  - [在 Lync Server 2013 中匯入語音路由組態檔](lync-server-2013-import-a-voice-route-configuration-file.md)

## 相關各節

