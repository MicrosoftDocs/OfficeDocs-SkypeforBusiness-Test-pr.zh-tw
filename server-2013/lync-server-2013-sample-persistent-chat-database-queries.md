---
title: Lync Server 2013：常設聊天室資料庫查詢範例
TOCTitle: 常設聊天室資料庫查詢範例
ms:assetid: 545b1a93-9758-4344-98cc-aa0e559d494f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558649(v=OCS.15)
ms:contentKeyID: 49290937
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的常設聊天室資料庫查詢範例

 

_**上次修改主題的時間：** 2012-10-06_

本節包含 常設聊天室資料庫的範例查詢。

請使用下列範例來取得特定日期之後最活躍的 常設聊天室清單。

    SELECT nodeName as ChatRoom, COUNT(*) as ChatMessages
      FROM tblChat, tblNode
      WHERE channelId = nodeID AND dbo.fnTicksToDate(chatDate) > '1/1/2011'
      GROUP BY nodeName
      ORDER BY ChatMessages DESC

請使用下列範例來取得特定日期之後最活躍的使用者清單。

    SELECT prinName as Name, count(*) as ChatMessages
      FROM tblChat, tblPrincipal
      WHERE prinID = userId AND dbo.fnTicksToDate(chatDate) > '1/1/2011'
      GROUP BY prinName
      ORDER BY ChatMessages DESC

請使用下列範例來取得曾傳送內含「Hello World」之訊息的所有人清單。

    SELECT nodeName as ChatRoom, prinName as Name, content as Message
      FROM tblChat, tblNode, tblPrincipal
      WHERE channelId = nodeID AND userId = prinID AND content like '%Hello World%'

請使用下列範例來取得特定主體的群組成員資格清單。

    SELECT prinName as Name    
      FROM tblPrincipalAffiliations as pa, tblPrincipal
      where principalID = 7 and affiliationID = prinID

請使用下列範例來取得使用者 Jane Dow 為直接成員的每個聊天室清單。

    SELECT DISTINCT nodeName as ChatRoom, prinName as Name          
      FROM tblPrincipalRole, tblPrincipal, tblNode
      WHERE  prinRoleNodeID = nodeID AND prinRolePrinID = prinID AND prinName = 'Jane Dow'

請使用下列範例來取得使用者已收到的邀請清單。

    SELECT prinName
          ,nodeName
          ,invID   
          ,createdOn
      FROM tblPrincipalInvites as inv, tblPrincipal as p, tblNode as n
      where inv.prinID = 5 AND inv.prinID = p.prinID and inv.nodeID = n.nodeID
      ORDER BY invID DESC

