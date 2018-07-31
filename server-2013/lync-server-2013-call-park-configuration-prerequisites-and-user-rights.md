---
title: Lync Server 2013：通話駐留組態先決條件和使用者權限
TOCTitle: 通話駐留組態先決條件和使用者權限
ms:assetid: 25b8cfe0-e4e7-487c-9e78-8c040f629059
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425730(v=OCS.15)
ms:contentKeyID: 49290365
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的通話駐留組態先決條件和使用者權限

 

_**上次修改主題的時間：** 2012-09-10_

通話駐留是部署 企業語音時，預設安裝的一項通話管理功能。本主題說明在設定 通話駐留前，必須備妥的項目，以及執行設定工作所需的使用者權限。

> [!IMPORTANT]  
> 在 Lync Server 2013 災害復原程序時，系統不會將 通話駐留應用程式的自訂等候音樂檔案備份，因此若檔案所上傳的集區受損、損毀或遭清除，這些檔案就會遺失。請一律另行備份一份用於 通話駐留的已上傳自訂等候音樂檔案複本。



本節假設您已閱讀與 通話駐留相關的規劃文件 (請參閱＜ [在 Lync Server 2013 中規劃通話管理功能](lync-server-2013-planning-for-call-management-features.md)＞)。

## 通話駐留組態先決條件

通話駐留須有以下元件：

  - 應用程式服務

  - 通話駐留應用程式

這些元件在部署 企業語音時即已自動安裝。

如果希望來電者在通話駐留時可以聽到音樂，則需要等候音樂檔案。部署 企業語音時會自動安裝預設的等候音樂檔案。您可以用自己的等候音樂檔案取代預設檔案。 通話駐留使用檔案存放區來存放音訊檔案。

## 通話駐留設定使用者權限

您可以使用下列系統管理工具來設定 通話駐留：

  - Lync Server 控制台

  - Lync Server 管理命令介面

您可以使用這些工具設定 通話駐留軌道範圍表，以及設定 通話駐留使用的其他設定值。

設定 通話駐留需要下列任一系統管理角色，依工作而定：

  - **CsVoiceAdministrator ：** 此系統管理員角色可以建立、設定和管理所有語音相關設定和原則。

  - **CsUserAdministrator ：** 此系統管理員角色可以啟用語音原則中的 通話駐留。其也具有所有語音設定的唯讀檢視存取權。

  - **CsServerAdministrator ：** 此系統管理員角色可以管理、監視和疑難排解伺服器及服務問題。

  - **CsAdministrator ：** 此系統管理員角色可以執行 CsVoiceAdministrator 、CsServerAdministrator 和 CsUserAdministrator 的所有工作。

> [!NOTE]  
> 如需管理權限的詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-planning-for-role-based-access-control.md">在 Lync Server 2013 中規劃角色型存取控制</a>＞。



## 請參閱

#### 概念

[在 Lync Server 2013 中部署企業語音](lync-server-2013-deploying-enterprise-voice.md)  

#### 其他資源

[在 Lync Server 2013 中規劃通話管理功能](lync-server-2013-planning-for-call-management-features.md)

