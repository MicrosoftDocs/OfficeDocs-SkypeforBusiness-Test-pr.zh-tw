---
title: Lync Server 2013 中的代表號顯示方式
TOCTitle: Lync Server 2013 中的代表號顯示方式
ms:assetid: cf6c6af5-3418-411e-a50b-7a9cf8e100d4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721892(v=OCS.15)
ms:contentKeyID: 49890321
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的代表號顯示方式

 

_**上次修改主題的時間：** 2012-09-21_

使用 Lync Server 2010，受話方的電話號碼 (也就是所撥打的電話號碼) 可以從 E.164 格式轉譯為「主幹同儕節點」 (也就是相關的閘道、專用交換機 (PBX) 或 SIP 主幹) 所需的本地撥號格式。若要這樣做，您必須定義一或多個轉譯規則，先轉譯要求 URI 後，再路由至主幹同儕節點。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>將一個或多個轉譯規則與企業語音主幹組態建立關聯的功能，主要是在主幹同儕節點上設定轉譯規則的「替代方法」。如果您已在主幹同儕節點上設定轉譯規則，請不要讓轉譯規則與企業語音主幹組態建立關聯，因為兩種規則可能會衝突。</td>
</tr>
</tbody>
</table>


您可以使用下列任何一種方法建立或修改轉譯規則：

  - 使用 \[建置轉譯規則\] 工具來指定開頭數字、長度、移除的數字和增加的數字適用的值，然後讓 Lync Server 控制台 自動產生對應的比對模式和轉譯規則。

  - 手動撰寫規則運算式來定義比對模式和轉譯規則。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需如何撰寫規則運算式的詳細資訊，請參閱＜.NET Framework 規則運算式＞，網址為：<a href="http://go.microsoft.com/fwlink/?linkid=140927%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=140927&amp;clcid=0x404</a>。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [使用組建轉譯規則工具建立或修改轉譯規則](lync-server-2013-create-or-modify-a-translation-rule-by-using-the-build-a-translation-rule-tool.md)

  - [手動建立或修改轉譯規則](lync-server-2013-create-or-modify-a-translation-rule-manually.md)

## 請參閱

#### 概念

[Lync Server 2013 中的來電顯示呈現方式](lync-server-2013-caller-id-presentation.md)

