---
title: 匯入原則與設定
TOCTitle: 匯入原則與設定
ms:assetid: b25decee-2ee5-4836-b370-454411d39252
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205178(v=OCS.15)
ms:contentKeyID: 49292041
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 匯入原則與設定

 

_**上次修改主題的時間：** 2012-09-28_

在將 Office Communications Server 2007 R2 拓撲資訊與 Lync Server 2013 試驗集區合併後，您必須執行 Lync Server 2013 管理命令介面 Cmdlet 以將 Office Communications Server 2007 R2 原則與組態設定移轉至 Lync Server 2013 試驗集區。

**Import-CsLegacyConfiguration** Cmdlet 可匯入原則、語音路由、撥號對應表、Communicator Web Access URL 以及 Lync Server 2013 的撥入存取號碼。

## 移轉原則與設定

1.  在 Lync Server 2013 前端伺服器上，啟動 Lync Server 管理命令介面。

2.  在命令列輸入下列命令：
    
        Import-CsLegacyConfiguration
    
    在匯入原則之後，請使用下列程序在 Lync Server 控制台中查看已匯入的原則。

## 檢視匯入的原則

1.  開啟 Lync Server 2013 控制台。

2.  按一下 \[語音路由\] ，然後檢視匯入的原則。

3.  按一下 \[會議\] ，然後檢視匯入的原則。

4.  按一下 \[同盟與外部存取\] ，然後檢視匯入的原則。

5.  按一下 \[監控和封存\] ，然後檢視匯入的原則。

