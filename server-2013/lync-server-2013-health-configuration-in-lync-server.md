---
title: Lync Server 2013 的健康情況設定
TOCTitle: Lync Server 2013 的健康情況設定
ms:assetid: c00a8c8e-c2d2-4557-8c42-211c7cc96550
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205234(v=OCS.15)
ms:contentKeyID: 49292191
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的健康情況設定

 

_**上次修改主題的時間：** 2015-03-09_

在執行 Lync Server 時遇到問題的系統管理員，可以從各種網站、Microsoft 知識庫文章和 Lync Server Resource Kit 工具獲得解決問題的方法。

由於 Lync Server 會被產品本身無法控制的許多因素所影響 (例如網路當機和硬體故障)，所以很明顯的，沒有辦法可以保證您在使用 Lync Server 2013 時永遠不會遇到問題。透過實施運作情況監控，系統管理員可以及早找出潛在問題，例如系統管理員可以使用 Lync Server 監控來識別趨勢和傾向。舉例來說，音訊/視訊會議數目穩定增加，可能代表需要增加容量，以免系統超載。

同樣的，系統管理員可以使用 System Center Operations Manager 來執行特定動作，例如當指定的事件發生時發出即時通知、執行綜合交易以主動測試系統等。Lync Server 中會使用綜合交易來確認使用者可以順利完成一般工作，例如登入系統、交換立即訊息，或撥打給位於公用交換電話網路 (PSTN) 的電話。例如，定期執行這些測試，可以讓您察覺使用者登入 Lync Server 時可能遇到的問題，讓您有機會及早修正問題，以免未來支援團隊會接到許多使用者無法連線的求助來電。透過以 System Center Operations Manager 執行這些綜合交易，系統管理員在每天 24 小時持續監控其 Lync Server 部署的例行工作中，只要在收到通知時進行回應，而不太需要做什麼其他動作。

> [!NOTE]  
> 對於 Lync Server 2013，System Center Operations Manager 的管理組件也能偵測可能對 Lync Server 造成不利影響的「外部」問題。例如，系統管理員可以在 Internet Information Services (IIS) 離線、Lync Server 電腦上的系統資源低於指定值，或 Lync Server 電腦遇到硬體故障時收到通知。



Lync Server 2013 中的運作情況設定是以 System Center Operations Manager 以及 Lync Server 管理組件的使用為基礎。這些管理組件包含一些新功能和增強功能，包括：

  - **從任何位置的案例可用性。** Lync Server 2010 管理組件引進以綜合交易監控使用者案例可用性的概念。在 Lync Server 2013 中，這些代理程式有更多綜合交易，並可從企業內各種位置執行、從企業外部的遠端地理位置執行、對分公司設備執行，以及對 Lync Server 2010 部署執行，以新增對舊版 Edge 部署的涵蓋範圍。

  - **綜合交易記錄檔。** 當綜合交易失敗時，系統管理員可以存取 HTML 記錄檔來判斷是哪些地方失敗。這包括去了解是哪個動作失敗、每個動作造成的延遲、用來執行測試的命令列，以及遇到的錯誤。

  - **提高通話可靠性涵蓋範圍。** Lync Server 2010 管理組件引進可靠性通知，以偵測會影響使用者音訊撥號的嚴重連線問題。Lync Server 2013 管理組件新增對對等立即訊息 (IM) 及其他基本會議功能的涵蓋範圍，以便擴大涵蓋範圍，同時降低雜音。

  - **相依性監控。** Lync Server 案例可能會因為各種外部因素 (如 IIS 離線、CPU 與記憶體資源有限以及磁碟問題) 而失敗。新的管理組件會檢查數項關鍵相依性，確保系統管理員注意到這些相依性的影響。

  - **增強版報告功能。** 有一組報告可協助系統管理員估計案例可用性、規劃容量，以及查看哪些元件遇到最多問題。

管理組件也包含各種可協助進行偵測及診斷的功能，讓您對於 Lync Server 部署運作情況有即時的了解。下表列出這些功能。

### 管理組件功能

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>綜合交易</p></td>
<td><p>可從各種位置執行的 Windows PowerShell Cmdlet，確定使用者案例 (如登入、目前狀態、IM 及會議) 已就緒，可供使用者運用。</p></td>
</tr>
<tr class="even">
<td><p>通話可靠性通知</p></td>
<td><p>這些資料庫查詢會尋找詳細通話記錄 (CDR)。這些記錄是由前端伺服器寫入，以反映使用者當時是否能連到通話，或是通話終止的原因。這些查詢會產生通知，表示有廣泛的使用者在使用對等通話或基本會議功能時遇到連線問題。</p></td>
</tr>
<tr class="odd">
<td><p>媒體品質通知</p></td>
<td><p>這些資料庫查詢會查看用戶端在每次通話結束時發佈的經驗品質 (QoE) 報告。這些查詢會產生通知，指出使用者在通話和會議期間可能會遇到不良媒體品質的案例。這些資料是以重要計量 (如封包延遲和遺失等這些已知直接跟通話品質有關的計量) 為基礎建立的。</p></td>
</tr>
<tr class="even">
<td><p>元件運作情況</p></td>
<td><p>個別伺服器元件會使用事件記錄和效能計數器發出通知。這些通知指出可能會嚴重影響一或多個使用者案例的失敗狀況。這些通知也能指出多各種其他失敗狀況，包括服務未執行、高失敗率、訊息高度延遲或連線問題。</p></td>
</tr>
<tr class="odd">
<td><p>相依性運作情況</p></td>
<td><p>造成失敗的原因有好幾種。管理組件現在會針對某些關鍵外部相依性，監控和收集可能指出嚴重問題的資料，包括 IIS 可用性、伺服器與處理程序的 CPU 和記憶體使用情形，以及磁碟計量。</p></td>
</tr>
</tbody>
</table>


系統發出的通知分為三大類別：

  - **高優先通知。** 這些通知指出會造成大群使用者面臨服務中斷的狀況。例如，因為 Lync Server 2013 已內建高可用性功能，所以單一機器上的某個元件故障並不是高優先通知。高優先通知所代表的是嚴重到必須「在半夜叫醒系統管理員」的問題。綜合交易偵測到的中斷以及服務 (例如音訊/視訊會議) 離線都符合高優先通知的資格。

  - **中優先通知。** 這些通知會指出影響一小群使用者的狀況，或指出通話品質降低。這包括元件故障、通話延遲建立或通話音訊品質降低等問題。此類通知會記取狀態，並指出問題的目前狀態。例如，假設您的通話建立時間超出通知臨界值，當通話建立時間回復正常時，System Center Operations Manager 中就會自動解決這些通知。這些通知的用意是要讓系統管理員在同一個工作天內加以查看。

  - **其他通知。** 這些是可能影響特定使用者或一小群使用者的元件所發出的通知。例如，通訊錄服務可能無法剖析某個使用者的 Active Directory 項目。這些通知的用意是要讓系統管理員在有空時再加以查看。

## 本節內容

  - [設定 Lync Server 以搭配 System Center Operations Manager 使用](lync-server-2013-configuring-lync-server-to-work-with-system-center-operations-manager.md)

  - [使用綜合交易的豐富記錄](lync-server-2013-using-rich-logging-for-synthetic-transactions.md)

  - [使用 Microsoft SQL Server 2008 R2 當成 System Center Operations Manager 資料庫](lync-server-2013-using-microsoft-sql-server-2008-r2-as-your-system-center-operations-manager-database.md)

