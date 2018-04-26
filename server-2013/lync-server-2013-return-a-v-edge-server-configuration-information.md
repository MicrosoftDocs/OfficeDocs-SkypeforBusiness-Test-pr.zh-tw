---
title: 傳回 A/V Edge Server 設定資訊
TOCTitle: 傳回 A/V Edge Server 設定資訊
ms:assetid: b041f5a4-2387-4075-846c-ec4f99640903
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721850(v=OCS.15)
ms:contentKeyID: 49890264
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 傳回 A/V Edge Server 設定資訊

 

_**上次修改主題的時間：** 2012-11-01_

A/V Edge Service 提供方法讓您的內部使用者 (登入您組織網路的使用者) 能與外部使用者 (未登入您組織網路的使用者) 共用音訊與視訊。A/V Edge Service 主要是使用 A/V Edge 組態設定來進行管理，您可在網站範圍或服務範圍 (就是可針對個別 A/V Edge Server 進行設定) 來配置這些設定。

若要傳回您組織內正在使用的 A/V Edge 組態設定資訊，您必須使用 \[Lync Server 管理命令介面\] 與 Get-CsAVEdgeConfiguration Cmdlet。如需詳細資訊，請參閱 [Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md) Cmdlet 的說明主題。

從 Get-CsAVEdgeConfiguration Cmdlet 傳回的資訊類似下列：

    Identity              : Global
    MaxTokenLifetime      : 08:00:00
    MaxBandwidthPerUserKb : 10000
    MaxBandwidthPerPortKb : 3000

## 傳回所有 A/V Edge 組態設定的資訊

  - 下列命令會傳回組織中目前正在使用的所有 A/V Edge 組態設定資訊：
    
        Get-CsAVEdgeConfiguration

## 傳回網站範圍 A/V Edge 組態設定的資訊

  - 若要傳回特定 A/V Edge 組態設定集合的資訊，請在執行 Get-CsAVEdgeConfiguration Cmdlet 時指定該集合的識別碼。例如，以下命令只會傳回套用至 Redmond 網站的設定資訊：
    
        Get-CsAVEdgeConfiguration -Identity "site:Redmond"

## 傳回服務範圍 A/V Edge 組態設定的資訊

  - 此命令只會傳回套用至特定 A/V Edge Server 的設定資訊：
    
        Get-CsAVEdgeConfiguration -Identity "service:EdgeServer:atl-edge-001.litwareinc.com"

## 請參閱

#### 工作

[建立或修改 A/V Edge Server 的組態設定集合](lync-server-2013-create-or-modify-a-collection-of-a-v-edge-server-configuration-settings.md)  
[刪除現有的 A/V Edge Server 組態設定集合](lync-server-2013-delete-an-existing-collection-of-a-v-edge-server-configuration-settings.md)  

#### 其他資源

[Lync Server 2013 中的音訊/視訊 (A/V) Edge Server](lync-server-2013-audio-video-a-v-edge-servers.md)

