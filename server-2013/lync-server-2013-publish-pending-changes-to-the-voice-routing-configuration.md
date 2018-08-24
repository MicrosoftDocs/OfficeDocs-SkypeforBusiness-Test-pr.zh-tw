---
title: Lync Server 2013：發佈擱置變更至語音路由設定
TOCTitle: 發佈擱置變更至語音路由設定
ms:assetid: ff941d0b-fb4b-47d2-b866-6d990ac66b81
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413088(v=OCS.15)
ms:contentKeyID: 49292935
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中發佈擱置變更至語音路由設定

 

_**上次修改主題的時間：** 2012-08-07_

您在 \[語音路由\] 群組的頁面中變更任何組態設定之後，請執行此程序檢閱、發佈或取消擱置的變更。

> [!Note]  
> 務必確定一次只有一位使用者修改 [語音路由] 組態設定。<br />
> 所有擱置的變更必須藉由執行 [全部認可] 命令同時發佈。您無法選擇性地發佈擱置的變更。在您發佈擱置的變更之前，執行 [檢閱未認可的變更] 命令，並取消您不想要發佈的任何組態變更。<br />
> 如果您在認可擱置的變更之前離開 [語音路由] 群組的頁面，則所有擱置的變更都會遺失。不過，您可以將目前的組態 (包括任何擱置的變更) 匯出至語音組態檔，然後匯入並發佈更新的組態。如需詳細資訊，請參閱 <a href="lync-server-2013-export-a-voice-route-configuration-file.md">在 Lync Server 2013 中匯出語音路由組態檔</a>。



## 若要檢閱、發佈或取消語音路由組態變更

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[語音路由\] 。

4.  在 \[語音路由\] 群組的每一個頁面上，對您想要的設定進行組態變更。

5.  若要檢閱擱置的變更但不進行發佈，請選取 \[認可\] 功能表中的 \[檢閱未認可的變更\] 。

6.  如果您想要取消任何擱置的變更，請執行下列其中一項操作：
    
      - 從 \[認可\] 功能表選取 \[取消所有未認可的變更\] 。
    
      - 導覽至 \[語音路由\] 頁面上您要取消其擱置變更的索引標籤，選取擁有擱置變更的項目，按一下 \[認可\] ，然後按一下 \[取消選取的變更\] 。

7.  在您檢閱所有擱置的變更並且取消任何不想要發佈的變更之後，按一下 \[認可\] ，再按一下 \[全部認可\] 。

8.  在顯示所有擱置變更之清單的 \[未認可的語音組態設定\] 對話方塊中，按一下 \[確定\] 。
    
    Lync Server 控制台 認可變更之後，\[已成功發行語音路由設定\] 訊息就會出現。

