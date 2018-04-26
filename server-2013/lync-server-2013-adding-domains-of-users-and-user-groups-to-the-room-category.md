---
title: Lync Server 2013：將使用者及使用者群組的網域新增至聊天室類別
TOCTitle: 將使用者及使用者群組的網域新增至聊天室類別
ms:assetid: ee03f2cf-1c84-41c4-b524-d0729be33b8c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ215884(v=OCS.15)
ms:contentKeyID: 49292723
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將使用者及使用者群組的網域新增至聊天室類別

 

_**上次修改主題的時間：** 2014-02-07_

若要將較多群組的使用者新增至聊天室，請參閱「部署」文件中的 [在 Lync Server 2013 中設定類別](lync-server-2013-configure-categories.md)與 [管理類別](manage-categories.md)。例如此命令可將使用中目錄的 NorthAmericaUsers OU 中的所有使用者新增至 NorthAmerica 聊天室：

    Set-CsPersistentChatRoom -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com\NorthAmerica" -Members @{Add="OU=NorthAmericaUsers,DC=litwareinc,DC=com"}

他的命令會將 Finance 通訊群組中的所有成員新增至相同的聊天室：

    Set-CsPersistentChatRoom -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com\NorthAmerica" -Members @{Add="CN=Finance,OU=ExternalUsers,DC=litwareinc,DC=com"}

