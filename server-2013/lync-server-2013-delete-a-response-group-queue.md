---
title: 刪除回應群組佇列
TOCTitle: 刪除回應群組佇列
ms:assetid: 67c7a489-8c5f-4c6b-9387-9d4c11d43695
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg521008(v=OCS.15)
ms:contentKeyID: 49291173
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除回應群組佇列

 

_**上次修改主題的時間：** 2012-11-01_

使用下列其中一個程序刪除佇列。

## 若要使用 Lync Server 控制台刪除佇列

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[回應群組\]**，然後按一下 **\[佇列\]**。

4.  在 \[搜尋\] 欄位中，輸入想要刪除之佇列的部分或全部名稱。

5.  在佇列清單中，按一下想要的佇列，並按一下 **\[編輯\]**，然後按一下 **\[刪除\]**。

6.  按一下 **\[確定\]**。

## 使用 Cmdlet 刪除佇列

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令列上執行：
    
        Get-CsRgsQueue -Identity <Application Server service> -Name "<name of queue>" | Remove-CsRgsQueue
    
    例如：
    
        Get-CsRgsQueue -Identity service:ApplicationServer:redmond.contoso.com -Name "Help Desk" | Remove-CsRgsQueue

