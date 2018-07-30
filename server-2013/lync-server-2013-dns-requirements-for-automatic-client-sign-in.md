---
title: Lync Server 2013 中的自動用戶端登入的 DNS 需求
TOCTitle: Lync Server 2013 中的自動用戶端登入的 DNS 需求
ms:assetid: 3bcd4bb3-a022-4ffa-b005-1a95ad2b1796
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425884(v=OCS.15)
ms:contentKeyID: 49290651
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的自動用戶端登入的 DNS 需求

 

_**上次修改主題的時間：** 2015-03-09_

本主題將說明自動用戶端登入所需的網域名稱系統 (DNS) 記錄。當您部署自己的 Standard Edition Server 或前端集區時，可以設定用戶端使用自動探索功能來登入適當的 Standard Edition Server 或前端集區。如果您打算要求用戶端手動連線到 Lync Server 2013，則可以略過本主題。

若要支援用戶端自動登入，您必須：

  - 指定單一伺服器或集區，以分送和驗證用戶端登入要求。這可以是您組織中裝載使用者的現有伺服器或集區，或者，您也可以指定不裝載任何使用者的專用伺服器或集區做為此用途。若要達到高可用性，建議您指定前端集區來執行此功能。

  - 建立內部 DNS SRV 記錄，以支援此伺服器或集區的自動用戶端登入。
    
    > [!NOTE]  
    > 下列記錄需求中，SIP 網域是指已指派給使用者的 SIP URI 的主機部分。例如，如果 SIP URI 的格式為 *@contoso.com，則 contoso.com 為 SIP 網域。SIP 網域通常與內部 Active Directory 網域不同。組織也可以支援多個 SIP 網域。
    


若要啟用用戶端的自動設定，您必須建立內部 DNS SRV 記錄，將下列其中一個記錄對應到前端集區或 Standard Edition Server 的完整網域名稱 (FQDN)，來分送 Lync 用戶端的登入要求：

  - \_sipinternaltls.\_tcp.*\<網域\>*：用於內部 TLS 連線

您只需要為會分散登入要求的前端集區或 Standard Edition Server 建立單一 SRV 記錄。

下表顯示一些虛構公司 Contoso 所需的範例記錄，該公司支援 contoso.com 和 retail.contoso.com 這兩個 SIP 網域。

### 針對多個 SIP 網域進行自動用戶端登入所需之 DNS 記錄的範例

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>用來分送登入要求之前端集區的 FQDN</th>
<th>SIP 網域</th>
<th>DNS SRV 記錄</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>pool01.contoso.com</p></td>
<td><p>contoso.com</p></td>
<td><p>_sipinternaltls._tcp.contoso.com 網域 (透過連接埠 5061) 的 SRV 記錄，對應到 pool01.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>pool01.contoso.com</p></td>
<td><p>retail.contoso.com</p></td>
<td><p>_sipinternaltls._tcp.retail.contoso.com 網域 (透過連接埠 5061) 的 SRV 記錄，對應到 pool01.contoso.com</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 根據預設，DNS 記錄的查詢符合使用者名稱中的網域與 SRV 記錄之間的嚴格網域名稱比對。如果您想要讓用戶端 DNS 查詢改用尾碼比對，可以設定 DisableStrictDNSNaming 群組原則。如需詳細資訊，請參閱規劃文件中的＜<a href="lync-server-2013-planning-for-clients-and-devices.md">規劃 Lync Server 2013 中的用戶端和裝置</a>＞。



## 用戶端自動登入所需之憑證和 DNS 記錄的範例

此範例使用前面表格中的相同範例名稱。Contoso 組織支援 contoso.com 以及 retail.contoso.com 這兩個 SIP 網域，而且其所有的使用者都具有下列其中一種格式的 SIP URI：

  - *\<使用者\>*@retail.contoso.com

  - *\<使用者\>*@contoso.com

