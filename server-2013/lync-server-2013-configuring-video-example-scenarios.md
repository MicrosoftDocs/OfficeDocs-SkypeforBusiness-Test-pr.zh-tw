---
title: 設定視訊範例案例
TOCTitle: 設定視訊範例案例
ms:assetid: da0d61a2-7ac4-4562-bf6a-18473a29acb2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205297(v=OCS.15)
ms:contentKeyID: 49292491
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定視訊範例案例

 

_**上次修改主題的時間：** 2015-03-09_

Lync 2013 新增視訊功能，支援 1920 x 1080 全彩高畫質 (HD) 視訊與圖庫檢視視訊。根據客戶資料的測量值顯示，和 Lync 2010 相比，一般視訊頻寬只有些微提升，但最大視訊資料流頻寬由於支援全彩 HD 而有所提升 (如需詳細資訊，請參閱＜[媒體流量的網路頻寬需求](lync-server-2013-network-bandwidth-requirements-for-media-traffic.md)＞中的＜媒體流量網路使用方式＞一節)。因此，管理員可能會希望限制特定使用者的視訊頻寬 (例如，分公司網路容量較少的使用者)，以及儘可能確保其他使用者能有最佳的視訊品質 (例如高階主管)。

下表提供建議設定的清單，用於設定適合不同網路容量的視訊。這些設定將限制某些使用者案例不能傳送和接收解析度較高的視訊 (請參閱最右欄)。由於最大接收網路頻寬很低，最小值設定將導致圖庫視訊無法使用。

### 建議的視訊設定

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>-</th>
<th>AllowMultiView</th>
<th>EnableMultiViewJoin</th>
<th>VideoBitRateKB</th>
<th>TotalReceiveVideoBitRateKB</th>
<th>預期會有良好視訊品質的視訊解析度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>最佳</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
<td><p>8000</p></td>
<td><p>8000</p></td>
<td><p>對等：最高 1920 x 1080 的視訊解析度</p>
<p>圖庫檢視：最多兩個 1920 x 1080 的視訊，或多個解析度較小的視訊</p></td>
</tr>
<tr class="even">
<td><p>良好</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
<td><p>2500</p></td>
<td><p>2500</p></td>
<td><p>對等：最高 1280 x 720 的視訊解析度</p>
<p>圖庫檢視：最多五個 640 x 360 解析度的視訊</p></td>
</tr>
<tr class="odd">
<td><p>中等</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
<td><p>1000</p></td>
<td><p>1000</p></td>
<td><p>對等：最高 960 x 540 的視訊解析度</p>
<p>圖庫檢視：最多五個 424 x 240 解析度的視訊</p></td>
</tr>
<tr class="even">
<td><p>最小值</p></td>
<td><p>True</p></td>
<td><p>False</p></td>
<td><p>350</p></td>
<td><p>350</p></td>
<td><p>對等：最高 424 x 240 的視訊解析度</p>
<p>圖庫檢視：無法使用</p></td>
</tr>
</tbody>
</table>


您可以使用上表來為組織中的某些使用者部署新的 HD 視訊與圖庫檢視的視訊會議功能，同時允許其他人使用不同的視訊解析度。

在下列範例中，管理員以最高視訊品質提供的新視訊功能，只限高階主管使用。對於網路容量低的遠端分公司員工，只會部署上表中的最小值設定。對於所有其他員工，則會部署上表中的「良好」設定。

為了向高階主管提供新的功能，管理員建立一個名為 ExecutiveVideo 的會議原則。此會議原則的設定如下：

  - VideoBitRateKB 設定為 8000 Kbps

  - TotalReceiveVideoBitRateKB 設定為 8000 Kbps

  - AllowMultiview 設定為 True

  - EnableMultiviewJoin 設定為 True

對於分公司的員工，管理員建立一個名為 BranchOfficeVideo 的會議原則。此會議原則的設定如下：

  - VideoBitRateKB 設定為 350 Kbps

  - TotalReceiveVideoBitRateKB 設定為 350 Kbps

  - AllowMultiview 設定為 True

  - EnableMultiviewJoin 設定為 False

對於所有其他員工，管理員建立一個名為 StandardVideo 的會議原則。此會議原則的設定如下：

  - VideoBitRateKB 設定為 2500 Kbps

  - TotalReceiveVideoBitRateKB 設定為 2500 Kbps

  - AllowMultiview 設定為 True

  - EnableMultiviewJoin 設定為 True

管理員會將會議原則指派給使用者，如下：

  - 將 ExecutiveVideo 會議原則指派給高階主管。

  - 將 BranchOfficeVideo 會議原則指派給分公司的所有員工。

  - 將 StandardVideo 會議原則指派給所有其他員工。

上述的會議原則指派產生下列使用者體驗：

  - 任何使用者召集的所有會議均支援圖庫檢視，但分公司員工無法體驗圖庫檢視。

  - 對於任何雙方或多方會議，只要配備的硬體與網路連結可支援，高階主管就可以傳送 1920 x 1080 全彩 HD 視訊，其他參與者用戶端亦可接收 1920 x 1080 全彩 HD 視訊。

  - 在雙方或多方會議中，非高階主管的員工體驗的解析度低於高階主管，但仍屬良好解析度。

  - Lync 顯示預設的視訊視窗大小時，分公司的員工在雙方通話時將有良好的視訊品質；不過，如果將 Lync 視窗放大成全螢幕，並不會增加視訊解析度。對於多方會議，分公司員工只會看到一個作用中視訊。

