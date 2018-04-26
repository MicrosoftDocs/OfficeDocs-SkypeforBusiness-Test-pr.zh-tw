---
title: 在 Lync Server 2013 中為立即訊息 (IM) 設定檔案傳輸和 URL 篩選
TOCTitle: 在 Lync Server 2013 中為立即訊息 (IM) 設定檔案傳輸和 URL 篩選
ms:assetid: 115a1a2c-599f-474c-a063-52f7144b5246
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520952(v=OCS.15)
ms:contentKeyID: 49290127
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中為立即訊息 (IM) 設定檔案傳輸和 URL 篩選

 

_**上次修改主題的時間：** 2012-11-01_

智慧型 IM 篩選器工具有助於保護您的 Lync Server 2013 部署，防止最常見形式之病毒的擴散，並且將對使用者經驗的影響降至最低。使用智慧型 IM 篩選器可以設定篩選器，以封鎖來自企業防火牆外部之不明端點的來路不明或潛在有害的立即訊息。您可以指定用來判斷所應封鎖項目的條件，藉以設定篩選器，例如立即訊息中包含具有特定首碼的超連結與具有特定副檔名的檔案。

智慧型 IM 篩選器提供下列功能：

  - 增強型 URL 篩選。

  - 增強型檔案傳輸篩選。

智慧型 IM 篩選器的設定包括：

  - 設定 URL 篩選。

  - 設定檔案傳輸篩選。

## 篩選選項套用至立即訊息的方式

在您部署智慧型 IM 訊息篩選器工具之前，必須先了解在 Lync Server 2013 伺服器之間路由訊息時，如何套用篩選選項。無論伺服器位於單一組織內，或是涵蓋多個組織，套用這些篩選選項的方式是一樣的。這種一致性適用於自訂通知和警告文字插入訊息及跨伺服器傳送的方式。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>立即訊息篩選器會增加訊息中處理 URL 所需的 CPU 資源量。這種對 CPU 需求的增加情形也會影響 Lync Server 的效能。</td>
</tr>
</tbody>
</table>


在 Lync Server 控制台中使用 \[IM 和目前狀態\] 群組中的「」URL 篩選器」頁面，可讓您封鎖部分或所有超連結或是設定警告。當您選擇 \[超連結首碼\] 選項 \[傳送警告訊息\] 時，即會在包含超連結的立即訊息開頭處插入警告。

當立即訊息從一部伺服器傳送到另一部伺服器時，會套用下列一般方針：

  - 如果伺服器封鎖立即訊息 (由於您在 **\[URL 篩選器\]** 頁面上選取了 **\[封鎖含有副檔名的 URL\]** 核取方塊，或選擇了 **\[超連結首碼\]** 選項 **\[封鎖超連結\]**)，則會將錯誤訊息傳回至用戶端。後續的伺服器將不會收到此立即訊息。

  - 如果伺服器 (Server1) 將警告新增至包含作用中超連結的立即訊息中，收到此立即訊息的後續伺服器 (Server2) 仍可以依據該立即訊息中出現的這個作用中超連結來採取不同的動作，並封鎖該立即訊息或新增警告。如果 Server2 設定為僅新增此 URL 的警告，便會移除之前由 Server1 新增的警告，而在 Server2 上所設定的警告將會新增至該立即訊息的開頭處。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您是在混合環境中執行 Lync Server 2013，則 Live Communications Server 2005 SP1 將是使用智慧型 IM 篩選器應用程式所需的最低版本。不具 SP1 的 Live Communications Server 2005 不支援智慧型 IM 篩選器。</td>
</tr>
</tbody>
</table>


## URL 篩選

URL 可根據其超連結首碼受到篩選。以下是有效首碼的範例：

  - www\*.

  - ftp.

  - http:

如果您未設定立即訊息篩選器來執行任何 URL 篩選，則立即訊息中所包含的所有 URL 都會以原狀通過伺服器。如果您設定立即訊息篩選器來執行 URL 篩選，則立即訊息中的 URL 都會根據您在 **\[編輯 URL 篩選器\]** 或 **\[新增 URL 篩選器\]** 對話方塊中所選取的選項受到篩選。

  - **啟用 URL 篩選器**   此選項可對全域部署或您所選取的網站啟用 URL 篩選。

  - **封鎖含有副檔名的 URL**   任何作用中的內部網路或網際網路 URL 所含之檔案若具有 **\[編輯檔案篩選器\]** 對話方塊中的 **\[要封鎖的副檔名\]** 下所列的副檔名，都會遭到立即訊息篩選器封鎖。封鎖 URL 時，系統會對傳送者顯示錯誤訊息。選取此選項時，其優先順序將高於所有針對 **\[要封鎖的副檔名\]** 下所定義的任何副檔名而設定的其他篩選選項。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>副檔名的篩選僅限於標準的檔案名稱。內嵌在其他名稱中的副檔名可能篩選不出來。</td>
    </tr>
    </tbody>
    </table>


