---
title: Lync Server 2013：為 Lync Room System Administrative Web Portal 設定您的環境
TOCTitle: 為 Lync Room System Administrative Web Portal 設定您的環境
ms:assetid: 1bf3cc55-cfa8-46ee-a8bc-6dab3bff76b2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn436325(v=OCS.15)
ms:contentKeyID: 59602852
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 為 Lync Room System Administrative Web Portal 設定您的 Lync Server 2013 環境

 

_**上次修改主題的時間：** 2014-05-22_

若要使用 Lync Room System (LRS) Administrative Web Portal，您將需要安裝和設定下列先決條件。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若是使用 Kerberos 和 NTLM 驗證設定伺服器，並在未加入網域的電腦上執行 LRS，Kerberos 驗證將失敗，且使用者將無法在系統管理入口網站中看到 LRS 的狀態。若要解決此問題，請使用 NTLM 驗證，或同時使用 NTLM 和 TLS-DSK 驗證 (不含 Kerberos) 來設定伺服器，或在網域中加入 LRS 電腦。</td>
</tr>
</tbody>
</table>


1.  安裝 Lync Server 2013 累計更新：Lync Server 拓撲，2013 年 7 月。
    
    若要取得更新或查看其隨附的內容，請參閱 [Lync 伺服器 2013年的更新](http://go.microsoft.com/fwlink/p/?linkid=323959)。

2.  建立啟用 SIP 的 Active Directory 使用者。
    
    LRS Administrative Web Portal 使用這些認證從 Lync Server 查詢資訊。建議的使用者名稱為 LRSApp。

3.  使用名稱 LRSSupportAdminGroup 建立 Active Directory 安全性群組。
    
    將 \[群組範圍\] 設為 \[全域\]，並將 \[群組類型\] 設為 \[安全性\] 來建立群組。新增至此群組並啟用 SIP 的使用者，將有權查看聊天室清單及執行某些命令，例如收集記錄。

4.  使用名稱 LRSFullAccessAdminGroup 建立 Active Directory 安全性群組。
    
    將 \[群組範圍\] 設為 \[全域\]，並將 \[群組類型\] 設為 \[安全性\] 來建立群組。新增至此群組並啟用 SIP 的使用者，將有權使用所有管理入口網站功能。
    
     
    
    ![具有安全性群組角色之管理員群組的清單](images/Dn436325.5d432819-a2e2-452c-bc2a-5d4ee79d8c33(OCS.15).png "具有安全性群組角色之管理員群組的清單")  
    
     

5.  將 LRSFullAccessAdminGroup 新增為 LRSSupportAdminGroup 的成員。
    
    ![\[LRSSupportAdminGroup 內容成員\] 頁面](images/Dn436325.91a4a28a-cacf-4ef6-aac1-915ec41c9648(OCS.15).png "[LRSSupportAdminGroup 內容成員] 頁面")  
    
     

6.  使用名稱 LRSSupport 建立啟用 SIP 的 Active Directory 使用者。將此使用者新增至 LRSSupportAdminGroup。
    
    ![\[LRSSupportAdminGroup 內容成員\] 頁面](images/Dn436325.7638055d-22ac-4909-914d-1966f5623909(OCS.15).png "[LRSSupportAdminGroup 內容成員] 頁面")  
    
     

7.  為 Visual Studio 2010 SP1 和 Visual Web Developer 2010 SP1 安裝 ASP.NET MVC 4，可從 Microsoft 下載中心取得，網址為 [http://go.microsoft.com/fwlink/p/?LinkId=323967](http://go.microsoft.com/fwlink/p/?linkid=323967)。

