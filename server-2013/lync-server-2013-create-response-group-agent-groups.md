---
title: Lync Server 2013：建立回應群組代理群組
TOCTitle: 建立回應群組代理群組
ms:assetid: 2a80de17-ead0-46e8-8a27-7a4e233dbde0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520969(v=OCS.15)
ms:contentKeyID: 49290403
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立回應群組代理群組

 

_**上次修改主題的時間：** 2012-09-12_

當您建立代理群組時，需要選取指派給該群組的代理，並指定額外的群組設定，例如路由方法以及代理是否可以登入和登出群組。

必須登入和登出群組 (與登入或登出 Lync Server 不同) 的代理，稱為「正式代理」 。正式代理必須先登入此群組，才可以接聽路由傳送到此群組的電話。對於以兼職身分接聽群組來電的代理而言，這可能相當實用。正式代理可按一下 Lync 2013 中的功能表項目，開啟 Windows Internet Explorer 網際網路瀏覽器並顯示網頁主控台，以登入或登出其群組。

未登入或登出群組的代理人稱為 *「非正式代理人」* 。非正式代理人會在登入 Lync Server 時自動登入群組，但無法登出群組。

> [!NOTE]  
> 代理人只能為內部部署使用者。若代理人從內部部署移至線上， 回應群組通話將不會路由傳送至該代理人。



## 本章節內容

[在 Lync Server 2013 中建立或修改代理人群組](lync-server-2013-create-or-modify-an-agent-group.md)

