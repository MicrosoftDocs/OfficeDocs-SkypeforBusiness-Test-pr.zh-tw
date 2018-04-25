---
title: Lync Server 2013：IPv6 的移轉與共存考量
TOCTitle: IPv6 的移轉與共存考量
ms:assetid: 8c769c4f-c8a9-4cbf-9080-beee3be9848a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205068(v=OCS.15)
ms:contentKeyID: 49291611
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 IPv6 的移轉與共存考量

 

_**上次修改主題的時間：** 2012-06-14_

Lync Server 2010 或 Office Communications Server 上不支援 IP 版本 6 (IPv6)。基於試驗目的，您可以測試 Lync Server 2010 和 Lync Server 2013 雙重堆疊共存。我們建議您先將指定之中央網站的所有集區升級至 Lync Server 2013，然後再針對任一個集區啟用 IPv6 (雙重堆疊網路)。如果您只需要為 IPv6 設定集區，則建議您在實驗室環境中設定僅 IPv6 集區來進行測試。

在移轉和共存期間支援下列案例：

  - Lync Server 2013、 Lync Server 2010，以及處於 IPv4 模式的 Office Communications Server 2007 R2，在雙重堆疊模式中與 Lync Server 2013 共存。

  - 如果僅 IPv6 集區是獨立的，則為處於僅 IPv6 模式的 Lync Server 2013 集區。

