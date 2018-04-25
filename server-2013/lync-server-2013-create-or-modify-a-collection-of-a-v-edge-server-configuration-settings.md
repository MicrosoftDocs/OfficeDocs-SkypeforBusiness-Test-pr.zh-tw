---
title: 建立或修改 A/V Edge Server 的組態設定集合
TOCTitle: 建立或修改 A/V Edge Server 的組態設定集合
ms:assetid: 43899518-59c6-4be4-8892-d6f6207bfaab
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688039(v=OCS.15)
ms:contentKeyID: 49890042
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改 A/V Edge Server 的組態設定集合

 

_**上次修改主題的時間：** 2012-11-01_

A/V Edge 服務可讓內部使用者 (即已登入您組織網路的使用者) 將音訊和視訊共用給外部使用者 (即未登入您組織網路的使用者)。此服務主要是採用 A/V Edge 組態設定管理，可以在網站範圍或服務範圍裡完成這些設定 (亦即可以針對個別 A/V Edge 伺服器進行設定)。

安裝 Lync Server 時，會一併幫您建立 A/V Edge 組態設定的全域集合。除此之外，也可利用 Lync Server 管理命令介面和 New-CsAVEdgeConfiguration Cmdlet 在網站範圍或服務範圍裡建立新設定 (亦即可針對個別 A/V Edge 伺服器進行)。若要建立新設定，請務必記住：

  - 服務範圍 (亦即在個別伺服器) 中的設定優先使用。

  - 在網站範圍進行的設定優先順序高於在全域範圍進行的設定，但服務範圍設定仍將取代網站範圍設定。

  - 若個別伺服器裡未進行任何服務設定，且該伺服器所處的網站無任何網站設定，才會使用全域範圍的設定。

任何設定都可以使用 Set-CsAVEdgeConfiguration Cmdlet 修改。如需詳細資訊，請參閱 [New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md) 和 [Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md) Cmdlet 的說明主題。

## 在網站範圍內建立新的 A/V Edge 組態設定

  - 以下的命令會針對 Redmond 網站，建立新的 A/V Edge 組態設定集合。
    
        New-CsAVEdgeConfiguration -Identity "site:Redmond"

## 在網站範圍內建立自訂的 A/V Edge 組態設定

  - 由於這些新設定不包含其他參數，因此會使用 A/V Edge 服務的預設值。您也可以選擇新增其他參數和參數值來建立自訂集合。舉例來說，此命令將 MaxTokenLifetime 屬性設為 4 小時 (04 時 : 00 分 : 00 秒)：
    
        New-CsAVEdgeConfiguration -Identity "site:Redmond" -MaxTokenLifetime "04:00:00"

## 在服務範圍內建立自訂的 A/V Edge 組態設定

  - 此命令建立套用至 A/V Edge 伺服器 atl-edge-001.litwareinc.com 的相似集合：
    
        New-CsAVEdgeConfiguration -Identity "service:EdgeServer:atl-edge-001.litwareinc.com" -MaxTokenLifetime "04:00:00"

## 修改現有的 A/V Edge 組態設定

  - 本範例是使用 Set-CsAVEdgeConfiguration Cmdlet 將 Redmond 網站的最大權杖存留期更改為 12 小時：
    
        Set-CsAVEdgeConfiguration -Identity "site:Redmond" -MaxTokenLifetime "12:00:00"

## 請參閱

#### 工作

[傳回 A/V Edge Server 設定資訊](lync-server-2013-return-a-v-edge-server-configuration-information.md)  
[刪除現有的 A/V Edge Server 組態設定集合](lync-server-2013-delete-an-existing-collection-of-a-v-edge-server-configuration-settings.md)  

#### 其他資源

[Lync Server 2013 中的音訊/視訊 (A/V) Edge Server](lync-server-2013-audio-video-a-v-edge-servers.md)  
[New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)  
[Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

