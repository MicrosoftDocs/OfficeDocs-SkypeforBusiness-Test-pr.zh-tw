---
title: Lync Server 2013：Windows PowerShell 和 Lync Server 管理工具
TOCTitle: Windows PowerShell 和 Lync Server 2013 管理工具
ms:assetid: 6a285f7c-0ef5-4cab-9976-d03be276e35d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn481130(v=OCS.15)
ms:contentKeyID: 59679124
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Windows PowerShell 和 Lync Server 2013 管理工具

 

_**上次修改主題的時間：** 2014-10-21_

在 Microsoft Lync Server 2013 中，管理工具是以 Windows PowerShell 實作。Windows PowerShell 包括命令列環境、產品專用的命令和完整的指令碼語言。Lync Server 2013 工具是使用 Windows PowerShell 實作，其中包括：

  - **拓撲產生器**。您可以使用 拓撲產生器 來建立、調整和發佈規劃的拓樸，並在開始安裝伺服器之前驗證拓樸。在個別伺服器上安裝 Lync Server 2013 時，伺服器會在安裝過程中讀取發佈的拓樸，而安裝程式會依照拓樸中的指示來部署伺服器。安裝完畢之後，設定資訊會自動複製到所有伺服器上。您只能用拓撲產生器在部署中新增元件。

  - **Lync Server 管理命令介面**。您可以使用 Lync Server 管理命令介面 在部署中進行完整的命令列管理。

  - **Lync Server 控制台**。您可以用 Microsoft Lync Server 2013 控制台 使用者介面來管理部署中最常見的工作。

這些工具會使用 Windows PowerShell Cmdlet 來管理您的部署，包括將近 550 個產品專用的 Cmdlet。Lync Server 2013 隨附的安全性 Cmdlet 主要用於管理驗證，以及使用者的權利和權限。可用來管理驗證的 Cmdlet 種類繁多，包括用於驗證憑證和個人識別碼 (PIN) 的 Cmdlet。另外，您可以用一些 Cmdlet 來使用新的角色型存取控制 (RBAC) 功能，以委派 Lync Server 2013 的系統管理控制權。如需 Lync Server Cmdlet 的相關細節，請參閱＜作業＞文件中的 [Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)。如需瞭解使用 拓撲產生器 和 Lync Server 2013 控制台 來管理部署的相關詳細資料，請參閱＜作業＞文件中的 [Lync Server 2013 控制台](https://technet.microsoft.com/zh-tw/library/gg133224\(v=ocs.15\))。

Windows PowerShell 的指令碼安全性功能專為預防舊版技術 (包括 Microsoft Visual Basic Scripting Edition (VBScript)) 的指令碼安全性問題而設計。Windows PowerShell 的安全性功能旨在建立使用者無法輕易或在不知情的情況下執行指令碼的環境。預設會啟用 Windows PowerShell 的安全性功能。您可以依據您的指令碼執行需求與各種安全性目標，來修改這些功能的狀態。這不代表命令介面會讓使用者無法執行指令碼。命令介面只是預設成增加使用者在不知情情況下執行指令碼的困難度。如需詳細資料，請參閱＜Windows PowerShell 指令碼安全性＞(英文)：[http://go.microsoft.com/fwlink/p/?LinkId=213145](http://go.microsoft.com/fwlink/p/?linkid=213145)。

