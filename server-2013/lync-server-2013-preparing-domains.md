---
title: Lync Server 2013：準備網域
TOCTitle: 準備網域
ms:assetid: 8eea541c-5f9d-4afc-92a8-a31d6f742544
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398721(v=OCS.15)
ms:contentKeyID: 49291636
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 準備網域

 

_**上次修改主題的時間：** 2012-10-29_

網域準備是為 Lync Server 2013 準備 Active Directory 網域服務 的最後一個步驟。網域準備步驟會將必要的存取控制項目 (ACE) 新增至萬用群組，而這些群組會授與權限來裝載和管理網域內的使用者。網域準備作業會在網域根目錄和三個內建容器上建立 ACE：使用者、電腦和網域控制站。

您可以在計劃部署 Lync Server 之網域中的任何電腦上，執行網域準備作業。對於將裝載 Lync Server 或使用者的每個網域，都必須進行網域的準備工作。

如果已停用權限繼承，或您的組織停用已驗證的使用者權限，則在進行網域準備時必須執行額外的步驟。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中準備鎖定的 Active Directory 網域服務](lync-server-2013-preparing-a-locked-down-active-directory-domain-services.md)＞。

如果您的組織使用組織單位 (OU) 而非三個內建的容器 (也就是使用者、電腦和網域控制站)，您必須將讀取權限授與 Authenticated Users 群組。執行網域準備工作時，必須要有容器的讀取存取權。如果 Authenticated Users 群組不具有 OU 的讀取存取權，請依照以下程式碼範例的說明執行 **Grant-CsOuPermission** Cmdlet，以便授與每個 OU 的讀取權限。

  ```
  Grant-CsOuPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <DN of the OU > 
  ```
  ```
  Grant-CsOuPermission -ObjectType "user","contact",inetOrgPerson" -OU "ou=Redmond,dc=contoso,dc=net"
  ```

如需 **Grant-CsOuPermission** Cmdlet 的詳細資訊，請參閱 Lync Server 管理命令介面文件。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需在網域根目錄以及在使用者、電腦和網域控制站容器中建立之 ACE 的詳細資訊，請參閱＜ <a href="lync-server-2013-changes-made-by-domain-preparation.md">Lync Server 2013 中的網域準備所進行的變更</a>＞。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [為 Lync Server 2013 執行網域準備](lync-server-2013-running-domain-preparation.md)

  - [將 Cmdlet 用於 Lync Server 2013 的反向網域準備](lync-server-2013-using-cmdlets-to-reverse-domain-preparation.md)

