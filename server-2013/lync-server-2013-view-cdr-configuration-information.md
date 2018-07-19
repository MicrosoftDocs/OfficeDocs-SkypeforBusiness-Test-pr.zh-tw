---
title: 檢視 CDR 設定資訊
TOCTitle: 檢視 CDR 設定資訊
ms:assetid: 77bd553f-da89-4c84-a5d0-2f7e91d04383
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688096(v=OCS.15)
ms:contentKeyID: 49890121
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視 CDR 設定資訊

 

_**上次修改主題的時間：** 2013-02-23_

詳細通話記錄 (CDR) 讓您能夠追蹤點對點即時訊息工作階段、Voice over Internet Protocol (VoIP) 電話通話，以及會議通話之類的使用狀況。這個使用狀況資料包含有關通話者雙方身分、通話時間以及通話時間長度的資訊。

當您安裝 Microsoft Lync Server 2013 時，系統將為您建立一個 CDR 組態設定的單一全域集合。系統管理員也可以選擇建立自訂的設定集合，以套用於個別網站。藉由使用 Lync Server 控制台或 [Get-CsCdrConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsCdrConfiguration) Cmdlet，您可以檢視組織所使用的 CDR 組態設定。

## 使用 Lync Server 控制台檢視 CDR 組態資訊。

1.  在 Lync Server 控制台中，按一下 **\[監控與封存\]**。

2.  您所有 CDR 組態設定的清單將在 **\[詳細通話記錄\]** 索引標籤中顯示；在每一個設定集合中，您將會看到 **\[名稱\]** 集合；無論是否啟用 CDR (**CDR** 屬性)；無論是否啟用清除 (**CDR purging** 屬性)。若要檢視有關集合的詳細資訊，請在該集合按兩下滑鼠，或選取合適的集合，按一下 **\[編輯\]**，然後按一下 **\[顯示詳細資訊\]**。請記住，您一次只能檢視單一 CDR 組態設定集合的詳細資訊。

## 使用 Lync Server 管理命令介面 Cmdlet 檢視 CDR 組態資訊

您也可以使用 Lync Server 管理命令介面與 Get-CsCdrConfiguration Cmdlet 檢視 CDR 組態設定。您可以從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段來執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視 CDR 組態資訊

  - 若要檢視有關 CDR 組態設定的資訊，請在 Lync Server 管理命令介面鍵入下列指令，然後按下 ENTER 鍵：
    
        Get-CsCdrConfiguration
    
    系統將傳回類似以下的資訊：
    
        Identity               : Global
        EnableCDR              : True
        EnablePurging          : True
        KeepCallDetailForDays  : 90
        KeepErrorReportForDays : 60
        PurgeHourOfDay         : 2

如需詳細資訊，請參閱 [Get-CsCdrConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsCdrConfiguration) Cmdlet 的說明主題。

