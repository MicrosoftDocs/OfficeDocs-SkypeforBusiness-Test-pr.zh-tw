---
title: 設定自動探索的支援
TOCTitle: 設定自動探索的支援
ms:assetid: 3a266456-69a0-4539-ba99-d388b83799a8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945622(v=OCS.15)
ms:contentKeyID: 52056089
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定自動探索的支援

 

_**上次修改主題的時間：** 2013-01-21_

Lync Server Web 服務**自動探索服務**首先出現於 Lync Server 2010 累計更新 (2011 年 11 月)。此更新是伴隨首次發行的 Lync Mobile 用戶端。自動探索服務會公開 Mobility Services，稱為 Mcx 服務。

自動探索服務是做為所有用戶端在要求有關哪些服務和功能可用，以及如何連絡服務 (透過完整網域名稱或統一資源定位器 Web 參考) 之資訊時的單一位置。自動探索會公開一些功能，且每個用戶端會根據用戶端可使用的功能做出要求。例如，桌面 Lync 2013 用戶端會使用自動探索來確定外部 Web 服務，但不會使用 Mobility Services (Mcx)。若要正確定義並啟用用戶端來使用其可用的功能，則必須定義出允許用戶端有效尋找並使用自動探索項目的案例。若要使用自動探索，部署會要求反向 Proxy 必須發行 Lync Server Web 服務， 且系統必須設定 DNS 記錄來解析對 Lync Server 自動探索服務和 Lync Server Web 服務的 DNS 查詢，還有系統也必須針對您的特定案例正確設定憑證服務。

> [!TIP]
> 如需自動探索要求/回應內元素之功能的詳細技術資訊，請參閱＜<a href="lync-server-2013-understanding-autodiscover.md">了解自動探索</a>＞。


下列資訊和表格會根據案例來定義您需要實作的設定 (如果有的話)，以提供對自動探索服務的完整且有效運用。下列主題中的資訊是針對 Microsoft Lync Server 2013。若要尋求如何規劃適用 Lync Server 2010 之 Mobility 的指示，請參閱 <http://go.microsoft.com/fwlink/?linkid=275113>。若要部署適用 Lync Server 2010 的 Mobility，請參閱 <http://go.microsoft.com/fwlink/?linkid=275114>

## 本章節內容

  - [設定自動探索的 DNS](lync-server-2013-configuring-dns-for-autodiscover.md)

  - [設定自動探索的憑證](lync-server-2013-configuring-certificates-for-autodiscover.md)

  - [設定自動探索的反向 Proxy](lync-server-2013-configuring-a-reverse-proxy-for-autodiscover.md)

  - [設定混合部署的自動探索](lync-server-2013-configuring-autodiscover-for-hybrid-deployments.md)

