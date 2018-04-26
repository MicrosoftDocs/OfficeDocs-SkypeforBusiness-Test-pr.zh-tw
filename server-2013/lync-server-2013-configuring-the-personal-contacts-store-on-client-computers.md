---
title: 在用戶端電腦上設定個人連絡人存放區
TOCTitle: 在用戶端電腦上設定個人連絡人存放區
ms:assetid: ec69a6cb-07f2-4057-9544-55035f83eeae
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721922(v=OCS.15)
ms:contentKeyID: 49890374
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在用戶端電腦上設定個人連絡人存放區

 

_**上次修改主題的時間：** 2014-02-05_

若您正在整合 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013，建議您在執行 Microsoft Lync 2010 的任何用戶端電腦上設定個人連絡人儲存區。明確地說，您應設定 Lync，將 Exchange 當作個人連絡人儲存區，同時確保使用者無法覆寫該決策。做法是在各用戶端電腦建立與設定 Registry 值。

請注意，不需要在執行 Lync 2013 的電腦上設定。

要在單一電腦上設定此值，請完成下列程序：

1.  在用戶端電腦上，依序按一下 \[開始\] 與 \[執行\]。

2.  在 \[執行\] 對話方塊中，輸入 regedit，然後按下 ENTER。

3.  在登錄編輯程式中，依序展開 **\[HKEY\_LOCAL\_MACHINE\]**、**\[Software\]**、**\[Policies\]**、**\[Microsoft\]** 以及 **\[Communicator\]**。

4.  以滑鼠右鍵按一下 **\[Communicator\]**，指向 **\[新增\]**，然後按一下 **\[DWORD (32-位元) 值\]**。

5.  建立新數值後，輸入 **PersonalContactStoreOverride**，然後按下 ENTER，為數值重新命名。

6.  確認 that the value of PersonalContactStoreOverride 值已設為 0，然後關閉登錄編輯程式。

若必須在多台電腦上進行相同變更，您可以建立自訂「群組原則」物件。如需詳細資訊，請參閱「群組原則」文件 (英文)，網址是：[http://go.microsoft.com/fwlink/?linkid=268543\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268543%26clcid=0x404)。

