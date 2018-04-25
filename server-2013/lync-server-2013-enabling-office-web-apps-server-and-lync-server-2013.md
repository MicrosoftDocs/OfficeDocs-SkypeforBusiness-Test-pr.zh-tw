---
title: Lync Server 2013：啟用 Office Web Apps Server 與 Lync Server 2013
TOCTitle: 啟用 Office Web Apps Server 與 Lync Server 2013
ms:assetid: 3370ab55-9949-4f32-b88b-5cffed6aaad8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204792(v=OCS.15)
ms:contentKeyID: 49290534
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 Office Web Apps Server 與 Lync Server 2013 的整合

 

_**上次修改主題的時間：** 2014-02-05_

Lync Server 2013 會運用 Office Web Apps Server 來處理 PowerPoint 簡報。如需有關此方法的優點之資訊，請參閱＜ [Lync Server 2013 中的 Web 會議概觀](lync-server-2013-web-conferencing-overview.md)＞。

為了使用這些新功能，系統管理員必須安裝 Office Web Apps Server，也必須設定 Lync Server 2013 才能與 Office Web Apps Server 進行通訊。本文件提供有關如何設定 Lync Server 2013 以搭配 Office Web Apps Server 運作的相關資訊。本文件並未提供有關如何安裝 Office Web Apps Server 本身的資訊；如需詳細資訊，請參閱 Microsoft Office Web Apps 部署網站，網址為： [http://go.microsoft.com/fwlink/?linkid=257525\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=257525%26clcid=0x404)。該指南包含有關 Office Web Apps Server 的完整必要資訊；請注意， Office Web Apps Server 應安裝在未執行 Lync Server、Microsoft SQL Server 或任何其他伺服器應用程式的獨立電腦上 (也不得在該電腦上安裝任何版本的 Microsoft Office)。用於執行 Office Web Apps Server 的任何電腦也必須安裝指定的軟體組合 (包括 .NET Framework 4.5 與 Windows PowerShell 3.0)；這些要求與有關設定憑證和 Internet Information Services (IIS) 的資訊，都會在 Microsoft Office Web Apps 部署網站中詳細討論，網址為： [http://go.microsoft.com/fwlink/?linkid=257525\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=257525%26clcid=0x404)。

本文件涵蓋下列主題領域：

  - [設定 Lync Server 2013 與 Office Web Apps Server 搭配使用](lync-server-2013-configuring-lync-server-2013-to-work-with-office-web-apps-server.md)

  - [在 Lync Server 2013 中使用反向 Proxy 伺服器發佈 Office Web Apps Server](lync-server-2013-publishing-office-web-apps-server-using-a-reverse-proxy-server.md)

  - [驗證 Office Web Apps Server 的設定](lync-server-2013-validating-the-configuration-of-office-web-apps-server.md)

  - [設定用戶端與 Office Web Apps Server 搭配使用](lync-server-2013-configuring-clients-for-use-with-office-web-apps-server.md)

