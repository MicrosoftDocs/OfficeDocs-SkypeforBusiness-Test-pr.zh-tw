---
title: Lync Server 2013：匯出語音路由組態檔
TOCTitle: 匯出語音路由組態檔
ms:assetid: 02ce922d-9ca8-4513-b09f-9de51f5c5bdc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398081(v=OCS.15)
ms:contentKeyID: 49289915
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中匯出語音路由組態檔

 

_**上次修改主題的時間：** 2012-11-01_

如果您想要儲存語音路由設定但不要發佈該設定，請依照這些步驟，使用 Lync Server 控制台設定匯出和匯入命令來儲存並擷取語音路由設定的快照。當您匯入語音路由設定檔 (.vcfg) 時，如果伺服器上的語音路由設定同時有所變更，則 Lync Server 控制台中 \[語音路由\] 群組內的頁面上，會指出語音路由有未認可的變更。這些未認可的變更是指這兩個設定間需要協調的差異處。

如果您在群組中的任何頁面上對設定進行了未認可的變更，這些變更會儲存在匯出的語音設定檔 (.vcfg) 中。這可讓您在發佈變更之前，在多個工作階段進行期間執行語音路由設定變更。

## 若要匯出語音路由設定

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[語音路由\] 。

4.  在 **\[執行\]** 功能表上，按一下 **\[匯出設定\]** 。

5.  指定位置和檔案名稱，然後按一下 **\[儲存\]** 。

## 請參閱

#### 工作

[在 Lync Server 2013 中匯入語音路由組態檔](lync-server-2013-import-a-voice-route-configuration-file.md)

