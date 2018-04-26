---
title: Lync Server 2013：周邊網路 VoIP 元件
TOCTitle: 周邊網路 VoIP 元件
ms:assetid: 74230008-695d-436a-90b9-9cd060c70f7b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398559(v=OCS.15)
ms:contentKeyID: 49291312
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的周邊網路 VoIP 元件

 

_**上次修改主題的時間：** 2012-09-21_

使用整合通訊用戶端進行個別或會議通話的外部來電者，會依賴 Edge Server 來與同事進行語音通訊。

在 Edge Server 上，Access Edge Service 會為來自組織防火牆之外的 Lync 使用者通話提供 SIP 訊號。A/V Edge Service 可以讓媒體周遊 NAT 和防火牆。從公司防火牆外使用整合通訊 (UC) 用戶端的來電者，會依賴 A/V Edge Service 來進行個別通話和電話會議。

A/V 驗證服務會和 A/V Edge Service 配置在一起，並為後者提供驗證服務。嘗試連接至 A/V Edge Service 的外部使用者，需要 A/V 驗證服務提供的驗證 Token 才能接通電話。