若要設定如何處理立即訊息交談中的超連結，請選取下列位於 \[超連結首碼\] 下方的其中一個選項：

  - **不要篩選**   訊息中的 URL 會傳送過伺服器。選擇此選項時，會出現 **\[允許訊息\]** 方塊。在 **\[允許訊息\]** 方塊中，請指定您要在每個包含超連結的立即訊息開頭處插入的通知。此通知最多可包含 65535 個字元。

  - **封鎖超連結**   傳送的立即訊息若包含作用中超連結，即會遭 Lync Server 封鎖，並對傳送者顯示錯誤訊息。

  - **傳送警告訊息**   Lync Server 會允許立即訊息中的作用中超連結，但會同時附上警告。選擇此選項時，會出現 \[警告訊息\] 方塊。在 \[警告訊息\] 方塊中，您必須輸入要在包含有效超連結的立即訊息中隨附的警告。例如，此警告可指出點選不明連結的潛在風險，或提及您組織的相關原則與需求。此警告最多可包含 65535 個字元。

選取 **\[封鎖超連結\]** 或 **\[傳送警告訊息\]** 時，可用的選項如下：

  - **排除近端內部網路超連結**   立即訊息篩選器只會封鎖網際網路 URL。內部網路內各位置的 URL 都會以原狀通過伺服器。但可通過執行 Lync Server 之個別伺服器的內部網路 URL，取決於哪些類型的本機網站會被視為其內部網路區域的一部分。若要檢查伺服器的內部網路區域設定，請參閱＜[修改預設 URL 篩選器](lync-server-2013-modify-the-default-url-filter.md)＞中的＜若要在 Internet Explorer 中設定您的內部網路設定＞程序。

  - **篩選這些超連結首碼**   若要選擇您要封鎖的首碼，請按一下 **\[選取\]**，然後在 **\[選取超連結首碼\]** 中，將首碼新增至 **\[超連結首碼\]** 清單中。
    
    除了 **href** 以外的所有首碼都必須以點或冒號結尾，或是以星號接著點為結尾。有效首碼可以包含有效 URL 字元組中的任何字元，但星號 (\*) 除外。有效的 URL 字元集為：\#\*+/0123456789=@ABCDEFGHIJKLMNOPQRSTUVWXYZ^\_\` abcdefghijklmnopqrstuvwxyz|~

## 檔案傳輸篩選

檔案傳輸篩選對立即訊息與會議都會有影響。對於會議，這些設定會影響 Office Live Meeting 2007 用戶端中的講義功能及多媒體播放功能。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 也提供檔案傳輸設定選項。除了 Lync Server 中可用的用戶端控制項以外，另外也提供此伺服器端選項。</td>
</tr>
</tbody>
</table>


當您在 Office Live Meeting 2007 用戶端中使用講義功能，或使用各種檔案類型的多媒體播放功能時，您可以篩選立即訊息交談期間的檔案傳輸。您可以設定下列選項以控制檔案傳輸：

  - **啟用檔案篩選器**   此選項可對全域部署或您所選取的網站啟用檔案篩選。
    
    當您啟用檔案篩選器時，您可以在 **\[檔案傳輸\]** 中選擇下列其中一個選項：
    
      - **封鎖特定檔案類型**   您透過指定要封鎖的副檔名清單，以指定伺服器所要篩選的檔案傳輸要求。清單中的項目可以包含所有標準字元，但是不可包含萬用字元 (\*)。Office Live Meeting 2007 用戶端中會啟用講義功能，但是無法上傳或下載任何具有此副檔名的檔案。如果您在 **\[URL 篩選器\]** 索引標籤上所列的 URL 篩選器設定上選取 **\[封鎖含有副檔名的 URL\]** 核取方塊，URL 篩選器即會使用這份相同清單封鎖包含這些副檔名的作用中超連結。若要選擇您要封鎖的檔案類型，請按一下 **\[選取\]**，然後在 **\[選取檔案類型\]** 中，將副檔名新增至 **\[選取的副檔名\]** 清單中。
    
      - **全部封鎖**   伺服器會捨棄所有包含檔案傳輸要求的立即訊息，並將錯誤訊息傳回給發出要求的傳送者。Office Live Meeting 2007 用戶端的講義功能也會停用。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>副檔名的篩選僅限於標準的檔案名稱。內嵌在其他名稱中的副檔名可能篩選不出來。</td>
</tr>
</tbody>
</table>


## 本節內容

  - [修改預設檔案傳輸篩選器](lync-server-2013-modify-the-default-file-transfer-filter.md)

  - [在特定的站台建立新檔案傳輸篩選器](lync-server-2013-create-a-new-file-transfer-filter-for-a-specific-site.md)

  - [修改預設 URL 篩選器](lync-server-2013-modify-the-default-url-filter.md)

  - [在 IM 交談中建立處理超連結的新 URL 篩選器](lync-server-2013-create-a-new-url-filter-to-handle-hyperlinks-in-im-conversations.md)

## 請參閱

#### 其他資源

[在 Lync Server 2013 中管理 IM 及顯示狀態設定](lync-server-2013-managing-im-and-presence-settings.md)

