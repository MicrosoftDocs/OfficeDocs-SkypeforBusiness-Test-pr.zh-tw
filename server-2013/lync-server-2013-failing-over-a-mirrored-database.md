---
title: Lync Server 2013：容錯移轉鏡像資料庫
TOCTitle: 容錯移轉鏡像資料庫
ms:assetid: 70185476-e3d4-440a-9316-fa24b226343e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204991(v=OCS.15)
ms:contentKeyID: 49291268
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中容錯移轉鏡像資料庫

 

_**上次修改主題的時間：** 2014-03-14_

若您已設定後端資料庫以使用具有見證的同步鏡像，將自動進行容錯移轉。若您已經設定不具見證的同步鏡像，則可以使用以下程序，針對資料庫進行容錯移轉與容錯回復。即使您已經設定見證，也可以使用這些程序對資料庫進行手動容錯移轉與容錯回復。

## 針對您的後端資料庫進行容錯移轉

1.  進行容錯移轉前，請鍵入下列 Cmdlet，以決定後端資料庫何者為主體以及何者為鏡像：
    
        Get-CsDatabaseMirrorState -PoolFqdn <poolFQDN> -DatabaseType User

2.  如果此集區裝載 中央管理存放區，請鍵入下列 Cmdlet，決定何者為 中央管理存放區主體以及何者為鏡像：
    
        Get-CsDatabaseMirrorState -PoolFqdn <poolFQDN> -DatabaseType CentralMgmt

3.  執行使用者資料庫容錯移轉：
    
      - 如果主要作業失敗，而您正在進行鏡像容錯移轉，請鍵入：
        
            Invoke-CsDatabaseFailover -PoolFqdn <poolFQDN> -DatabaseType User -NewPrincipal mirror -Verbose
    
      - 如果鏡像失敗而您正在進行主要作業的容錯移轉，請鍵入：
        
            Invoke-CsDatabaseFailover -PoolFqdn <poolFQDN> -DatabaseType User -NewPrincipal primary -Verbose

4.  如果該集區裝載 中央管理伺服器，請執行 中央管理存放區容錯移轉。
    
      - 如果主要作業失敗，而您正在進行鏡像容錯移轉，請鍵入：
        
            Invoke-CsDatabaseFailover -PoolFqdn <poolFQDN> -DatabaseType CentralMgmt -NewPrincipal mirror -Verbose
    
      - 如果鏡像失敗而您正在進行主要作業的容錯移轉，請鍵入：
        
            Invoke-CsDatabaseFailover -PoolFqdn <poolFQDN> -DatabaseType CentralMgmt -NewPrincipal primary -Verbose

