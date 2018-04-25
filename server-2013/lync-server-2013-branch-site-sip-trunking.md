---
title: Lync Server 2013：分支網站 SIP 主幹連線
TOCTitle: 分支網站 SIP 主幹連線
ms:assetid: c4d9dfcd-8baa-41ea-9677-48b0e429429d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412974(v=OCS.15)
ms:contentKeyID: 49292257
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的分支網站 SIP 主幹連線

 

_**上次修改主題的時間：** 2012-09-21_

在某些情況下，您必須在選取的 分支網站實作分散式 SIP 主幹連線。若要判斷 分支網站是否需要 SIP 主幹，請檢閱 [如何在 Lync Server 2013 中實作 SIP 主幹？](lync-server-2013-how-do-i-implement-sip-trunking.md)中的資訊。

如需關於在 分支網站中部署 SIP 主幹時可支援之拓撲選項的詳細資訊，請參閱 [Lync Server 2013 中的分支網站恢復解決方案](lync-server-2013-branch-site-resiliency-solutions.md)。

## 範例分支網站 SIP 主幹需求分析

當您決定部署 分支網站 SIP 主幹時，您需執行網站專屬的成本分析。例如，在華盛頓州 Redmond 擁有 中央網站並在紐約擁有 分支網站的企業，應該進行分析來判斷是否要實作從紐約網站到當地服務提供者的 SIP 主幹。

若要判斷在紐約的分散式 SIP 主幹是否具成本效益，請找出要使用 SIP 主幹的直接向內撥號 (DID) 號碼，並且分析紐約撥打至 Redmond (425) 以外區域的通話數。您的 分支網站 DID 終端機可以位於 中央網站。例如，Redmond 中央網站可以裝載紐約 分支網站的 DID 號碼。如果實作分散式 SIP 主幹的成本低於這些通話的成本，則考慮在紐約 分支網站實作 SIP 主幹。

## 其他分支網站 SIP 主幹的需求

選擇部署 SIP 主幹而非閘道主要是依據每一個選項的公用交換電話網路 (PSTN) 長途電話費用。如果您部署 分支網站 SIP 主幹，則也需要判斷恢復和頻寬需求。如果您的 分支網站和 中央網站之間的連結具有恢復能力而且擁有足夠的頻寬，則可以部署 SIP 主幹或閘道。您不需要在 分支網站部署 Survivable Branch Appliance。如果您的 分支網站和 中央網站之間的連結不具有恢復能力，則在 分支網站上部署 Survivable Branch Appliance 或具有閘道或 SIP 主幹的 Survivable Branch 伺服器。

