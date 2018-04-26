---
title: 移除監控伺服器的 SQL Server 資料庫
TOCTitle: 移除監控伺服器的 SQL Server 資料庫
ms:assetid: aed5e394-d63e-4ad4-af40-f12d3a044344
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721848(v=OCS.15)
ms:contentKeyID: 49890262
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除監控伺服器的 SQL Server 資料庫

 

_**上次修改主題的時間：** 2012-10-04_

在您移除 Microsoft Lync Server 2010  監控伺服器後，可以移除主控伺服器資料的 SQL Server 資料庫。請使用下列程序，從 拓撲產生器中移除定義，然後從資料庫伺服器移除資料庫和記錄檔。

## 使用 拓撲產生器移除 SQL Server 資料庫

1.  在 Lync Server 2013 前端伺服器上，開啟 拓撲產生器。

2.  在 拓撲產生器上，瀏覽至 \[共用元件\] 後再瀏覽至 \[SQL Server 存放區\] ，以滑鼠右鍵按一下與已移除或已重新配置的 監控伺服器關聯的 SQL Server 執行個體，然後按一下 \[刪除\] 。

3.  發行拓撲，然後檢查複寫狀態。

## 移除 SQL Server 上的資料庫檔案

1.  若要移除以 SQL Server 伺服器上的資料庫，必須具備要移除之資料庫檔案所屬 SQL Server 的 SQL Server sysadmins 群組成員資格。

2.  開啟 Lync Server 管理命令介面。

3.  在命令列輸入下列命令：
    
        Uninstall-CsDataBase -DatabaseType Monitoring -SqlServerFqdn <FQDN> [-SqlInstanceName <instance>]
    
    其中 *\<FQDN\>* 是資料庫伺服器的完整網域名稱 (FQDN)，而 *\<instance\>* 是具名的資料庫執行個體 (選用)。

4.  當 **Uninstall-CsDataBase** Cmdlet 提示您確認動作時，請閱讀資訊，然後按 **Y** (或按 Enter) 繼續作業，或是依序按 **N** 及 Enter 停止 Cmdlet (例如發生錯誤時)。

