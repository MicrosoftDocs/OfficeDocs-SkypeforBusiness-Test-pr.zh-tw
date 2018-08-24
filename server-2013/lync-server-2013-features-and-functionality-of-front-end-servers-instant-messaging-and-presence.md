---
title: Lync Server 2013：前端伺服器、立即訊息及顯示狀態的功能
TOCTitle: 前端伺服器、立即訊息及顯示狀態的功能
ms:assetid: 05b29536-dcd7-49b5-934a-2ebf20ddc45c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398109(v=OCS.15)
ms:contentKeyID: 49289963
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的前端伺服器、立即訊息及顯示狀態的功能

 

_**上次修改主題的時間：** 2013-03-17_

前端伺服器提供大多數 Lync Server 功能。目前提供兩種版本： Lync Server Enterprise Edition，主要針對大型組織所設計； Lync Server Standard Edition，主要針對需要較少硬體投資且不需要高可用性的小型組織所設計。這兩種版本均支援所有 Lync Server 工作量，包括 IM、目前狀態、會議及 Enterprise Voice。

立即訊息 (IM) 可讓使用者在電腦上使用文字訊息，與其他使用者進行即時溝通。同時支援雙方或多方 IM 工作階段。雙方 IM 交談中的參與者可以隨時將第三個參與者加入交談中。若發生這種情況，\[交談\] 視窗會變更成可支援會議功能。

> [!IMPORTANT]  
> Lync 和 Communicator 用戶端在用於一對一通訊時，通常稱為對等通訊。技術上而言，兩個用戶端是在一對一的交談中進行通訊，以立即訊息多點控制設備 (IMMCU) 做為中介。IMMCU 是 前端伺服器 的元件。將 IMMCU 置於所需的通訊工作流程，可讓詳細通話記錄及 前端伺服器 啟用的其他功能得以使用。通訊是從用戶端上的動態來源連接埠，通向 前端伺服器 連接埠 TLS/TCP/5061 (假設使用建議的傳輸層安全性)。依照預設，對等通訊 (以及多方 IM) 只有在 Lync Server 和 IMMCU 啟用且可以使用的狀態下才能進行。



「目前狀態」 可為使用者提供網路上其他使用者的狀態資訊。使用者的目前狀態所提供的資訊有助於其他人決定是否應嘗試連絡該名使用者，以及是否要使用立即訊息、電話或電子郵件。目前狀態會促進立即通訊，但也會提供使用者正在開會中或不在辦公室的資訊，指出無法進行立即通訊。在 Lync 和其他可識別目前狀態的應用程式 (包括 Outlook 訊息和共同作業用戶端、Microsoft SharePoint 技術、Microsoft Word 和 Microsoft Excel 試算表軟體) 中，此目前狀態會顯示為目前狀態圖示。目前狀態圖示表示使用者目前是否有空，以及通訊意願。

