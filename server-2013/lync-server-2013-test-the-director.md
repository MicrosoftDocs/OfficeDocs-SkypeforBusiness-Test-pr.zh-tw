---
title: Lync Server 2013：測試 Director
TOCTitle: 測試 Director
ms:assetid: 9627a7e2-28cc-429c-b79b-7c7a27573bb7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398767(v=OCS.15)
ms:contentKeyID: 49291746
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中測試 Director

 

_**上次修改主題的時間：** 2012-09-08_

到這個階段為止，您已經擁有已設定的 Director 或 Director 集區了，但網域名稱系統 (DNS) SRV 項目仍然指定用戶端使用集區或 Standard Edition Server 登入。在變更 DNS 記錄以使 Lync 2013 用戶端自動使用 Director 登入之前，請以手動方式將用戶端指向 Director 以資測試。

## 若要測試部署

1.  以隸屬於 **CSAdministrator** 群組的網域帳戶登入安裝 Lync Server 控制台的電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  按一下導覽窗格中的 **\[拓撲\]** ，在 **\[狀態\]** 欄中確認您的 Director 或 Director 集區有綠色的伺服器和箭頭 (即 ![帶有綠色箭頭的伺服器圖示](images/Gg398767.2263cdb7-7e60-457a-a528-a3a082bd051b(OCS.15).jpg "帶有綠色箭頭的伺服器圖示"))。

4.  連接兩部已安裝 Lync Server 2013 用戶端的用戶端電腦，再以其他啟用 Lync Server 2013 的使用者帳戶登入這兩部電腦。

5.  在其中一部電腦上按一下 **\[選項\]** 功能表並選取 **\[個人\]** 設定群組，再依序按一下 **\[進階\]** 和 **\[手動設定\]** ，接著將 **\[內部伺服器名稱或 IP 位址\]** 設定為新 Director 或 Director 集區的完整網域名稱 (FQDN)。

6.  登入這兩個用戶端，確認使用 Director 登入的用戶端能成功登入、能查看其他使用者的顯示狀態，以及能交換立即訊息。

