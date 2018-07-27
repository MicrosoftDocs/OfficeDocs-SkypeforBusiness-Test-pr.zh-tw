---
title: Lync Server 2013：分支網站彈性功能
TOCTitle: 分支網站彈性功能
ms:assetid: 8e3feda5-9a38-4e3c-b808-af29f19c5eb9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398715(v=OCS.15)
ms:contentKeyID: 49291619
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的分支網站彈性功能

 

_**上次修改主題的時間：** 2014-02-10_

如果您提供分支網站恢復能力，當分支網站和中央網站間的 WAN 連線故障或當中央網站無法連線時，以下語音功能仍可繼續運作：


  - 輸入和輸出公用交換電話網路 (PSTN) 通話

  - 相同與不同的網站之間的使用者，皆可進行企業通話

  - 基本通話處理，包括通話保留、取回和轉接

  - 雙方立即訊息

  - 來電轉接、端點的同時響鈴、通話委派及小組通話等服務，但僅限委託人和代理人 (例如，經理和經理的系統管理員) 或小組成員都設定在相同的網站時

  - 詳細通話記錄 (CDR)

  - 使用會議自動語音應答的 PSTN 撥入式會議

  - 語音信箱功能 (如果您已設定語音信箱重新路由設定。如需詳細資訊，，請參閱＜ [Lync Server 2013 的分支網站復原需求](lync-server-2013-branch-site-resiliency-requirements.md)＞)。

  - 使用者驗證和授權

唯有當您的恢復解決方案是部署在分支網站的全規模 Lync Server 部署時，才能使用以下功能：

  - IM、Web 和 A/V 會議

  - 目前狀態和以請勿打擾 (DND) 為主的路由傳送 (可防止來電在已啟動 DND 的分機上響起)

  - 更新來電轉接設定

  - 回應群組應用程式和 通話駐留應用程式

  - 佈建新電話和用戶端，但僅限具有 Active Directory 網域服務 的分支網站。

  - 增強型 9-1-1 (E9-1-1)
    
    如果已部署 E9-1-1，當中央網站的 SIP 主幹由於 WAN 連結失效而無法連接時， Survivable Branch Appliance 會將 E9-1-1 通話路由傳送至本地分支閘道。若要啟用這項功能，當 WAN 失敗時，分支網站使用者的語音原則應將通話路由傳送至本地閘道。

> [!NOTE]  
> XMPP 不支援 SBA (基本分公司)。位於 SBA 組態中的使用者將無法傳送 IM 或看見 XMPP 連絡人的存在。


