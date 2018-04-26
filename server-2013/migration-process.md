---
title: 移轉處理序
TOCTitle: 移轉處理序
ms:assetid: 13d71f4b-9d5e-4ea3-9e93-29fdad7ac68f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204696(v=OCS.15)
ms:contentKeyID: 49290166
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉處理序

 

_**上次修改主題的時間：** 2012-09-17_

Lync Server 2013 的建議及支援移轉程序為並存移轉。本主題說明應使用並存移轉的原因，並包含共存測試的相關資訊。

## 並存移轉

幾乎在每個移轉中都應使用並存移轉路徑。在並存移轉中，使用 Lync Server 2013 以及執行 Lync Server 2010 的對應伺服器部署新的伺服器，然後將作業轉移到新伺服器。如果有必要回復到 Lync Server 2010，您只能將作業切換回原本的伺服器。請注意，在此情況下，任何以升級之用戶端所排定的新會議將無法運作，而用戶端也可能需要降級。

## 共存測試

將 Lync Server 2013 與 Lync Server 2010 平行部署之後，部署會呈現 Lync Server 2013 與 Lync Server 2010 的共存測試狀態。在此狀態中，請務必測試並確定服務已啟動、每個網台都可以受系統管理，且用戶端可與目前及舊版使用者通訊。移轉所有使用者之前，請先了解每個部署的狀態並確定兩者皆正常運作，這點是非常重要的。一般來說，整個 Lync Server 2013 試驗測試中，都存在著共存測試。舊版使用者會暫時移至 Lync Server 2013 以確保應用程式相容性和功能運作正常。試驗測試結束後，使用者和應用程式將會移轉至正式版的 Lync Server 2013，而 Lync Server 2010 的舊版集區和應用程式則就此退役。

