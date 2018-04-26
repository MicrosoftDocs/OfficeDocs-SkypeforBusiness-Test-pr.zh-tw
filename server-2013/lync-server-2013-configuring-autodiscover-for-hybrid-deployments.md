---
title: 設定混合部署的自動探索
TOCTitle: 設定混合部署的自動探索
ms:assetid: ca605e62-181c-42ca-80a1-e37e610f8277
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945653(v=OCS.15)
ms:contentKeyID: 52056208
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定混合部署的自動探索

 

_**上次修改主題的時間：** 2012-12-12_

「混合式部署」是同時使用 Microsoft Lync Online 雲端服務與內部部署的組態。在這種類型的組態中，「自動探索」服務必須能找出使用者所在的實際位置。亦即「自動探索」會協助尋找使用者帳戶，以及代管使用者帳戶的伺服器位置，無論是在內部部署或 商務用 Skype Online 部署中。

例如，如果使用者帳戶是由 商務用 Skype Online 中的伺服器代管，則嘗試尋找使用者位置的過程 (稱為「可測知性」)：

  - 使用者會嘗試建立與內部部署 **contoso.com** 的連線。

  - 系統會將此嘗試傳送至 lyncdiscover.contoso.com，這是與「自動探索」服務相關聯的 DNS 名稱。

  - 「自動探索」會參照 contoso.com 內部部署中假設的登錄器集區，並且會得到 商務用 Skype Online 所代管之使用者的實際主伺服器資訊。然後「自動探索」會將使用者轉介至 **lync.com** 線上「自動探索」服務。

  - 使用者會嘗試啟動與 lync.com 線上「自動探索」服務的連線，且能找出使用者的帳戶與主伺服器。

若要啟用用戶端以探索主伺服器所在的部署，您必須以新統一資源定位器 (URL) 設定「自動探索」服務。請執行下列步驟以設定「自動探索」服務。

## 設定混合部署的自動探索

1.  在[Lync Server 2013 的自動探索服務需求](lync-server-2013-autodiscover-service-requirements.md)主題中，您可使用 Get-CsHostingProvider 擷取 ProxyFQDN 屬性值。

2.  從 Lync Server 管理命令介面，輸入
    
        Set-CsHostingProvider -Identity [identity] -AutodiscoverUrl https://webdir.online.lync.com/autodiscover/autodisccoverservice.svc/root
    
    其中 \[identity\] 請替換為共用 SIP 位址空間的網域名稱。

## 請參閱

#### 其他資源

[Get-CsHostingProvider](get-cshostingprovider.md)  
[Set-CsHostingProvider](set-cshostingprovider.md)

