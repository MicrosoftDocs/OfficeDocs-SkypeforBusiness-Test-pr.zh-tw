---
title: Lync Server 2013：增強及保護伺服器和應用程式
TOCTitle: 增強及保護 Lync Server 2013 的伺服器和應用程式
ms:assetid: 9ca2b233-26f1-4d72-96e7-81a82c727806
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn518331(v=OCS.15)
ms:contentKeyID: 60471184
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 增強及保護 Lync Server 2013 的伺服器和應用程式

 

_**上次修改主題的時間：** 2013-12-05_

您應根據該特定元件的最佳作法來增強並保護作業系統和應用程式。本節說明如何增強應用程式伺服器，並使用群組原則來實作安全性鎖定。

> [!NOTE]  
> 您也可以增強並保護用於 Microsoft Lync Server 2013 部署的資料庫。如需詳細資訊，請參閱<a href="lync-server-2013-hardening-and-protecting-databases.md">增強及保護 Lync Server 2013 的資料庫</a>。



## 保障應用程式伺服器的安全

若是應用程式伺服器，則應增強作業系統和應用程式。例如，專門用來執行 Microsoft Internet Security and Acceleration (ISA) Server 2006 的 Windows Server 2008 電腦應在作業系統和應用程式方面加以增強。首要目標應該是盡量減少執行的服務數量，以及伺服器提供的服務數量。

## 保障虛擬伺服器的安全

虛擬伺服器快照中包含了伺服器資料磁碟的複本，以及記憶體內部資料的傾印，這兩者皆可能含有機密的密碼編譯資料，可能會引來攻擊。針對以虛擬化實作的生產伺服器，應停用所有伺服器快照或嚴密地管理伺服器快照。如需保護 Hyper-V 虛擬伺服器安全性的詳細資訊，請參閱 Hyper-V 安全性指南，網址為：[http://go.microsoft.com/fwlink/p/?LinkId=214176](http://go.microsoft.com/fwlink/p/?linkid=214176)。

## 群組原則

在 Windows Server 2008 和 Windows Server 2008 R2 中，群組原則提供目錄式的桌面設定管理。您可以透過在下列各項的群組原則物件 (GPO) 內定義 \[電腦及使用者\] 設定，使用群組原則來實作安全性鎖定：

  - 登錄型原則

  - 安全性

  - 軟體安裝

  - 指令碼

  - 資料夾重新導向

  - 遠端安裝服務

為提供使用者介面讓系統管理員進行這些設定，作業系統、Service Pack 和部分應用程式 (包括 Lync Server 2013) 發行時都會隨附系統管理範本。

Communicator.adm 檔案是一個隨附於 Lync Server 2013 的系統管理範本，安裝在 *%windir%*\\inf\\ 目錄下，並且提供一個群組原則設定介面。Communicator.adm 中的每一項設定都對應到登錄中會影響應用程式行為的設定。

這些設定可以從 GPedit.dll 存取，該檔案可在 Active Directory \[使用者和電腦\] 主控台以及群組原則管理主控台 (GPMC) 中找到。

## 群組原則安全性設定

群組原則中包含了從 GPedit.dll 存取 GPO 時 (位於電腦設定/Windows 設定/安全性設定) 的安全性設定。您可以匯入安全性範本來設定 GPO 的安全性設定。＜Windows Server 2008 安全性指南＞(英文，位於 [http://go.microsoft.com/fwlink/p/?LinkId=145186](http://go.microsoft.com/fwlink/p/?linkid=145186)) 和 Windows Server 2008 R2 安全性規範管理工具組 (英文，位於 [http://go.microsoft.com/fwlink/p/?LinkId=211882](http://go.microsoft.com/fwlink/p/?linkid=211882)) 中包含了一些範例範本，您可以根據需要求修改。

## 最佳作法

  - 增強所有伺服器的作業系統和應用程式。

  - 保護伺服器快照並強化所有虛擬伺服器的安全性。

  - 使用群組原則實作安全性鎖定。

