---
title: 移轉程序
TOCTitle: 移轉程序
ms:assetid: b2bd9c76-2f4b-4d14-a5c4-157bbff75de0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205181(v=OCS.15)
ms:contentKeyID: 49292049
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉程序

 

_**上次修改主題的時間：** 2012-09-24_

Lync Server 2013 的建議及支援移轉程序為並存移轉程序。本主題說明應該使用並存移轉的原因，並包含共存資訊。

## 並存移轉

幾乎在每種移轉時，您都應該使用並存移轉路徑。進行並存移轉的方法是，先使用 Lync Server 2013 部署一個新伺服器，再配合一個執行 Office Communications Server 2007 R2 的相對應伺服器，然後再將作業傳送到新伺服器。如果有必要回復到 Office Communications Server 2007 R2，您只能將作業切換回原本的伺服器。請注意在這樣的情況下，任何與升級用戶端排定的新會議皆無法運作，導致用戶端也必須降級。

## 共存測試

部署了 Lync Server 2013 及平行的 Office Communications Server 2007 R2 後，拓撲會呈現出 Lync Server 2013 與 Office Communications Server 2007 R2 的共存測試狀態。在此狀態中，請務必測試並確定服務有啟動、每個網站都可以受系統管理，且用戶端可與目前及舊版使用者通訊。移轉所有使用者之前，請先了解每個部署的狀態並確定每個部署皆正常運作，這點是非常重要的。一般來說，整個 Lync Server 2013 試驗測試中，都會進行這項共存測試。舊版使用者會暫時移至 Lync Server 2013 以確保應用程式相容性和功能運作正常。試驗測試結束後，使用者和應用程式將會移至正式版的 Lync Server 2013，而 Office Communications Server 2007 R2 的舊版集區和應用程式則就此停用。

