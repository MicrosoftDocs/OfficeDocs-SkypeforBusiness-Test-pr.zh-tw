---
title: Lync Server 2013：設定檔案儲存
TOCTitle: 設定檔案儲存
ms:assetid: a985be20-5a00-4f38-b45b-83dc82de3827
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205150(v=OCS.15)
ms:contentKeyID: 49291943
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 設定檔案儲存

 

_**上次修改主題的時間：** 2012-09-13_

Lync Server 2013 支援在分散式檔案系統 (DFS) 上使用檔案共用。如需關於 Windows Server 2008 之 DFS 的詳細資訊，請參閱《Windows Server 2008 的 DFS 逐步指南》，網址為： [http://go.microsoft.com/fwlink/?linkid=202835\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=202835%26clcid=0x404)。若要使用 DFS， Lync Server 2013 要求下列各項：

  - 命名空間是以網域為基礎

  - 所有命名空間伺服器都是執行最基本的 Windows 2008

Lync Server 2013 安裝程式需要共用資料夾的權限，才能讓系統管理員擁有完整存取權。 Lync Server 2013 將使用 NTFS 檔案權限來設定資料夾的 ACL。繼承的 DFS 共用權限不會用於限制存取權。

如需關於檔案共用需求的詳細資訊，請參閱支援文件中的＜ [Lync Server 2013 中的檔案儲存支援](lync-server-2013-file-storage-support.md)＞。

下列程序說明如何使用 \[DFS 命名空間精靈\] 正確設定共用資料夾權限 (如 DFS 安裝指南所述)。

## 設定共用資料夾權限

1.  按一下 \[開始\] ，依序指向 \[所有程式\] 和 \[系統管理工具\] ，然後按一下 \[DFS 管理\] 。

2.  在 \[DFS 管理\] 嵌入式管理單元中，用滑鼠右鍵按一下命名空間伺服器 (例如 filesrv1.contoso.com)，然後按一下 \[編輯設定\] 。

3.  選取 \[共用資料夾權限\] 。

4.  選取 \[使用自訂權限\] 。

5.  針對系統管理員群組，選取 \[允許\] 下的下列項目：
    
      - \[完全控制\]
    
      - \[變更\]
    
      - \[讀取\]

6.  按一下 \[套用\] ，然後按一下 \[確定\] 。

