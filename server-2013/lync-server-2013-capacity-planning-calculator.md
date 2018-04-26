---
title: 使用 Lync Server 2013 容量規劃計算器
TOCTitle: 使用 Lync Server 2013 容量規劃計算器
ms:assetid: e86c1f05-1393-408a-9549-6001572ec50d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362852(v=OCS.15)
ms:contentKeyID: 56269163
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 Lync Server 2013 容量規劃計算器

 

_**上次修改主題的時間：** 2013-11-21_

Microsoft® Lync™ Server 2013 容量規劃計算器可從網路進行下載：<http://www.microsoft.com/en-us/download/details.aspx?id=36828>。此計算器的設計用途，在於協助您根據組織中所啟用的使用者數與通訊型式來判定伺服器需求。在您輸入組織的設定檔後，計算器將提供相關建議以協助您規劃拓撲。

計算器的建議僅限規劃用途。您需要實際的負載模擬，以確保 Lync Server 2013 妥善佈建。若要在模擬負載下執行壓力測試，請使用 [Lync Server 2013 壓力和效能工具](http://go.microsoft.com/fwlink/?linkid=282724) (英文)。

決定好要為您的使用者啟用的使用者設定檔與型式後，即可使用計算器規劃所需的伺服器、記憶體以及頻寬數。此版本的計算器並無提供磁碟 I/O 需求的指南。

此計算器可作為 [Microsoft Lync Server](http://go.microsoft.com/fwlink/?linkid=282725) 與 [Microsoft Lync Server](lync-server-2013-planning.md) 的輔助工具。使用計算器前，請先詳閱指南內容，並且使用規劃工具建立出建議的拓撲。

如果能夠透過計算器取得精確詳盡的特定使用者設定檔資訊，將可為您帶來莫大助益。例如，啟用語音功能的使用者百分比、每位使用者每小時的平均通話數、通話持續時間，以及會議中同時連線的使用者百分比等因素，均會對伺服器需求造成明顯差異。若要從計算器中得出精確的建議值，您必須提供精確的資訊。

## 使用容量計算器

此計算器採用 Microsoft Excel® 試算表。橘色儲存格代表供您輸入的部分。預設值也已輸入 (單一集區中有 80,000 名使用者，前端伺服器十二台)，但您可根據組織需求變更這些數值。

使用狀況模型包含下列區塊。若要計算您的容量需求，請按照說明輸入資料：

**立即訊息與目前狀態**

  - 在 \[Number of Users (使用者數)\] 底下，輸入將同時登入的使用者數。此數值通常為佈建使用者總數的 80%。在大部分情況下，100% 的同步使用者將啟用 IM 與目前狀態。預設值為 80,000。

  - 連絡人清單中的平均連絡人數代表我們在驗證您的系統需求時所採用的連絡人數。此數值無法變更。

**企業語音**

  - 在 \[Users enabled for Enterprise Voice (啟用企業語音的使用者)\] 中，輸入您的使用者中啟用企業語音的百分比。預設值為 60%。

  - 在 \[Average number of calls per user per hour (peak) (每名使用者每小時的平均通話數 (尖峰))\] 中，輸入您預期每名使用者在尖峰負載期間平均每小時參與的通話數。預設值為 4。

  - 在 \[Percentage of calls that use media bypass (使用媒體旁路的通話百分比)\] 中，輸入由使用者撥號且將執行中繼伺服器旁路作業的通話百分比。預設值為 65%。

  - 在 \[Percentage of voice users involved in UC-PSTN calls (UC-PSTN 通話涉及之語音使用者百分比)\] 中，輸入組織中屬於 UC-PSTN 通話的百分比。預設值為 60%

  - \[Percentage of voice users involved in UC-UC calls (UC-UC 通話涉及之語音使用者百分比)\] 會顯示啟用企業語音且僅啟用 UC-UC 通話的使用者百分比。此數字是根據您在 \[Percentage of voice users enabled for UC-PSTN calls (啟用 UC-PSTN 通話之語音使用者百分比)\] 中所輸入的資料計算得出。

**會議**

  - 在 \[Percentage of users in concurrent conferences,(同時會議中的使用者百分比)\] 中，輸入同時參與會議的使用者百分比。預設值為 5%。

  - 在 \[Percentage of conferences with group IM only (no voice) 僅有群組 IM 的會議百分比 (無語音)\] 中，輸入僅會涉及立即訊息的會議百分比；也就是未包含音訊的會議。預設值為 10%。

  - 在 \[Percentage of users using dial-in conferencing (使用撥入式會議的使用者百分比)\] 中，輸入參與將使用撥入式會議功能之會議的同時參與者百分比。預設值為 15%。

  - 在 \[Percentage of conferences using voice (使用語音的會議百分比)\] 中，輸入將包含音訊元件的會議百分比。
    
      - 若是 20% 的語音會議亦將包括一般視訊，請選取 \[Including video (no Multi View) (包括視訊 (無多重檢視)\] 核取方塊。
    
      - 若是 20% 的會議亦將包括多重視窗視訊，請選取 \[Including Multi View (包括多重視窗)\] 核取方塊。
    
      - 若是 50% 的語音會議亦將包括應用程式共用，請選取 \[Including application sharing (包括應用程式共用)\] 核取方塊。
    
      - 若是 20% 的語音會議包括資料上傳，例如 Microsoft PowerPoint® 簡報，請選取 \[Including web conferencing (包括網路會議)\] 核取方塊。

**行動性**

  - 在 \[Percentage of users enabled for Mobility (啟用行動性的使用者百分比)\] 中，輸入將使用行動裝置連線至 Lync Server 的使用者百分比。預設值為 40%。

在您輸入所有必要資訊後，容量計算器即會評估您的需求。黃色儲存格會根據 Lync Server 2013 的 \[效能\] 索引標籤中所執行的測試，針對 CPU、記憶體以及頻寬需求提供計算值。這些數值乃是作為參考準則提供，並非每個搭配組合均經過測試與驗證。下列數值均為計算得出的數值；

  - \[Front End CPU (前端 CPU\]：在整個負載是由單一前端伺服器處理且伺服器規格與用於 Microsoft 測試之伺服器規格相同時，CPU 的使用量百分比

  - \[Network in Mbps (網路 (Mbps))\]：相對工作負載的每秒頻寬需求 (Mbps)。

  - \[Memory in GB (記憶體 (GB))\]：相對工作負載的所需記憶體 (GB)。

綠色儲存格會針對您所輸入的使用狀況模型提供建議值。

  - \[Total Front End Servers (前端伺服器總數)\]：所需的實體伺服器數是以執行 Lync Server 2013 的專用伺服器計算，伺服器具備雙處理器，十六核心，2,260 Megacycle。

  - 請注意，啟用超執行緒是建議採行的作法，且已證實可改善支援音訊/視訊之伺服器的效能。

  - \[Edge Servers (Edge Server)\]：根據所有同時使用者有 30% 透過 Edge Server 進行通訊而計算得出的所需 Edge Server 數。此百分比值無法在計算器中進行變更。

  - \[Archiving/Call Detail Recording/Quality of Experience services Store (封存/通話詳細資訊記錄/經驗品質服務存放區)\]：組織啟用封存或監控功能時所需的存放區數。

  - \[Back End Database Server Required (Pools Required) (所需後端資料庫伺服器 (所需集區))\]：支援所選工作負載的所需後端資料庫伺服器數。

此外，您在 \[Total Front End Servers (前端伺服器總數)\] 的下行中，將可找到更多針對所有規劃的工作負載總量所提供之伺服器與網路負載的相關資訊。

  - \[Average CPU Load (平均 CPU 負載)\]：各台前端伺服器的平均 CPU 使用量。

  - \[Network in Mbps (網路 (Mbps))\]：支援所輸入之使用狀況模型的所需頻寬配置。

  - \[Memory in GB (記憶體 (GB))\]：各台前端伺服器的所需記憶體 (GB)。

## 調整您的處理器

試算表中的所有 CPU 使用數據假定各台伺服器均有一個雙處理器，十六核心且 2.26 GHz，記憶體至少 32 GB，8 顆以上的 10,000-RPM 硬碟，至少 72 GB 的可用空間。

若是您的伺服器採用其他處理器，您可以調整該數據以配合您的硬體條件。

