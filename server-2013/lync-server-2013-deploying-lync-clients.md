---
title: 在 Lync Server 2013 中部署 Lync 用戶端
TOCTitle: 在 Lync Server 2013 中部署 Lync 用戶端
ms:assetid: 3d10abf2-d484-4fa0-8f10-4a5f9dfba4f5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204827(v=OCS.15)
ms:contentKeyID: 49290666
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中部署 Lync 用戶端

 

_**上次修改主題的時間：** 2012-10-03_

Lync 2013 推出了不同的用戶端部署方式。與舊版不同的是，Lync 2013 不再有自己的安裝程式，而是在 Office 2013 安裝程式之中包含 Lync。如要部署 Lync 2013 到使用者，可使用 Office 2013 安裝方法及自訂工具。

  - **Office 2013 Windows Installer** 是以 Windows Installer 為基礎的安裝套件，包含了多個 MSI 檔案。中性語言核心 MSI 套件結合了一或多個特定語言套件，組成完整的產品。安裝程式組合了個別套件，在安裝 Office 於使用者的電腦期間 (以及之後)，執行自訂與維護工作。本節中的主題描述如何使用及自訂 Office 2013 Windows Installer 以部署 Lync 2013。

  - **Office 2013 隨選即用**是將 Office 安裝程式檔案從 Microsoft Office 365 入口網站串流至使用者的安裝程式。管理員可以使用隨選即用的 Office 部署工具來自訂安裝。因為 Office 2013 隨選即用主要是用於 Microsoft Office 365 環境，所以本節並不詳述此安裝方法。有關使用及自訂隨選即用安裝的詳細資訊提供於＜Office 2013 Resource Kit＞文件中。管理員也可以將 Office 2013 隨選即用程式與語言來源檔案下載至內部部署位置，如想要最小化對網路的需求，或者因為公司安全性需求而想要防止使用者從網際網路安裝軟體，這都是非常有用的。

本節中的主題著重於如何使用 Office 2013 以 MSI 為基礎的安裝程式來部署用戶端。您的主要參考資料應為＜Office 2013 Resource Kit＞文件，其中詳細描述如何準備基礎結構、自訂安裝程式，以及部署 Office 2013。不過您應該在使用 Office 文件時搭配本節中的主題，因為本節針對 Lync 2013 指出部署的考量。

> [!Note]  
> <ul>
> <li><p>Lync 2013 的線上會議增益集會隨著 Lync 2013 自動安裝，支援在 Outlook 訊息和共同作業用戶端內管理會議。</p></li>
> <li><p>Office 2013 安裝程式不會解除安裝舊版的 Lync 或 Office Communicator。Lync 2013 用戶端會與其他 Lync 或 Office Communicator 用戶端並存安裝。</p></li>
> </ul>


## 本節內容

  - [自訂用戶端安裝](lync-server-2013-customizing-client-installation.md)

  - [自訂 Lync 行為與使用者介面](lync-server-2013-customizing-lync-behavior-and-the-user-interface.md)

  - [在 Lync Server 2013 中自訂線上會議增益集](lync-server-2013-customizing-the-online-meeting-add-in.md)

  - [在 Lync Server 2013 中設定會議加入頁面](lync-server-2013-configuring-the-meeting-join-page.md)

  - [設定受支援的用戶端版本](lync-server-2013-configuring-supported-client-versions.md)

  - [設定增強的顯示狀態隱私權模式](lync-server-2013-configuring-enhanced-presence-privacy-mode.md)

