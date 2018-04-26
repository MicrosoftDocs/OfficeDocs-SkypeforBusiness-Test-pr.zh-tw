---
title: Lync Server 2013：媒體旁路和中繼伺服器
TOCTitle: 媒體旁路和中繼伺服器
ms:assetid: 8ed35f95-05cd-4b5d-8470-442d2323df71
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398719(v=OCS.15)
ms:contentKeyID: 49291635
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的媒體旁路和中繼伺服器

 

_**上次修改主題的時間：** 2012-09-21_

媒體旁路是一項 Lync Server 功能，它能讓系統管理員將通話路由設定為直接在使用者端點和公用交換電話網路 (PSTN) 閘道間流動，而不需要周遊 中繼伺服器。媒體旁路能減少延遲時間、不必要的轉譯、封包遺失率及可能的失敗點數，進而提升通話品質。當不具有 中繼伺服器的遠端網站透過一個或多個啟用頻寬限制的 WAN 連結與中央網站連接時，媒體旁路能讓遠端網站之用戶端的媒體直接流向本地閘道，而不需要先經由 WAN 連結流向中央網站的 中繼伺服器後再返回，藉此降低頻寬需求。減輕的媒體處理負載亦能補足 中繼伺服器控制多個閘道的能力。

媒體旁路和通話許可控制 (CAC) 是彼此互斥的功能。如果您為通話採用媒體旁路，便無法為該通話執行 CAC (假設通話未涉及具有頻寬限制的連結)。

## 請參閱

#### 概念

[Lync Server 2013 中的通話許可控制和中繼伺服器](lync-server-2013-call-admission-control-and-mediation-server.md)  

#### 其他資源

[在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)

