---
title: Lync Server 2013：匯入語音路由組態檔
TOCTitle: 匯入語音路由組態檔
ms:assetid: 4bac05e5-ed8b-4f10-96b0-b8a65ff356ec
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398301(v=OCS.15)
ms:contentKeyID: 49290857
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中匯入語音路由組態檔

 

_**上次修改主題的時間：** 2012-11-01_

如果您想要儲存語音路由設定但不要發佈該設定，請依照這些步驟，使用 Lync Server 控制台設定匯出和匯入命令來儲存並擷取語音路由設定的快照。當您匯入語音路由設定檔 (.vcfg) 時，如果伺服器上的語音路由設定同時有所變更，則 Lync Server 控制台中 \[語音路由\] 群組內的頁面上，會指出語音路由有未認可的變更。這些未認可的變更是指這兩個設定間需要協調的差異處。

如果您在群組中的任何頁面上對設定進行了未認可的變更，這些變更會儲存在匯出的語音設定檔 (.vcfg) 中。這可讓您在發佈變更之前，在多個工作階段進行期間執行語音路由設定變更。

## 若要匯入語音路由設定

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[語音路由\] 。

4.  在 **\[執行\]** 功能表上，按一下 **\[匯入設定\]** 。

5.  尋找您要匯入的組態檔，然後按一下 **\[開啟\]** 。

6.  依序按一下 **\[認可\]** 和 **\[全部認可\]** 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>每當您匯入語音設定檔時，您必須執行 <strong>[全部認可]</strong> 命令來發佈設定變更。如需詳細資訊，請參閱作業文件中的 <a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中發佈擱置變更至語音路由設定</a></td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 工作

[在 Lync Server 2013 中匯出語音路由組態檔](lync-server-2013-export-a-voice-route-configuration-file.md)  
[在 Lync Server 2013 中發佈擱置變更至語音路由設定](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)

