---
title: Lync Server 2013：整合式 Unified Messaging 的功能
TOCTitle: 整合式 Unified Messaging 和 Lync Server 的功能
ms:assetid: 094f549d-fccc-43ab-9f39-6ddd18130915
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398144(v=OCS.15)
ms:contentKeyID: 49290024
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 整合式 Unified Messaging 和 Lync Server 2013 的功能

 

_**上次修改主題的時間：** 2012-10-01_

Lync Server 2013、 企業語音使用 Exchange 整合通訊 (UM) 基礎結構來提供來電接聽、來電通知、語音存取 (包含語音信箱) 和自動語音應答服務。

## 來電接聽

當使用者的電話沒人接聽或是忙線中，來電接聽功能就會代表使用者接收語音訊息。其中包括播放個人的問候語、記錄訊息，以及送出訊息，以排入佇列傳送到使用者的信箱 (信箱會儲存在 Exchange 信箱伺服器上)。

如果來電者留下訊息，該訊息就會傳送到使用者的收件匣。如果來電者選擇不留下任何訊息，則會在使用者的信箱中儲存未接來電通知。然後使用者可以使用 Microsoft Outlook 訊息和共同作業用戶端、Outlook Web Access、Exchange ActiveSync 技術或 Outlook Voice Access 存取自己的收件匣。可以使用與電子郵件類似的方式來顯示來電的主旨和優先順序。

## Outlook Voice Access

Outlook Voice Access 不只可讓 企業語音使用者從電話語音介面存取語音信箱，還可以存取 Exchange 收件匣，其中包括電子郵件、行事曆和連絡人。訂戶存取號碼是由 Exchange UM 系統管理員所指派。

## 自動語音應答

自動語音應答是一項 Exchange UM 功能，它可用來設定一個電話號碼，讓外面的使用者可以撥打此號碼來聯繫公司的代表人員。特別是，它提供了一系列的語音提示，可協助外部來電者瀏覽功能表系統。可用選項的清單是由 Exchange UM 系統管理員在 Exchange UM 伺服器上設定。

## 傳真服務

Exchange UM 包含傳真功能，可讓使用者在 Exchange 信箱中接收傳入的傳真。如需詳細資訊，請參閱 Microsoft Exchange Server 文件中的＜整合通訊＞，網址為 [http://go.microsoft.com/fwlink/?linkid=135652\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=135652%26clcid=0x404)。

> [!NOTE]  
> Exchange UM 伺服器所提供的傳真服務無法用在與 Microsoft Exchange Server 2010、 Exchange 2010 (含最新 Service Pack) 或 Exchange 2013 整合的 Lync Server 部署中。


