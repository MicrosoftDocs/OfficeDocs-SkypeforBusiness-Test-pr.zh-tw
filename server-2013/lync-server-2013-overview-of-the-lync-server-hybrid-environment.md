---
title: Lync Server 2013：Lync Server 混合式環境概觀
TOCTitle: Lync Server 2013 混合式環境概觀
ms:assetid: 0d16ec3a-28f0-4483-96e7-8e68f30398fa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204669(v=OCS.15)
ms:contentKeyID: 49290073
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 混合式環境概觀

 

_**上次修改主題的時間：** 2014-05-28_

Lync Server 2013 混合環境指的是部署中部分使用者位於內部部署的 Lync Server 2013，其他使用者則位於 Lync Online，但使用者皆共用相同的網域，例如 user@contoso.com。

## 關於本指南

本指南將說明設定 Lync Server 2013 環境以與 Lync Online 互通，然後將使用者從內部部署移至 Lync Online 所需進行的工作。

## 先決條件

您將需要安裝下列應用程式與公用程式，才能完成設定混合部署的工作。這些檔案的安裝程式隨附於針對部署所提供的安裝媒體上，以及下列清單中所包含的連結。

  - [Active Directory Federation Services (AD FS) 2.0](http://go.microsoft.com/fwlink/p/?linkid=257305)

  - [Microsoft 目錄同步作業工具 9.1](http://go.microsoft.com/fwlink/p/?linkid=257307) (英文)

  - [安裝 Windows PowerShell 以使用 AD FS 進行單一登入](http://go.microsoft.com/fwlink/p/?linkid=398710)

  - Microsoft Online Services 登入小幫手 (msoidcli-7.0.msi) 隨附於 Office 365 桌面設定中，可透過 Office 365 管理入口網站連結的「下載」頁面取得。

## 系統管理員認證

當系統要求您提供系統管理員認證時，請使用您 Office 365 租用戶之系統管理員帳戶的使用者名稱和密碼。在設定 Active Directory Federation Services (AD FS) 2.0、目錄同步處理、單一登入、同盟，以及將使用者移至 Lync Online 時，也會使用這些認證。

## 連線到 Lync Online PowerShell

系統管理員現在能夠使用 Windows PowerShell 管理 Lync Online 與其 Lync Online 使用者帳戶。若要執行此操作，您必須先從 Microsoft 下載中心 (http://go.microsoft.com/fwlink/?LinkId=294688) 下載並安裝 Lync Online 連接器模組。如需下載、安裝及使用 Lync Online 連接器模組的詳細資訊，以及使用 Windows PowerShell 管理 Lync Online 的詳細資訊，請參閱 [使用 Windows PowerShell 管理 Lync Online](skype-for-business-online-using-windows-powershell-to-manage-your-tenant.md)。

