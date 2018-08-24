---
title: Lync Server 2013：改善語音路由測試案例
TOCTitle: 改善語音路由測試案例
ms:assetid: 6546e24c-9ad2-428b-92b2-63948ed0f884
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398460(v=OCS.15)
ms:contentKeyID: 49291143
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中改善語音路由測試案例

 

_**上次修改主題的時間：** 2013-02-21_

測試案例提供了測試組織中語音路由的方法；定義要撥打的號碼，以及要採用的撥號對應表和語音原則等，然後 Lync Server 2013 就可以驗證在指定的那些條件下，驗證提供的號碼是否可以成功路由至 PSTN 網路。

測試案例 (可以使用 Lync Server 控制台建立) 通常僅儲存在原先建立並執行案例的伺服器上。不過這些測試案例可以匯出為 XML 檔案 (副檔名為 .vtest)，然後匯入其他伺服器。這讓您可以在位於拓撲中不同點之不同電腦上執行相同的測試。

## 匯入語音路由測試案例

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[語音路由\] 。

4.  在 **\[執行\]** 功能表上，按一下 **\[匯入測試案例\]** 。

5.  尋找想要匯入的測試案例檔案 (.vtest)，然後按一下 **\[開啟\]** 。

6.  依序按一下 **\[認可\]** 和 **\[全部認可\]** 。
    
    > [!NOTE]  
    > 只要匯入 .vtest 檔案，就必須執行 <strong>[全部認可]</strong> 命令，來發行測試案例。如需詳細資訊，請參閱作業文件中的 <a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中發佈擱置變更至語音路由設定</a>。
    


## 請參閱

#### 工作

[在 Lync Server 2013 中匯出語音路由測試案例](lync-server-2013-export-voice-routing-test-cases.md)

