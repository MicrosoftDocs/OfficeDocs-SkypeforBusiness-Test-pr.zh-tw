---
title: Lync Server 2013：主控 Exchange UM 路由
TOCTitle: 主控 Exchange UM 路由
ms:assetid: 6c90dc8b-6aef-4ce8-b483-37c7b5a553c2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398512(v=OCS.15)
ms:contentKeyID: 49291240
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的主控 Exchange UM 路由

 

_**上次修改主題的時間：** 2012-10-01_

Exchange UM Routing 應用程式是在 前端伺服器上執行以將通話路由傳送至內部部署 Microsoft Exchange Server 整合通訊 (UM) 部署或裝載的 Exchange UM 服務。

## ExUM Routing 應用程式

Lync Server 2013Exchange UM Routing 應用程式使用使用者帳戶設定及裝載的語音信箱原則參數中的資訊，決定如何路由傳送裝載語音訊息的通話 (如下圖所示)。

**混合部署 Exchange UM 路由範例**

![內部部署 Lync Server Exchange UM 部署](images/Gg398512.75258286-1f23-487b-bf46-d8538e7d540e(OCS.15).jpg "內部部署 Lync Server Exchange UM 部署")

Exchange UM 路由可以設定成將通話路由傳送給啟用內部部署 Exchange UM 的使用者、啟用裝載 Exchange UM 的使用者，或上述兩者的組合。

例如，假設 Roy 的信箱及 Exchange UM 服務位於內部部署 Exchange 部署中。

  - Roy 使用者帳戶的 Proxy 位址資訊提供 ExUM Routing 應用程式用來將通話路由傳送至內部部署 Exchange UM 伺服器的資訊。

Alice 的信箱及 Exchange UM 服務位在裝載的 Exchange 服務提供者的資料中心上。其 Exchange UM 通話之路由的設定如下：

  - Alice 使用者帳戶之 msExchUCVoiceMailSettings 屬性中所設定的值，會告知 ExUM Routing 應用程式檢查裝載語音信箱原則中的路由詳細資料。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Exchange 服務提供者或 Lync Server 2013 系統管理員可以設定 msExchUCVoiceMailSettings 屬性的值。在上圖所顯示的範例中， Lync Server 2013 系統管理員已設定值 (CsHostedVoiceMail=1) 來啟用 Alice 的裝載語音信箱。如需此屬性的詳細資訊，請參閱＜ <a href="lync-server-2013-hosted-exchange-user-management.md">Lync Server 2013 中的主控 Exchange 使用者管理</a>＞。</td>
    </tr>
    </tbody>
    </table>


  - 指派給 Alice 使用者帳戶的裝載語音信箱原則提供路由詳細資料：
    
      - 目的地是裝載的 Exchange UM 服務提供者 (在此範例中是 ls.ExUm.*\<hostedExchangeServer\>*.com)。
    
      - 組織是透過租用戶 ID 所識別，而租用戶 ID 是路由 FQDN，適用於位在 ls.ExUm.*\<hostedExchangeServer\>*.com 之 Exchange Server 租用戶的 SIP 訊息 (在此範例中是 corp.contoso.com 及 corp.litwareinc.com)。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Exchange Online 的 FQDN 為 exap.um.outlook.com。</td>
        </tr>
        </tbody>
        </table>
        
        如需詳細資訊，請參閱＜[Lync Server 2013 中的主控語音信箱原則](lync-server-2013-hosted-voice-mail-policies.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果使用者帳戶中同時存在 msExchUCVoiceMailSettings 屬性及 UM Proxy 位址設定，則會優先採用 msExchUCVoiceMailSettings 屬性。</td>
</tr>
</tbody>
</table>

