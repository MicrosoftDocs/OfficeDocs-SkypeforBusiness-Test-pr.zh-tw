---
title: 移除封存伺服器的 SQL Server 資料庫
TOCTitle: 移除封存伺服器的 SQL Server 資料庫
ms:assetid: 6e8a1fcd-ed09-43b0-82c9-60e7ce116a01
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688087(v=OCS.15)
ms:contentKeyID: 49890109
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除封存伺服器的 SQL Server 資料庫

 

_**上次修改主題的時間：** 2012-10-04_

在移除 Microsoft Lync Server 2010  封存伺服器後，便可移除裝載集區資料的 SQL Server 資料庫。請使用下列程序從 拓撲產生器移除定義，然後從資料庫伺服器移除資料庫及記錄檔。

## 使用 拓撲產生器移除 SQL Server 資料庫

1.  在 Lync Server 2013 前端伺服器上，開啟 拓撲產生器。

2.  在拓撲產生器中，依序導覽至 **\[共用元件\]** 和 \[SQL Server 存放區\]，對於所要移除或重設之封存伺服器相關聯的 SQL Server 執行個體按一下滑鼠右鍵，然後按一下 \[刪除\]。

3.  發行拓撲，然後檢查複寫狀態。

## 移除 SQL Server 上的資料庫檔案

1.  若要移除 SQL Server 上的資料庫，您必須是所要移除資料庫檔案之 SQL Server 的 SQL Server sysadmins 群組成員。

2.  開啟 Lync Server 管理命令介面。

3.  在命令列輸入下列命令：
    
        Uninstall-CsDataBase -DatabaseType Archiving -SqlServerFqdn <FQDN> [-SqlInstanceName <instance>]
    
    其中 *\<FQDN\>* 是資料庫伺服器的完整網域名稱 (FQDN)，而 *\<instance\>* 是具名的資料庫執行個體 (若有定義的話)。

4.  當 **Uninstall-CsDataBase** Cmdlet 提示您確認動作時，請閱讀資訊，然後按 **Y** (或按 Enter) 繼續作業，或是依序按 **N** 及 Enter 停止 Cmdlet (例如發生錯誤時)。

