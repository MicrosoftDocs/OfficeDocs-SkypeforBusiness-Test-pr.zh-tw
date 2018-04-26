---
title: 共存考量
TOCTitle: 共存考量
ms:assetid: 9d1a3c0f-492a-4e37-bc2f-63509e328785
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205131(v=OCS.15)
ms:contentKeyID: 49291810
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 共存考量

 

_**上次修改主題的時間：** 2012-10-06_

移轉之後，只有 Lync Server 2013、 Persistent Chat Server 集區會存在， 您可以解除委任舊版部署。

在移轉完成之前及完全解除委任目前的 群組聊天伺服器部署之前，您可能會有下列任何部署：

  - Lync Server 2013、 Persistent Chat Server 集區，必須裝載於 Lync Server 2013 集區。

  - Lync Server 2010 群組聊天集區，必須裝載於 Lync Server 2010 集區。

  - Office Communications Server 2007 R2群組聊天集區，必須裝載於 Office Communications Server 2007 R2 集區。

這些部署可以並存。但是， 一個部署中的類別、聊天室及增益集不會與其他部署中的類別、分組討論區及增益集互動。

使用手動組態時，舊版用戶端 ( 群組聊天用戶端) 一次可以可以連線至 Office Communications Server 2007 R2、 Lync Server 2010 群組聊天或 Lync Server 2013 的一個集區。

Lync 2013 (用戶端) 只能與 Lync Server 2013、 Persistent Chat Server 集區互動，而不能與舊版 群組聊天伺服器集區互動。 若要在 Lync 2013 (用戶端) 使用 常設聊天室，使用者必須裝載於 Lync 2013 並且已根據原則啟用。

