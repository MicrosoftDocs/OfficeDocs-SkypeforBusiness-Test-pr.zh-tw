---
title: 群組來電接聽組態先決條件和使用者權限
TOCTitle: 群組來電接聽組態先決條件和使用者權限
ms:assetid: 8757b1d3-751d-49c3-b1b8-b678f663f18e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945641(v=OCS.15)
ms:contentKeyID: 52056163
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 群組來電接聽組態先決條件和使用者權限

 

_**上次修改主題的時間：** 2013-01-30_

群組來電接聽是是部署企業語音時，預設安裝的一項通話管理功能。本主題說明在設定群組來電接聽前，必須備妥的項目，以及執行設定工作所需的使用者權限。

本節假設您已閱讀群組來電接聽的相關規劃文件 (請參閱＜[規劃 Lync Server 2013 中的群組來電接聽](lync-server-2013-planning-for-group-call-pickup.md)＞)。

## 群組來電接聽設定先決條件

群組來電接聽需要以下元件：

  - 應用程式服務

  - 通話駐留應用程式

這些元件在部署企業語音時即已自動安裝。

## 群組來電接聽設定使用者權限

您可使用下列管理工具來設定群組來電接聽：

  - Lync Server 管理命令介面

  - SEFAUtil Resource Kit 工具

使用 Lync Server 管理命令介面建立並管理通話駐留範圍表中的來電接聽群組。使用 SEFAUtil Resource Kit 工具以指派來電接聽群組，並為使用者啟用或停用群組來電接聽。

依工作而定，設定群組來電接聽需要下列任一系統管理角色：

  - **CsVoiceAdministrator：**此系統管理員角色可以建立、設定和管理所有語音相關設定和原則。

  - **CsUserAdministrator：**此系統管理員角色可以為使用者啟用群組來電接聽。其也具有所有語音設定的唯讀檢視存取權。

  - **CsServerAdministrator：**此系統管理員角色可以管理、監視和疑難排解伺服器及服務問題。

  - **CsAdministrator：**此系統管理員角色可以執行 CsVoiceAdministrator 、CsServerAdministrator 和 CsUserAdministrator 的所有工作。

> [!NOTE]  
> 如需管理權限的詳細資訊，請參閱規劃文件中的＜<a href="lync-server-2013-planning-for-role-based-access-control.md">在 Lync Server 2013 中規劃角色型存取控制</a>＞。



## 請參閱

#### 概念

[在 Lync Server 2013 中部署企業語音](lync-server-2013-deploying-enterprise-voice.md)  

#### 其他資源

[在 Lync Server 2013 中規劃通話管理功能](lync-server-2013-planning-for-call-management-features.md)

