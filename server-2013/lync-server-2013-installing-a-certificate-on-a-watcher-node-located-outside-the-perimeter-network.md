---
title: 將憑證安裝在位於周邊網路外的監看員節點上
TOCTitle: 將憑證安裝在位於周邊網路外的監看員節點上
ms:assetid: 825c9c02-1951-4d7a-a25e-a313a85333f8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688113(v=OCS.15)
ms:contentKeyID: 49890145
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將憑證安裝在位於周邊網路外的監看員節點上

 

_**上次修改主題的時間：** 2012-10-22_

周邊網路中執行 (例如 Lync Server Edge Server)、企業外部 (例如外部綜合異動監控程式節點) 或 Active Directory 網域服務 信任界限上的 System Center Operations Manager 代理程式可能需要 System Center Operations Manager Gateway Server 的組態。這個伺服器角色可讓與 Root Management Server 沒有任何信任關係的代理程式發出通知。如需詳細資訊，請參閱 System Center Operations Manager TechNet Library 中的「在 Operations Manager 2007 中管理閘道伺服器」(網址為：[http://go.microsoft.com/fwlink/?linkid=268703\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268703%26clcid=0x404))。

如果在這些位置當中部署代理程式，您也需要要求和設定憑證，讓監控程式節點將通知傳送到 System Center Operations Manager。為了簡化這個程序，Operations Manager 團隊已建立一套公用程式，讓您要求正確類型的憑證，並安裝於監控程式節點電腦上。如需詳細資訊，並下載這些公用程式，請參閱「使用憑證產生精靈輕鬆取得未加入網域之代理程式的憑證」部落格文章 (網址為：[http://go.microsoft.com/fwlink/?linkid=267421\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=267421%26clcid=0x404))。

