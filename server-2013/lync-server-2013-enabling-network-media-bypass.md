---
title: 啟用網路媒體旁路
TOCTitle: 啟用網路媒體旁路
ms:assetid: 95c4fa06-49d3-41ac-acdc-7dcda66e5508
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182552(v=OCS.15)
ms:contentKeyID: 49291719
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用網路媒體旁路

 

_**上次修改主題的時間：** 2012-11-01_

您可以在整個 Microsoft Lync Server 2013 部署全域套用媒體旁路設定。媒體旁路允許通話略過中繼伺服器。如需何時可使用媒體旁路的詳細資訊，請參閱＜規劃＞一節中的[在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)。

您可以從 Lync Server 控制台啟用及設定媒體旁路。

## 若要啟用及設定媒體旁路

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[網路設定\]，然後按一下 \[通用\]。

4.  在 \[通用\] 頁面上，按一下 \[通用\] 設定。其中一律只有一項設定，且一律稱為「通用」。

5.  在 \[編輯\] 功能表中，按一下 \[檢視詳細資料\]。

6.  在 **\[編輯通用設定\]** 頁面中，按一下 **\[啟用媒體旁路\]** 核取方塊。

7.  選取以下任一選項：
    
      - **永遠略過**   選取此選項可嘗試對所有通話執行媒體旁路。在啟用通話許可控制 (CAC) 時，無法使用此選項。如果 CAC 未啟用，在下列情況下請選取此選項。
        
          - 不需要頻寬控制。
        
          - 不需要精細的組態來決定旁路的發生時機。
        
          - 閘道和用戶端之間有完整的連線能力。
    
      - **使用網站和地區設定**   如果 CAC 已啟用，依預設系統會選取此選項且您無法變更。當此選項已選取時，系統會使用網路組態網站和地區來判斷媒體旁路的適用時機。如果您選取此選項，可以針對未對應的網站選擇啟用旁路。唯有在有一個或多個大型網站與沒有頻寬限制的相同地區 (如大型的中央網站) 相關聯，同時還有某些分支網站與具有頻寬限制的相同地區相關聯時，才按一下 \[啟用非對應網站的旁路\] 核取方塊。當您啟用非對應網站的旁路時，設定作業比較精簡，因為您只需指定與分支網站關聯的子網路，而不需指定與所有網站關聯的所有子網路。如果已啟用 CAC，則建議您不要選取 \[啟用非對應網站的旁路\] 核取方塊。

8.  按一下 \[認可\] 以儲存變更。

## 請參閱

#### 工作

[停用網路媒體旁路](lync-server-2013-disabling-network-media-bypass.md)  

#### 概念

[Lync Server 2013 中的全域媒體旁路選項](lync-server-2013-global-media-bypass-options.md)  

#### 其他資源

[在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)

