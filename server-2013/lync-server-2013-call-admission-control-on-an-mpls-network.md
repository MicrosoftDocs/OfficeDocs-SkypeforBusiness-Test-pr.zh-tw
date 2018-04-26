---
title: Lync Server 2013：MPLS 網路上的通話許可控制
TOCTitle: MPLS 網路上的通話許可控制
ms:assetid: 0beec6be-2431-4255-a3d2-512dd030e66a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398168(v=OCS.15)
ms:contentKeyID: 49290057
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 Lync Server 2013 在 MPLS 網路上進行通話許可控制

 

_**上次修改主題的時間：** 2012-09-22_

在多重通訊協定標籤交換 (Multiprotocol Label Switching，MPLS) 網路中，所有網站都由完整網狀 (Full-Mesh) 連線。也就是，所有網站都會直接連線至網際網路服務提供者的 MPLS 骨幹，而且每個網站都已佈建要透過 MPLS 雲端的 WAN 連結使用的頻寬。沒有網路集線器或中央網站可控制 IP 路由。下圖顯示以 MPLS 技術為基礎的簡易網路。

**MPLS 網路範例**

![使用 MPLS 的 CAC](images/Gg398168.54602e6e-ec11-4dae-936d-b01acda8a179(OCS.15).jpg "使用 MPLS 的 CAC")

若要在 MPLS 網路中部署通話許可控制 (CAC)，您可建立網路地區代表 MPLS 雲端，以及建立網路網站代表每個 MPLS 衛星網站。下圖說明如何設定網路地區和網路網站以代表上圖中的 MPLS 網路範例。整體頻寬限制和頻寬工作階段限制都是以從每個網路網站連至代表 MPLS 雲端之網路地區的 WAN 連結為基礎。

**MPLS 網路的網路地區和網路網站**

![使用 MPLS 的通話許可控制 (CAC) 圖表](images/Gg398168.f8f76283-5c0c-4133-8a78-3fbbfd016dc4(OCS.15).jpg "使用 MPLS 的通話許可控制 (CAC) 圖表")

