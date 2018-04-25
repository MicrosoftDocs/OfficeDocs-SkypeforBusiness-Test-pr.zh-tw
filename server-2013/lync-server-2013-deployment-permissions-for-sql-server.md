---
title: Lync Server 2013：SQL Server 的部署權限
TOCTitle: SQL Server 的部署權限
ms:assetid: 56ea0c02-bcf5-4d45-aa13-570531c29074
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398375(v=OCS.15)
ms:contentKeyID: 49290972
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 SQL Server 的部署權限

 

_**上次修改主題的時間：** 2015-03-09_

Microsoft SQL Server 2012 在安裝與部署 Lync Server 2013 時，必須滿足特定的需求。由於 Windows 與 SQL Server 會以不同的方式定義安全性，以 Active Directory 網域的系統管理員身分登入並不表示自動授與 SQL Server 相關權限。您同時必須是所要設定之 SQL Server 伺服器上的 sysadmin 實體成員。

## 資料庫與 Lync Server 安裝所需的權限

下列選項詳述安裝 Lync Server 2013 檔案與 SQL Server 資料庫時相關的三種權限與群組成員資格。請針對組織需求選擇最適合的案例。

### 權限與群組成員資格關聯

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>SQL Server 或 Lync Server 2013 角色</th>
<th>角色典型的 SQL Server 權限與群組成員資格</th>
<th>角色典型的 Lync Server 2013 權限與群組成員資格</th>
<th>權限結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync Server 2013 系統管理員</p></td>
<td><p>必須賦予 sysadmins SQL Server 安全性群組與 SQL Server 本機 Administrators 群組成員資格</p></td>
<td><p>必須是 RTCUniversalServerAdmins 群組成員</p></td>
<td><p>Lync Server 2013 系統管理員具有同時安裝 Lync Server 2013 及 SQL Server 資料庫的適當權限。</p></td>
</tr>
<tr class="even">
<td><p>SQL Server 系統管理員</p></td>
<td><p>SQL Server sysadmin 群組成員 (或相等地位的成員) 及 SQL Server 本機 Administrators 群組成員</p></td>
<td><p>必須是 RTCUniversalServerReadOnly 群組成員</p></td>
<td><p>SQL Server 系統管理員具有同時安裝 Lync Server 2013 與 SQL Server 資料庫的適當權限。</p></td>
</tr>
<tr class="odd">
<td><p>這兩位系統管理員共同分攤安裝責任</p></td>
<td><p>SQL Server 系統管理員是 sysadmins 群組成員 (或相等地位的成員) 及 SQL Server 本機 Administrators 群組的成員</p></td>
<td><p>Lync Server 2013 系統管理員是 RTCUniversalServerAdmins 成員</p></td>
<td><p>Lync Server 2013 系統管理員可以安裝 Lync Server 2013，但不能安裝資料庫。SQL Server 系統管理員使用 Lync Server 2013 系統管理員所提供的 Lync Server 管理命令介面與 Windows PowerShell Cmdlet 來安裝資料庫。SQL Server 系統管理員所使用的 Lync Server 2013 管理命令介面會安裝在 前端伺服器 上，這樣一來，您就不用在 SQL Server 伺服器上安裝 Lync Server 2013 系統管理工具。</p></td>
</tr>
</tbody>
</table>

