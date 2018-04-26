---
title: 安裝 Operation Manager 代理程式檔案
TOCTitle: 安裝 Operation Manager 代理程式檔案
ms:assetid: e2246c44-0c75-43fc-8b04-26e53c5dd572
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205345(v=OCS.15)
ms:contentKeyID: 49292584
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝 Operation Manager 代理程式檔案

 

_**上次修改主題的時間：** 2012-10-20_

要在電腦上安裝 Operations Manager 代理程式檔案，請完成下列步驟。

1.  在 System Center 安裝媒體上按兩下 \[SetupOM.exe\] 。

2.  在 System Center Operation Manager 安裝程式，按一下 \[安裝 Operations Manager 代理程式\]。

3.  在 System Center 安裝精靈的 \[歡迎使用 System Center Operations Manager 安裝程式\] 精靈頁面上按 \[下一步\]。

4.  在 \[目的資料夾\] 頁面上，選擇要安裝 Operations Manager 代理程式檔案的資料夾，然後按 \[下一步\]。

5.  在 \[管理群組設定\] 頁面中，選擇 \[指定管理群組資訊\]，然後按 \[下一步\]。

6.  在 \[管理群組設定\] 頁面的 \[管理群組名稱\] 方塊中，輸入 Operations Manager 管理群組名稱的名稱，然後在 \[管理伺服器\] 方塊中輸入 Operations Manager 伺服器 (例如 atl-scom-001) 的主機名稱。若您變更了 Operations Manager 所使用的連接埠號碼，則請在「管理伺服器連接埠」方塊中輸入新連接埠號碼。否則，請保留連接埠預設值 5723，然後按 \[下一步\]。

7.  在 \[代理程式動作帳戶\] 頁面上，選取 \[本機系統\]，然後按 \[下一步\]。

8.  在 \[Microsoft Update\] 頁面上，選擇 \[我不要使用 Microsoft Update\]，然後按 \[下一步\]。

9.  在 \[準備安裝\] 頁面上，按一下 \[安裝\]。

10. 在 \[完成 System Center Operations Manager 安裝精靈\] 頁面上，按一下 \[完成\]。

11. 按一下 \[結束\]。

若您使用 System Center 2007 R2，要驗證代理程式是否已建立，可依序按一下 \[開始\]、\[所有程式\]、\[System Center Operations Manager 2007 R2\]，然後按一下 \[Operations Manager 殼層\] 。在 Operations Manager 殼層中，輸入下列 Windows PowerShell 命令，然後按下 ENTER：

    Get-Agent 

所有 Operations Manager 代理程式的清單會出現在螢幕上。

若使用 System Center 2012，請從 Operations 2012 Manager 殼層執行此命令：

    Get-SCOMAgent

