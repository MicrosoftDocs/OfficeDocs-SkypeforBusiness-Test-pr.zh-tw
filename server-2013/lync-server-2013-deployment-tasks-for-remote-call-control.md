---
title: Lync Server 2013：遠端呼叫控制的部署工作
TOCTitle: 遠端呼叫控制的部署工作
ms:assetid: 20218871-4f27-4611-9b7e-c0ca55908284
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558624(v=OCS.15)
ms:contentKeyID: 49290304
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中遠端呼叫控制的部署工作

 

_**上次修改主題的時間：** 2012-10-05_

本主題說明為了啟用 Lync Server 環境中使用者的遠端呼叫控制，必須執行的部署工作。

> [!NOTE]
> 如果您移轉的是先前在 Microsoft Office Communicator 2007 R2 中有啟用遠端呼叫控制的使用者，則必須先執行一個額外的部署工作，才能開始執行本主題所述的遠端呼叫控制部署工作。在移轉至 Lync Server 的過程中，必須視需要使用 Office Communications Server 2007 R2 系統管理工具，移除信任的應用程式項目 (舊稱為「授權主機項目」 )。<br />
> 如需移除授權主機的詳細資訊，請參閱＜ <a href="lync-server-2013-remove-a-legacy-authorized-host-optional.md">在 Lync Server 2013 中移除舊版授權主機 (選用)</a>＞。


## 步驟 1：安裝並設定 SIP/CSTA 閘道，以便與 PBX 通訊

您必須至少安裝一個 SIP/CSTA 閘道，以便連接至環境中的 Lync Server 以及現有專用交換機 (PBX)，才能提供遠端呼叫控制功能給使用者。SIP/CSTA 閘道是 SIP 和電腦支援的電信應用程式 (CSTA) 間的閘道。無論您安裝了幾個閘道，都只能設定一個閘道或 PBX 給每位使用者。如果現有的 PBX 不含 SIP/CSTA 介面，請務必部署可以支援 PBX 的 SIP/CSTA 閘道，包括可以支援特定 PBX 廠商的專利訊號通訊協定。如需功能詳細資訊，請直接洽詢各廠商。

當您準備部署可和 Lync Server 整合以提供遠端呼叫控制的 SIP/CSTA 閘道時，請同時洽詢閘道廠商或參閱廠商的閘道文件，了解關於下列資訊的閘道語法：

  - 閘道的線路伺服器 URI

  - 將指派給閘道之使用者的線路 URI

設定使用者組態時需指定上述設定，閘道才能正確路由傳送並連接至 PBX。

關於廠商，您可以參考 Microsoft 整合通訊 Open Interoperability Program 網站： [http://go.microsoft.com/fwlink/?linkid=203309\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=203309%26clcid=0x404)。

## 步驟 2：設定 Lync Server 將 CSTA 要求路由傳送到 SIP/CSTA 閘道

您必須針對部署中要用來路由傳送遠端呼叫控制要求的所有 SIP/CSTA 閘道，在 Lync Server 集區中建立目的地位址 (伺服器 URI) 的靜態路由。您也必須建立信任的應用程式項目，用來對應每個目的地位址。將閘道指定為信任的應用程式後，即使該閘道是由協力廠商開發，也會給予信任狀態，讓其作為 Lync Server 環境的一部分執行 (且因為不是產品內建服務，所以會以 *外部服務* 的形式執行)。最後，如果 Lync Server 使用傳輸控制通訊協定 (TCP) 連線來連接 SIP/CSTA 閘道，而非使用傳輸層安全性 (TLS) 連線，您還必須使用 拓撲產生器定義閘道 IP 位址。

如需設定靜態路由的詳細資訊，請參閱＜ [在 Lync Server 2013 中設定遠端呼叫控制的靜態路由](lync-server-2013-configure-a-static-route-for-remote-call-control.md)＞。

如需設定信任的應用程式項目的詳細資訊，請參閱＜ [在 Lync Server 2013 中為遠端呼叫控制設定信任的應用程式項目](lync-server-2013-configure-a-trusted-application-entry-for-remote-call-control.md)＞。

如需在 拓撲產生器中定義 SIP/CSTA 閘道 IP 位址的詳細資訊，請參閱＜ [在 Lync Server 2013 中定義 SIP/CSTA 閘道 IP 位址](lync-server-2013-define-a-sip-csta-gateway-ip-address.md)＞。

## 步驟 3：為 Lync 使用者設定遠端呼叫控制

在 Lync Server 中啟用使用者後，接著可以使用 Lync Server 控制台或 Lync Server 管理命令介面為使用者啟用遠端呼叫控制。在這個部署步驟中，您需指派線路伺服器 URI 和線路 URI 給每位使用者。線路伺服器 URI 是您計畫指派給使用者之 SIP/CSTA 閘道的 SIP URI。線路 URI 則是要指派給使用者的唯一電話號碼。

如需為遠端呼叫控制設定使用者的詳細資訊，請參閱＜ [在 Lync Server 2013 中允許 Lync 使用者進行遠端呼叫控制](lync-server-2013-enable-lync-users-for-remote-call-control.md)＞。

## 步驟 4：定義 Lync Server 電話號碼正規化規則

在遠端呼叫控制案例中， Lync Server 使用電話號碼正規化規則，將從 SIP/CSTA 閘道收到的電話號碼轉換成 E.164 格式。電話號碼必須是標準化格式，某些遠端呼叫控制功能才能正確運作。遠端呼叫控制採用您為通訊錄服務電話號碼正規化所設定的電話號碼正規化規則，此規則與 Enterprise Voice 的電話號碼正規化規則不同。

如需遠端呼叫控制如何使用電話號碼正規化規則的詳細資訊，請參閱＜ [Lync Server 2013 中的遠端呼叫控制和電話號碼正規化](lync-server-2013-remote-call-control-and-phone-number-normalization.md)＞。如需通訊錄服務之電話號碼正規化規則的詳細資訊，請參閱作業文件中的＜ [在 Lync Server 2013 中管理通訊錄服務](lync-server-2013-administering-the-address-book-service.md)＞主題。

