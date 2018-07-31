---
title: Lync Server 2013：Lync 用戶端視訊需求
TOCTitle: Lync 用戶端視訊需求
ms:assetid: 8f68f4c2-3194-487c-bd2f-fbe71ba8ad70
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688132(v=OCS.15)
ms:contentKeyID: 49890204
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的 Lync 用戶端視訊需求

 

_**上次修改主題的時間：** 2015-03-09_

本節說明 Lync 2013 視訊通話的視訊硬體支援，並說明如何判斷各種電腦、平板電腦和行動裝置組態的預期視訊品質。

## Windows 桌面和平板電腦視訊需求和功能

Lync 2013 引進了硬體加速，可以根據 H.264/MPEG-4 Part 10 進階音訊編碼標準來進行視訊編碼與解碼。此功能允許 CPU 時脈速度較低的電腦將較高解析度的視訊編碼與解碼。視訊硬體需求會根據所需的電腦組態和視訊解析度而不同。

## 視訊硬體需求


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用 DirectX 視訊加速 (DXVA) 的硬體加速 H.264 解碼</p></td>
<td><ul>
<li><p>圖形卡必須支援 DirectX 9.0，而且必須公開 DXVA2_ModeH264_VLD_NoFGT 解碼模式。</p></li>
<li><p>必須安裝最新的圖形卡驅動程式。</p></li>
</ul>
<div class="alert">

> [!NOTE]  
> 如需關於解碼模式的詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/p/?linkid=268530">http://go.microsoft.com/fwlink/p/?LinkId=268530</a> (可能為英文網頁)。


</div></td>
</tr>
<tr class="even">
<td><p>硬體加速的 H.264 編碼：晶片組需求</p></td>
<td><p>支援下列 Intel 硬體加速的視訊編碼解決方案：</p>
<ul>
<li><p>第二代和第三代 Intel HD Graphics 2000、2500、3000 及 4000 晶片組 (或更新版本)，以及整合的硬體視訊編碼器。必須安裝 Intel HD Graphics 驅動程式 15.28.9.2884 或包含下列項目的最新驅動程式。</p>
<ul>
<li><p>顯示驅動程式 9.17.10.2884 或最新的驅動程式</p></li>
<li><p>Hardware Media Foundation Transform (HMFT) 版本 3.12.10.31 或最新的 HMFT</p></li>
</ul></li>
</ul>
<p>支援下列 AMD 硬體加速視訊編碼解決方案 (需要 Lync Server 2013 CU1 更新)：</p>
<ul>
<li><p>AMD 視訊轉碼器引擎，數種圖形卡和 AMD A 系列加速處理器之整合式加速處理裝置皆有提供。必須安裝 AMD 視訊轉碼器引擎驅動程式 9.12.0.0 或以上版本。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>硬體加速的 H.264 編碼：相機需求</p></td>
<td><p>含有整合之 H.264 硬體編碼器的 USB 攝影機，該編碼器符合 USB 視訊類別 (UVC) 規格版本 1.5。</p>
<div class="alert">

> [!NOTE]  
> Lync 2013 在 Windows 8 或 Windows 8.1 支援 UVC 1.5 相機，其中包含對 UVC 1.5 的支援。因為 Windows 7 未包含對 UVC 1.5 的支援，所以 Lync 2013 會將 UVC 1.5 相機視為未包含硬體編碼支援的一般相機。


</div></td>
</tr>
<tr class="even">
<td><p>使用 DirectX 視訊加速 (DXVA) 的硬體加速 H.264 解碼</p></td>
<td><ul>
<li><p>圖形卡必須支援 DirectX 9.0，而且必須公開 DXVA2_ModeH264_VLD_NoFGT 解碼模式。</p></li>
<li><p>必須安裝最新的圖形卡驅動程式。</p></li>
</ul>
<div class="alert">

> [!NOTE]  
> 如需關於解碼模式的詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/p/?linkid=268530">http://go.microsoft.com/fwlink/p/?LinkId=268530</a> (可能為英文網頁)。


</div></td>
</tr>
<tr class="odd">
<td><p>硬體加速的 H.264 編碼：晶片組需求</p></td>
<td><p>支援下列 Intel 硬體加速的視訊編碼解決方案：</p>
<ul>
<li><p>第二代和第三代 Intel HD Graphics 2000、2500、3000 及 4000 晶片組 (或更新版本)，以及整合的硬體視訊編碼器。必須安裝 Intel HD Graphics 驅動程式 15.28.9.2884 或包含下列項目的最新驅動程式。</p>
<ul>
<li><p>顯示驅動程式 9.17.10.2884 或最新的驅動程式</p></li>
<li><p>Hardware Media Foundation Transform (HMFT) 版本 3.12.10.31 或最新的 HMFT</p></li>
</ul></li>
</ul>
<p>支援下列 AMD 硬體加速視訊編碼解決方案 (需要 Lync Server 2013 CU1 更新)：</p>
<ul>
<li><p>AMD 視訊轉碼器引擎，數種圖形卡和 AMD A 系列加速處理器之整合式加速處理裝置皆有提供。必須安裝 AMD 視訊轉碼器引擎驅動程式 9.12.0.0 或以上版本。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>硬體加速的 H.264 編碼：相機需求</p></td>
<td><p>含有整合之 H.264 硬體編碼器的 USB 攝影機，該編碼器符合 USB 視訊類別 (UVC) 規格版本 1.5。</p>
<div class="alert">

