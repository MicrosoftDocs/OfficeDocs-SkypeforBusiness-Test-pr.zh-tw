---
title: Lync 2013 的群組原則設定
TOCTitle: Lync 2013 的群組原則設定
ms:assetid: 5917a52b-dae0-4ec0-8548-a68dc20ab71c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204924(v=OCS.15)
ms:contentKeyID: 49290996
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync 2013 的群組原則設定

 

_**上次修改主題的時間：** 2012-10-03_

在舊版 Lync 和 Office Communicator 中，獨立的 Communicator.adm 系統管理範本可用來設定用戶端群組原則設定。針對 Lync 2013，新的系統管理範本檔 (.admx 和 .adml 檔案) 均包含在 Office 群組原則系統管理範本中。可用的 Lync 2013 .admx 和 .adml 檔案，允許您下載範本並集中管理所有 Office 程式與語言套件的群組原則設定。如需詳細資訊，請參閱 ＜Office 2013 ＞文件中的＜Office 2013 A系統管理範本檔案 (ADMX、ADML)＞，網址為[http://go.microsoft.com/fwlink/?linkid=267516\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=267516%26clcid=0x404)。

## 用戶端啟動原則

有幾個用戶端啟動原則是您必須在使用者第一次登入伺服器之前設定的。由於這些原則會在用戶端登入並開始接收來自伺服器的頻內佈建設定之前生效，因此，您可以使用群組原則進行設定。如需詳細資訊，請參閱部署文件中的＜[在 Lync Server 2013 中設定用戶端啟動程序原則](lync-server-2013-configuring-client-bootstrapping-policies.md)＞。

