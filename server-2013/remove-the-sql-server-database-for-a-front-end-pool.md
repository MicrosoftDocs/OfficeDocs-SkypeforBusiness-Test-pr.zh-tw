---
title: 移除前端集區的 SQL Server 資料庫
TOCTitle: 移除前端集區的 SQL Server 資料庫
ms:assetid: 6bb932df-3ed7-49b6-ae17-61e4c6a5fe82
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688084(v=OCS.15)
ms:contentKeyID: 49890105
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除前端集區的 SQL Server 資料庫

 

_**上次修改主題的時間：** 2012-10-04_

在您移除 Microsoft Lync Server 2010前端集區或重新設定集區以使用其他資料庫後，即可移除裝載過集區資料的 SQL Server 資料庫。使用下列程序將定義從 拓撲產生器移除，然後將資料庫和記錄檔從資料庫伺服器移除。

## 使用 拓撲產生器移除 SQL Server 資料庫

1.  在 Lync Server 2013 前端伺服器開啟 拓撲產生器並下載現有的拓撲。

2.  在 拓撲產生器 中，依序瀏覽至**共用元件** 和 \[SQL Server Stores\]，針對與您要移除或重新設定之 前端集區 相關聯的 SQL Server 執行個體，按一下滑鼠右鍵，然後按一下 \[刪除\]。

3.  發行拓撲，然後檢查複寫狀態。

## 從 SQL Server 移除使用者和應用程式資料庫

1.  若要移除 SQL Server 上的資料庫，您必須是所要移除資料庫檔案之 SQL Server 的 SQL Server sysadmins 群組成員。

2.  開啟 Lync Server 管理命令介面

3.  若要移除集區使用者存放區的資料庫，請鍵入：
    
        Uninstall-CsDataBase -DatabaseType User -SqlServerFqdn <FQDN> [-SqlInstanceName <instance>]
    
    其中 *\<FQDN\>* 是資料庫伺服器的完整網域名稱 (FQDN)，而 *\<instance\>* 是具名的資料庫執行個體 (若有定義的話)。

4.  若要移除集區應用程式存放區的資料庫，請鍵入：
    
        Uninstall-CsDataBase -DatabaseType Application -SqlServerFqdn <FQDN> [-SqlInstanceName <instance>]
    
    其中 *\<FQDN\>* 是資料庫伺服器的 FQDN，而 *\<instance\>* 則是具名資料庫執行個體 (即如果已定義)。

5.  當 **Uninstall-CsDataBase** Cmdlet 提示您確認動作時，請閱讀資訊，然後按 **Y** (或按 Enter) 繼續作業，或是依序按 **N** 及 Enter 停止 Cmdlet (例如發生錯誤時)。

