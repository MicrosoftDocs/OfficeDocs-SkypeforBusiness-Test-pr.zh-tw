---
title: 刪除現有的 CDR 組態設定集合
TOCTitle: 刪除現有的 CDR 組態設定集合
ms:assetid: 8ebf5da8-c0fc-498c-8d85-527d3be8479a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688128(v=OCS.15)
ms:contentKeyID: 49890201
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除現有的 CDR 組態設定集合

 

_**上次修改主題的時間：** 2013-02-23_

詳細通話記錄 (CDR) 可讓您追蹤對等立即訊息工作階段、Voice over Internet Protocol (VoIP) 電話通話以及會議通話的使用情形。這項使用資料包括撥號方、收話方、通話時間及通話時間長度等資訊。

當您安裝 Microsoft Lync Server 2013 時，即會為您建立 CDR 組態設定的單一全域集合。系統管理員也可以選擇建立可套用至個別網站的自訂設定集合。根據設計，在網站範圍進行的設定優先順序高於在全域範圍進行的設定。如果您刪除網站範圍的設定，則在該網站中將使用全域設定來管理 CDR。

請注意，您也可以「刪除」全域設定。但是，全域設定將不會實際移除，而是將該集合中的所有屬性重設為預設值。例如，預設會在 CDR 組態設定的集合中啟用清除功能。假設您修改全域設定來停用清除功能。如果您稍後刪除全域設定，所有的內容都將重設為其預設值。在此情況下，這表示將再次啟用清除功能。

您可以使用 Lync Server 控制台或 [Remove-CsCdrConfiguration](remove-cscdrconfiguration.md) Cmdlet 來移除 CDR 組態設定。

## 使用 Lync Server 控制台移除 CDR 組態設定

1.  在 Lync Server 控制台中，按一下 \[監控和封存\]。

2.  在 \[詳細通話記錄\] 索引標籤中，選取一或多個要移除的 CDR 設定集合。若要選取多個集合，請按一下第一個集合、按住 Ctrl 鍵，然後按一下其他集合。

3.  按一下 \[編輯\]，然後按一下 \[刪除\]。

4.  在 \[Lync Server 控制台\] 對話方塊中，按一下 \[確定\]。

## 使用 Lync Server 管理命令介面 Cmdlet 移除 CDR 組態設定

您可以使用 Windows PowerShell 和 **Remove-CsCdrConfiguration** Cmdlet 來刪除詳細通話記錄組態設定。此 Cmdlet 可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 移除特定的 CDR 組態設定集合

  - 此命令會移除套用至 Redmond 網站的 CDR 組態設定：
    
        Remove-CsCdrConfiguration -Identity "site:Redmond"

## 移除所有套用至網站範圍的 CDR 組態設定

  - 此命令會移除所有套用至網站範圍的 CDR 組態設定：
    
        Get-CsCdrConfiguration -Filter "site:*" | Remove-CsCdrConfiguration

## 移除所有停用詳細通話記錄的 CDR 組態設定

  - 此命令會移除所有已停用 \[詳細通話記錄\] 的 CDR 組態設定：
    
        Get-CsCdrConfiguration | Where-Object {$_.EnableCDR -eq $False} | Remove-CsCdrConfiguration

如需詳細資訊，請參閱適用於 [Remove-CsCdrConfiguration](remove-cscdrconfiguration.md) Cmdlet 的說明主題。

