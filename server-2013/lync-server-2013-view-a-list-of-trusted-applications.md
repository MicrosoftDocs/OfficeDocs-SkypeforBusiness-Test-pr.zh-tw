---
title: 檢視受信任應用程式的清單
TOCTitle: 檢視受信任應用程式的清單
ms:assetid: f09300b3-67cf-4e70-a51a-23d62479b913
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182604(v=OCS.15)
ms:contentKeyID: 49292758
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視受信任應用程式的清單

 

_**上次修改主題的時間：** 2012-09-21_

您可以使用 Lync Server 2013 控制台，來檢視已在您的 Lync Server 2013 環境中部署的信任的應用程式清單。信任的應用程式是以 Lync Server 2013 所信任之 Microsoft Unified Communications Managed API (UCMA) 3.0 Core SDK 為基礎的應用程式。此信任關係在下列清單中摘要說明：

  - 信任的應用程式不會受到 Lync Server 的驗證挑戰。

  - 信任的應用程式不會由 Lync Server 進行 SIP 交易、連線或撥出 VoIP 電話的節流處理。

  - 信任的應用程式可以模擬任何使用者，而且可以加入會議而不顯示在名冊中。

  - 信任的應用程式具有高度可用性和彈性。

在 Lync Server 控制台 中，您可以看到應用程式的名稱、執行應用程式的集區，以及應用程式使用的連接埠。

## 若要檢視信任的應用程式清單

1.  使用指派給 CsServerAdministrator、CsAdministrator、CsHelpDesk 或 CsViewOnlyAdministrator 角色的使用者帳戶，登入內部部署中的任一電腦。如需 Lync Server 2013 中可用的預先定義管理角色的詳細資料，請參閱[在 Lync Server 2013 中規劃角色型存取控制](lync-server-2013-planning-for-role-based-access-control.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[拓撲\]，然後按一下 \[信任的應用程式\]。

4.  在 \[信任的應用程式\] 頁面上，視需要按一下欄標題以排序應用程式。

## 請參閱

#### 其他資源

[管理 Lync Server 2013 拓撲](lync-server-2013-managing-the-lync-server-topology.md)

