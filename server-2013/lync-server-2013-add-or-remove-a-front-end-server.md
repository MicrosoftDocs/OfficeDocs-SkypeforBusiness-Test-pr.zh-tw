---
title: 在 Lync Server 2013 中新增或移除前端伺服器
TOCTitle: 在 Lync Server 2013 中新增或移除前端伺服器
ms:assetid: ab748733-6bad-4c93-8dda-db8d5271653d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205153(v=OCS.15)
ms:contentKeyID: 49291983
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中新增或移除前端伺服器

 

_**上次修改主題的時間：** 2013-11-19_

當您將前端伺服器新增到集區中或從集區移除前端伺服器時，您必須重新啟動集區。若要防止使用者發生服務中斷，請使用下列程序來新增或移除前端伺服器。

## 新增或移除前端伺服器

1.  若要移除任何前端伺服器，請先停止這些伺服器的新連線。若要這樣做，您可使用下列 Cmdlet：
    
        Stop -CsWindowsServices -Graceful

2.  當正在移除的伺服器沒有目前的工作階段時，停止這些伺服器上的 Lync Server 服務。

3.  開啟拓撲產生器，然後新增或移除必要的伺服器。

4.  發行拓撲。

5.  如果集區從擁有兩個前端伺服器變成兩個以上，或從擁有兩台以上的伺服器變成實際上兩台，則您需要輸入下列 Cmdlet：
    
        Reset-CsPoolRegistrarState-ResetType FullReset -PoolFqdn <PoolFqdn>
    
    如果集區擁有 3 台以上的伺服器，當您輸入此 Cmdlet 時，必須至少執行 3 台伺服器。

6.  重新啟動集區中的所有前端伺服器，一次一個。

