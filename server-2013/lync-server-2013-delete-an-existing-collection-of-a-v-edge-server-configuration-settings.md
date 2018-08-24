---
title: 刪除現有的 A/V Edge Server 組態設定集合
TOCTitle: 刪除現有的 A/V Edge Server 組態設定集合
ms:assetid: 668d3613-e464-4b68-967a-cfff90b9ce4b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688077(v=OCS.15)
ms:contentKeyID: 49890096
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除現有的 A/V Edge Server 組態設定集合

 

_**上次修改主題的時間：** 2012-11-01_

A/V Edge Service 為內部使用者 (登入組織網路的使用者) 提供了與外部使用者 (非登入組織網路的使用者) 共用音訊和視訊的方法。主要是使用 A/V Edge 組態設定來管理 A/V Edge Service，這些設定可在網站範圍設定，或在服務範圍設定 (亦即可針對個別 A/V Edge Server 設定)。

安裝 Lync Server 時，就會自動建立 A/V Edge 組態設定的全域集合。此全域集合無法刪除，不過，可使用 Lync Server 管理命令介面和 Remove-CsAVEdgeConfiguration Cmdlet 來「重設」全域集合；這表示全域集合中所有的屬性值會重設為預設值。例如，如果已設定 MaxTokenLifetime 屬性為 16 小時，該屬性會重設為預設值 8 小時。

然而，使用 Remove-CsAVEdgeConfiguration Cmdlet 可刪除在網站範圍或服務範圍建立的自訂設定集合。如果刪除網站設定，則該網站中的 A/V Edge Server 會由全域設定進行管理。如果刪除服務範圍設定，該伺服器就會由網站設定 (若存在) 或全域設定 (若無網站設定) 進行管理。

如需詳細資訊，請參閱 [Remove-CsAVEdgeConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsAVEdgeConfiguration) Cmdlet 的說明主題。

## 重設全域集合

  - 下列命令會重設 A/V Edge 組態設定的全域集合：
    
        Remove-CsAVEdgeConfiguration -Identity "global"

## 從網站範圍移除集合

  - 下列命令會移除套用至 Redmond 網站的 A/V Edge 組態設定：
    
        Remove-CsAVEdgeConfiguration -Identity "site:Redmond"

## 從服務範圍移除集合

  - 下列命令會移除套用至 A/V Edge Server atl-edge-001.litwareinc.com 的設定：
    
        Remove-CsAVEdgeConfiguration -Identity "service:EdgeServer:atl-edge-001.litwareinc.com"

## 請參閱

#### 工作

[傳回 A/V Edge Server 設定資訊](lync-server-2013-return-a-v-edge-server-configuration-information.md)  
[建立或修改 A/V Edge Server 的組態設定集合](lync-server-2013-create-or-modify-a-collection-of-a-v-edge-server-configuration-settings.md)  

#### 其他資源

[Lync Server 2013 中的音訊/視訊 (A/V) Edge Server](lync-server-2013-audio-video-a-v-edge-servers.md)  
[Remove-CsAVEdgeConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsAVEdgeConfiguration)

