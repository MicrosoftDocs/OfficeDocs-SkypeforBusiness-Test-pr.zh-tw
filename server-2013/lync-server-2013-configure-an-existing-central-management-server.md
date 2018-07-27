---
title: Lync Server 2013：設定現有的中央管理伺服器
TOCTitle: 設定現有的中央管理伺服器
ms:assetid: d715b24a-1256-4a7c-a5ef-1cee41d6b733
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205315(v=OCS.15)
ms:contentKeyID: 49292444
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定現有的中央管理伺服器

 

_**上次修改主題的時間：** 2013-02-21_

如果您重複使用現有 Lync Server 2013 部署的中央管理伺服器，您必須執行以下所述的程序，確保 Lync Server 控制台與 Windows PowerShell 可正確運作。

## 設定現有 中央管理伺服器

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  使用 **Update-CsAdminRole** Cmdlet 以更新 中央管理伺服器中儲存的角色型存取控制 (RBAC) 角色。
    
    > [!NOTE]  
    > 除非發生錯誤，否則不會有任何輸出。
    

