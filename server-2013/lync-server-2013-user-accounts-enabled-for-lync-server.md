---
title: 針對 Lync Server 2013 啟用的使用者帳戶
TOCTitle: 針對 Lync Server 2013 啟用的使用者帳戶
ms:assetid: 8021087e-5084-4a39-9fef-ab9376c6d371
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182543(v=OCS.15)
ms:contentKeyID: 49291476
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 啟用的使用者帳戶

 

_**上次修改主題的時間：** 2015-03-09_

本節中的主題將針對使用 Lync Server 2013 控制台 中的 \[使用者\] 頁面所能執行的工作，提供逐步程序。

> [!IMPORTANT]  
> 您無法以 Lync Server 控制台 管理身為 Active Directory Domain Admins 群組成員的使用者。對於 Domain Admins 使用者，您僅能使用 Lync Server 控制台 執行唯讀搜尋作業。若要對 Domain Admins 使用者執行寫入作業 (例如對 Lync Server 控制台 啟用或停用、變更集區或原則指派、電話語音設定、SIP 位址)，您必須以 Domain Admins 使用者的身分登入，並使用 Windows PowerShell Cmdlet。如需使用 Windows PowerShell Cmdlet 來管理使用者的詳細資訊，請參閱 <a href="lync-server-2013-lync-server-management-shell.md">Lync Server 管理命令介面</a>。



當您進行任何需要搜尋某位使用者或篩選使用者搜尋結果的 Lync Server 2013 管理工作時，某些使用者屬性 (properties) 會以屬性 (attributes) 的型態存在於 Active Directory 網域服務 中，但它們在部署 Microsoft Exchange Server 之前並不會複製到通用類別目錄。 Microsoft Exchange (而非 Lync Server)，會標記出下列屬性，以待安裝後複製到通用類別目錄：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>使用者資訊</th>
<th>地址和電話</th>
<th>所屬機構</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>簡稱</p></td>
<td><p>街道地址</p>
<p>國家/地區</p>
<p>呼叫器</p>
<p>傳真</p>
<p>Mobile</p></td>
<td><p>標題</p>
<p>公司</p>
<p>Department</p>
<p>辦公室</p></td>
</tr>
</tbody>
</table>


## 本章節內容

  - [檢視針對 Lync Server 2013 啟用之使用者帳戶的相關資訊](lync-server-2013-viewing-information-about-user-accounts-enabled-for-lync-server.md)

  - [啟用和停用 Lync Server 2013 使用者](lync-server-2013-enabling-and-disabling-users-for-lync-server.md)

  - [管理使用者的 Enterprise Voice](lync-server-2013-managing-enterprise-voice-for-users.md)

  - [修改使用者帳戶屬性](lync-server-2013-modifying-user-account-properties.md)

  - [在 Lync Server 2013 中管理外部使用存取原則](lync-server-2013-manage-external-access-policy-for-your-organization.md)

  - [指派每位使用者的原則](lync-server-2013-assigning-per-user-policies.md)

## 請參閱

#### 概念

[使用者管理 Cmdlet](lync-server-2013-user-management-cmdlets.md)  

#### 其他資源

[在 Lync Server 2013 中管理使用者](lync-server-2013-managing-users-in-lync-server.md)

