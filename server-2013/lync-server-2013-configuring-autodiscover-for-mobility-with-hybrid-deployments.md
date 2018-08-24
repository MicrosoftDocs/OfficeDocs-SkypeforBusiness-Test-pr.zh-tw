---
title: Lync Server 2013：利用混合部署針對行動性設定自動探索
TOCTitle: 利用混合部署針對行動性設定自動探索
ms:assetid: f838af79-d8b4-4122-b81c-7889573d143e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ215885(v=OCS.15)
ms:contentKeyID: 49292860
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中利用混合部署針對行動性設定自動探索

 

_**上次修改主題的時間：** 2014-06-18_

「混合式部署」是同時使用 Microsoft Lync Online 雲端服務與內部部署的組態。在這種類型的組態中，「自動探索」服務必須能找出使用者所在的實際位置。亦即「自動探索」會協助尋找使用者帳戶，以及代管使用者帳戶的伺服器位置，無論是在內部部署或 商務用 Skype Online 部署中。

例如，如果使用者帳戶是由 商務用 Skype Online 中的伺服器代管，則嘗試尋找使用者位置且稱為 *可測知性* 的過程如下：

  - 使用者會嘗試建立與內部部署 **contoso.com** 的連線。

  - 系統會將此嘗試傳送至 lyncdiscover.contoso.com，這是與「自動探索」服務相關聯的 DNS 名稱。

  - 「自動探索」會參照 contoso.com 內部部署中假設的登錄器集區，並且會得到使用者受 商務用 Skype Online 代管的實際主要伺服器資訊。然後「自動探索」會將使用者轉介至 **lync.com** 線上「自動探索」服務。

  - 使用者會嘗試建立與 lync.com 線上「自動探索」服務的連線，且能找出使用者的帳戶與主伺服器。

若要啟用行動用戶端以探索主伺服器所在的部署，您必須以新統一資源定位器 (URL) 設定「自動探索」服務。請執行下列步驟以設定「自動探索」服務。

## 設定混合部署的自動探索

1.  您使用 Get-CsHostingProvider 擷取屬性 ProxyFQDN 的值。

2.  在 Lync Server 管理命令介面中輸入：
    
        Set-CsHostingProvider -Identity [identity] -AutodiscoverUrl https://webdir.online.lync.com/autodiscover/autodiscoverservice.svc/root
    
    其中 \[identity\] 可以共用 SIP 位址空間的網域名稱取代。 space.

## 請參閱

#### 其他資源

[Get-CsHostingProvider](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsHostingProvider)  
[Set-CsHostingProvider](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsHostingProvider)

