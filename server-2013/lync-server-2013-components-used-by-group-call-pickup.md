---
title: 群組來電接聽使用的元件
TOCTitle: 群組來電接聽使用的元件
ms:assetid: 45db2f23-d486-4b20-a8cf-7b48a1f9fd3a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945625(v=OCS.15)
ms:contentKeyID: 52056104
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 群組來電接聽使用的元件

 

_**上次修改主題的時間：** 2013-01-30_

群組來電接聽會在您部署企業語音和通話駐留應用程式時自動部署。透過設定通話駐留範圍表，將不同範圍的號碼指定為來電接聽群組號碼，然後將使用者指派給來電接聽群組，並啟用群組來電接聽的使用者，即可啟用群組來電接聽。下列 Lync Server 元件可支援群組來電接聽︰

  - **應用程式服務**   應用程式服務提供部署、裝載和管理整合通訊應用程式 (如通話駐留應用程式) 的平台。應用程式服務會自動安裝在前端集區中的每部前端伺服器上，以及每部 Standard Edition Server 上。

  - **通話駐留應用程式**   通話駐留應用程式是應用程式服務裝載的整合通訊應用程式之一。群組來電接聽的基礎為通話駐留應用程式。

  - **Lync Server 管理命令介面**   您可使用 Lync Server 管理命令介面來管理群組來電接聽群組。

  - **SEFAUtil Resource Kit 工具**   您可使用次要分機功能啟動公用程式 (SEFAUtil)，將使用者指派給來電接聽群組，並啟用或停用使用者的來電接聽。

