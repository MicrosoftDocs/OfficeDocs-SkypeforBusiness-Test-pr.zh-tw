---
title: Lync Server 2013：宣告組態先決條件和角色
TOCTitle: 宣告組態先決條件和角色
ms:assetid: 82f2dfe9-4c5e-4d65-96a1-96495d506ea4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398658(v=OCS.15)
ms:contentKeyID: 49291504
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的宣告組態先決條件和角色

 

_**上次修改主題的時間：** 2013-02-25_

宣告是 企業語音 通話管理功能。本主題說明在設定宣告之前您必須準備就緒的項目，以及您需要執行設定工作的角色指派。

本節假設您已閱讀有關宣告的規劃文件 (請參閱＜ [在 Lync Server 2013 中規劃通話管理功能](lync-server-2013-planning-for-call-management-features.md)＞)。

## 宣告設定先決條件

宣告應用程式須有以下元件：

  - 應用程式服務

  - 回應群組應用程式

  - 用來存放音訊檔案的檔案存放區

當您部署 企業語音時，預設會安裝上述所有元件。

## 宣告設定角色

您可以使用下列系統管理工具來設定宣告：

  - Lync Server 控制台

  - Lync Server 管理命令介面

設定 宣告應用程式時須有以下任一系統管理角色：

  - **CsVoiceAdministrator**   此系統管理員角色能建立、設定及管理所有和語音相關的設定和原則 (包括宣告設定)。

  - **CsServerAdministrator**   此系統管理員角色能管理、監控及疑難排解伺服器和服務，以及設定所有宣告設定。

  - **CsAdministrator**   此系統管理員角色可以執行所有系統管理工作，以及修改所有設定。

  - **CsViewOnlyAdministrator**   此系統管理員角色可以檢視部署，以監控部署健康情況。

> [!NOTE]  
> 如需關於系統管理使用者權限的詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-planning-for-role-based-access-control.md">在 Lync Server 2013 中規劃角色型存取控制</a>＞。



## 請參閱

#### 概念

[在 Lync Server 2013 中部署企業語音](lync-server-2013-deploying-enterprise-voice.md)  

#### 其他資源

[在 Lync Server 2013 中規劃通話管理功能](lync-server-2013-planning-for-call-management-features.md)