> [!NOTE]  
> Lync 2013 在 Windows 8 或 Windows 8.1 支援 UVC 1.5 相機，其中包含對 UVC 1.5 的支援。因為 Windows 7 未包含對 UVC 1.5 的支援，所以 Lync 2013 會將 UVC 1.5 相機視為未包含硬體編碼支援的一般相機。


</div></td>
</tr>
</tbody>
</table>


## 判斷 H.264 視訊編碼與解碼功能

一般而言，有四個主要因素可判斷特定電腦設定的編碼與解碼功能上限：

  - 使用 DXVA 支援硬體加速解碼

  - 支援硬體加速編碼

  - 實際核心數

  - Windows 體驗指數 (WEI)

Windows 系統評定工具 (WinSAT) 會判斷 WEI。當您執行 WinSAT 工具時，它會在電腦上的 %windir%\\Performance\\WinSAT\\DataStore 目錄中產生 Formal.Assessment XML 文件。此 XML 檔案包含下列兩種分數，這兩種分數在判斷編碼與解碼功能時特別重要：

  - VideoEncodeScore 表示電腦上以軟體為主的視訊編碼功能。

  - GraphicsScore 值表示電腦上硬體加速的編碼功能。

下列三個表格會針對不同的電腦類型，根據它們支援的硬體加速來說明編碼與解碼功能的上限。若解析度為 640x360 (含) 以上，支援的最大播放速率為每秒 30 個畫面 (fps)。若解析度低於 640x360，則支援的最大播放速率為 15 fps。

### 不含 DXVA 且不含硬體加速編碼器的電腦

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>可使用編碼器的解析度</th>
<th>可使用解碼器的解析度</th>
<th>需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>424x240</p></td>
<td><p>424x240 (如果是只會接收的案例，為 640x360 及 15fps)</p></td>
<td><p>1 核心且 VideoEncodeScore ≥ 4.0</p></td>
</tr>
<tr class="even">
<td><p>640x360</p></td>
<td><p>640x360</p></td>
<td><p>2 核心且 VideoEncodeScore ≥ 4.5</p></td>
</tr>
<tr class="odd">
<td><p>640x360</p></td>
<td><p>1280x720</p></td>
<td><p>2 核心且 VideoEncodeScore ≥ 4.5</p></td>
</tr>
<tr class="even">
<td><p>640x360</p></td>
<td><p>1920x1080</p></td>
<td><p>4 核心且 VideoEncodeScore ≥ 4.5</p></td>
</tr>
<tr class="odd">
<td><p>1280x720</p></td>
<td><p>1280x720</p></td>
<td><p>4 核心且 VideoEncodeScore ≥ 7.3</p></td>
</tr>
<tr class="even">
<td><p>1280x720</p></td>
<td><p>1920x1080</p></td>
<td><p>4 核心且 VideoEncodeScore ≥ 7.3</p></td>
</tr>
<tr class="odd">
<td><p>1920x1080</p></td>
<td><p>1920x1080</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="even">
<td><p>424x240</p></td>
<td><p>424x240 (如果是只會接收的案例，為 640x360 及 15fps)</p></td>
<td><p>1 核心且 VideoEncodeScore ≥ 4.0</p></td>
</tr>
<tr class="odd">
<td><p>640x360</p></td>
<td><p>640x360</p></td>
<td><p>2 核心且 VideoEncodeScore ≥ 4.5</p></td>
</tr>
<tr class="even">
<td><p>640x360</p></td>
<td><p>1280x720</p></td>
<td><p>2 核心且 VideoEncodeScore ≥ 4.5</p></td>
</tr>
<tr class="odd">
<td><p>640x360</p></td>
<td><p>1920x1080</p></td>
<td><p>4 核心且 VideoEncodeScore ≥ 4.5</p></td>
</tr>
<tr class="even">
<td><p>1280x720</p></td>
<td><p>1280x720</p></td>
<td><p>4 核心且 VideoEncodeScore ≥ 7.3</p></td>
</tr>
<tr class="odd">
<td><p>1280x720</p></td>
<td><p>1920x1080</p></td>
<td><p>4 核心且 VideoEncodeScore ≥ 7.3</p></td>
</tr>
<tr class="even">
<td><p>1920x1080</p></td>
<td><p>1920x1080</p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>


