---
title: Lync Server 2013：定義正規化規則
TOCTitle: 定義正規化規則
ms:assetid: ed31d56c-00b5-4f72-bd9f-beb4100d441f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399071(v=OCS.15)
ms:contentKeyID: 49292730
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中定義正規化規則

 

_**上次修改主題的時間：** 2014-04-22_

Lync Server 2013 正規化規則使用 .NET Framework 規則運算式來將撥出的電話號碼轉譯成 E.164 格式；換句話說，正規化規則會擷取使用者所撥打的電話號碼並將該號碼轉換為 Lync Server 內部使用的格式。每個撥號對應表都必須指派一或多個正規化規則。

如需有關正規化規則的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的撥號對應表和正規化規則](lync-server-2013-dial-plans-and-normalization-rules.md)＞。

如需如何撰寫規則運算式的詳細資訊，請參閱＜.NET Framework 規則運算式＞，網址為 [http://go.microsoft.com/fwlink/?linkid=140927\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=140927%26clcid=0x404)。

您可以使用下列任一種方法定義或編輯正規化規則：

  - 使用 **\[建置正規化規則\]** 工具指定開頭數字、長度、要移除的數字和要加入的數字的值，然後讓 Lync Server 控制台自動產生對應的比對模式和轉譯規則。

  - 手動撰寫規則運算式來定義符合模式和轉譯規則。

## 本章節內容

  - [在 Lync Server 2013 中使用 \[建置正規化規則\] 建立或修改正規化規則](lync-server-2013-create-or-modify-a-normalization-rule-by-using-build-a-normalization-rule.md)

  - [在 Lync Server 2013 中手動建立或修改正規化規則](lync-server-2013-create-or-modify-a-normalization-rule-manually.md)

## 請參閱

#### 工作

[在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)  
[在 Lync Server 2013 中修改撥號對應表](lync-server-2013-modify-a-dial-plan.md)

