---
title: Lync Server 2013：新增自訂文字到立即訊息
TOCTitle: 新增自訂文字到立即訊息
ms:assetid: cabcc3ec-9d35-42ac-a403-e21b7d538c2c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398847(v=OCS.15)
ms:contentKeyID: 52056224
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中新增自訂文字到立即訊息

 

_**上次修改主題的時間：** 2013-02-20_

使用 **New-CSClientPolicy** 或 **Set-CSClientPolicy**Lync Server 管理命令介面 Cmdlet 搭配 IMWarning 參數，在每個 Lync 2013 立即訊息 (IM) 交談的開頭加上免責聲明或警告。

下列範例中的命令會在每次新的 IM 交談開始時，將安全性提醒新增至 \[交談\] 視窗的頂端：

    New-CsClientPolicy -Identity IMSecurityNotice -IMWarning 
    "Remember, security is everyone's responsibility. Keep it confidential."

使用 **Grant-CSClientPolicy** 將此新原則指派給使用者。如需詳細資訊，請參閱 Lync Server 管理命令介面 說明文件的 **New-CSClientPolicy** 和 **Grant-CSClientPolicy**。