### 含 DXVA 但不含硬體加速編碼器的電腦

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>可使用編碼器的解析度</th>
<th>可使用解碼器的解析度</th>
<th>需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>424x240</p></td>
<td><p>1920x1080</p></td>
<td><p>1 核心且 VideoEncodeScore ≥ 3.0</p></td>
</tr>
<tr class="even">
<td><p>640x360</p></td>
<td><p>1920x1080</p></td>
<td><p>2 核心且 VideoEncodeScore ≥ 4.5</p></td>
</tr>
<tr class="odd">
<td><p>960x540</p></td>
<td><p>1920x1080</p></td>
<td><p>2 核心且 VideoEncodeScore ≥ 6.0</p></td>
</tr>
<tr class="even">
<td><p>1280x720</p></td>
<td><p>1920x1080</p></td>
<td><p>4 核心且 VideoEncodeScore ≥ 6.7</p></td>
</tr>
<tr class="odd">
<td><p>1920x1080</p></td>
<td><p>1920x1080</p></td>
<td><p>4 核心且 VideoEncodeScore ≥ 8.2</p></td>
</tr>
<tr class="even">
<td><p>424x240</p></td>
<td><p>1920x1080</p></td>
<td><p>1 核心且 VideoEncodeScore ≥ 3.0</p></td>
</tr>
<tr class="odd">
<td><p>640x360</p></td>
<td><p>1920x1080</p></td>
<td><p>2 核心且 VideoEncodeScore ≥ 4.5</p></td>
</tr>
<tr class="even">
<td><p>960x540</p></td>
<td><p>1920x1080</p></td>
<td><p>2 核心且 VideoEncodeScore ≥ 6.0</p></td>
</tr>
<tr class="odd">
<td><p>1280x720</p></td>
<td><p>1920x1080</p></td>
<td><p>4 核心且 VideoEncodeScore ≥ 6.7</p></td>
</tr>
<tr class="even">
<td><p>1920x1080</p></td>
<td><p>1920x1080</p></td>
<td><p>4 核心且 VideoEncodeScore ≥ 8.2</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> Windows 7 上的 WinSAT 分數最高為 7.9。因此，不含硬體加速編碼器之電腦的編碼功能僅可在 Windows 8 或 Windows 8.1 上達成，其 WinSAT 分數最高為 9.9。



### 含 DXVA 且含 Intel HD Graphics 硬體加速解碼器的電腦

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>可使用編碼器的解析度</th>
<th>可使用解碼器的解析度</th>
<th>需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1280x720</p></td>
<td><p>1920x1080</p></td>
<td><p>所有第二代和第三代的 Intel HD Graphics</p></td>
</tr>
<tr class="even">
<td><p>1920x1080</p></td>
<td><p>1920x1080</p></td>
<td><p>第二代和第三代的 Intel HD Graphics 且 GraphicsScore ≥ 5.0</p></td>
</tr>
<tr class="odd">
<td><p>1280x720</p></td>
<td><p>1920x1080</p></td>
<td><p>所有第二代和第三代的 Intel HD Graphics</p></td>
</tr>
<tr class="even">
<td><p>1920x1080</p></td>
<td><p>1920x1080</p></td>
<td><p>第二代和第三代的 Intel HD Graphics 且 GraphicsScore ≥ 5.0</p></td>
</tr>
</tbody>
</table>


## 行動裝置視訊功能

下表說明所支援行動裝置的最大視訊功能。如需有關行動裝置支援的詳細資訊，請參閱 [規劃 Lync Server 2013 中的行動用戶端](lync-server-2013-planning-for-mobile-clients.md) (規劃行動用戶端)。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>Windows Phone</th>
<th>iPhone 和 iPad</th>
<th>Android</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>H.264 編碼最大解析度</p></td>
<td><p>640x480</p></td>
<td><p>iPhone 4：192x144</p>
<p>iPad 和所有其他支援的 iPhone 模型：352x288</p></td>
<td><p>320x2401</p></td>
</tr>
<tr class="even">
<td><p>H.264 解碼最大解析度</p></td>
<td><p>640x480</p></td>
<td><p>iPhone 和 iPad：352x288</p></td>
<td><p>320x2401</p></td>
</tr>
<tr class="odd">
<td><p>H.264 編碼最大解析度</p></td>
<td><p>640x480</p></td>
<td><p>iPhone 4：192x144</p>
<p>iPad 和所有其他支援的 iPhone 模型：352x288</p></td>
<td><p>320x2401</p></td>
</tr>
<tr class="even">
<td><p>H.264 解碼最大解析度</p></td>
<td><p>640x480</p></td>
<td><p>iPhone 和 iPad：352x288</p></td>
<td><p>320x2401</p></td>
</tr>
</tbody>
</table>


1若裝置具備使用任何 8x60 晶片組的 Qualcomm Snapdragon S3 或 S4 處理器Android，則支援傳送和接收為 640x480 解析度。

