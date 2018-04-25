---
title: 重設通話許可控制
TOCTitle: 重設通話許可控制
ms:assetid: 5873f56c-f3d6-4d73-beea-c9f37d5077f6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688064(v=OCS.15)
ms:contentKeyID: 49890078
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 重設通話許可控制

 

_**上次修改主題的時間：** 2012-10-11_

如果 Lync Server 2010前端集區裝載了通話許可控制 (CAC)，則您必須先將 CAC 裝載移至 Lync Server 2013 集區，才能移除 Lync Server 2010前端集區。

## 重設 CAC

1.  開啟 拓撲產生器。

2.  以滑鼠右鍵按一下網站節點，然後按一下 **\[編輯屬性\]** 。

3.  在 **\[通話許可控制設定\]** 下方，確定已選取 **\[啟用通話許可控制\]** 。

4.  在 **\[執行通話許可控制 (CAC) 的前端集區\]** 下方，選取要裝載 CAC 的 Lync Server 2013 集區，然後按一下 **\[確定\]** 。

5.  發行拓撲。

