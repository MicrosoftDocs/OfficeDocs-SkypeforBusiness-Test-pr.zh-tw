---
title: 備份封存資料庫和監控資料庫
TOCTitle: 備份封存資料庫和監控資料庫
ms:assetid: c120db81-b02c-4a4c-90cd-8aca6cff64f9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202188(v=OCS.15)
ms:contentKeyID: 52056215
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 備份封存資料庫和監控資料庫

 

_**上次修改主題的時間：** 2013-02-17_

如有部署封存或監控，必須依據組織的 SQL Server 備份原則備份這些資料庫。

> [!NOTE]  
> 當您備份中央管理存放區時，會一併備份封存及監控的設定。如需詳細資訊，請參閱＜<a href="lync-server-2013-backing-up-core-data-and-settings.md">備份核心資料和設定</a>＞。



對於封存及監控，您可以使用 SQL Server 工具 (例如 SQL Server Management Studio) 執行手動備份，也可以使用 SQL Server 管理工具安排定期自動備份。

