---
title: Lync Server 2013：測試 Standard Edition Server
TOCTitle: 測試 Standard Edition Server
ms:assetid: b6ef67bb-9665-43e4-b8b3-eac8898eebf6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412890(v=OCS.15)
ms:contentKeyID: 49292087
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中測試 Standard Edition Server

 

_**上次修改主題的時間：** 2012-10-01_

下列程序將說明如何測試 Standard Edition 伺服器的部署。

## 若要測試 Standard Edition Server 的部署

1.  使用 Active Directory 電腦和使用者將 Lync Server 2013 部署 (安裝 Lync Server 控制台的所在位置) 之系統管理員角色的 Active Directory 使用者物件新增至 \[CSAdministrator\] 群組。

2.  如果使用者物件目前為登入狀態，請先登出再登入，以登錄新的群組指派。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>使用者帳戶不可以是執行 Lync Server 2013 Standard Edition 之伺服器的本機系統管理員。如果您未將適當的使用者和群組加入至 CsAdministors 群組，則會在開啟 Lync Server 2013 控制台時收到錯誤，表示「未授權: 存取被拒，因為角色型存取控制 (RBAC) 授權失敗」。</td>
    </tr>
    </tbody>
    </table>


3.  使用系統管理帳戶登入安裝 Lync Server 控制台所在的電腦。

4.  啟動 Lync Server 控制台，然後在提示時提供認證。 Lync Server 2013 控制台會顯示部署資訊。

5.  在左導覽列中，按一下 \[拓撲\] ，然後確認服務狀態是帶有綠色箭頭的電腦圖示，而且每一個已部署且上線的 Lync Server 伺服器角色旁邊都有一個綠色核取記號。

6.  在左導覽列中，按一下 \[使用者\] ，然後為兩位使用者啟用 Lync Server 2013。

7.  將一個使用者登入已加入網域的電腦，並將另一個使用者登入網域中的其他電腦。

8.  在這兩部用戶端電腦上安裝 Lync Server 2013，然後確認兩位使用者都能夠登入 Lync Server 2013 並且傳送立即訊息給對方。

## 請參閱

#### 概念

[在 Lync Server 2013 中部署用戶端和裝置](lync-server-2013-deploying-clients-and-devices.md)

