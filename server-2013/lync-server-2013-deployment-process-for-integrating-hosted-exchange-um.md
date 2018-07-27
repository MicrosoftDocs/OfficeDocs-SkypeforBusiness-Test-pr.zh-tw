---
title: Lync Server 2013：整合主控 Exchange UM 的部署程序
TOCTitle: 整合主控 Exchange UM 和 Lync Server 的部署程序
ms:assetid: dbec9c38-7f66-419d-b8c3-c61380052cac
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398968(v=OCS.15)
ms:contentKeyID: 49292525
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 整合主控 Exchange UM 和 Lync Server 2013 的部署程序

 

_**上次修改主題的時間：** 2015-03-09_

有效規劃 Lync Server 2013 與裝載 Exchange 整合通訊 (UM) 的整合，需要考慮下列事項：

  - 將 Lync Server 2013 與裝載 Exchange UM 整合的先決條件

  - 整合過程中所需的步驟

## 與裝載 Exchange UM 整合的部署先決條件

在您開始進行整合程序之前，必須先部署 Lync Server 2013 (至少有一個前端集區和一部 Standard Edition Server)、Edge Server 及 Lync 2013 或 Lync 2010 用戶端。

## 整合程序

下表提供裝載 Exchange UM 整合程序的概觀。如需部署步驟的詳細資訊，請參閱部署文件中的 [在主控 Exchange UM 上提供 Lync Server 2013 使用者語音信箱](lync-server-2013-providing-lync-server-users-voice-mail-on-hosted-exchange-um.md)。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>階段</th>
<th>步驟</th>
<th>權限</th>
<th>部署文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>設定 Edge Server。</p></td>
<td><ol>
<li><p>設定同盟的 Edge Server。</p></li>
<li><p>手動將資料複寫至 Edge Server。</p></li>
<li><p>在 Edge Server 上設定裝載提供者。</p></li>
</ol></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-configure-the-edge-server-for-integration-with-hosted-exchange-um.md">將 Edge Server 設定為與主控 Exchange UM 整合</a></p></td>
</tr>
<tr class="even">
<td><p>設定裝載語音信箱原則。</p></td>
<td><ol>
<li><p>修改全域裝載語音信箱原則，或建立網站或個別使用者範圍的新託管語音信箱原則。</p></li>
<li><p>針對個別使用者範圍的原則，將原則指派給使用者或群組。</p></li>
</ol></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-manage-hosted-voice-mail-policies.md">在 Lync Server 2013 中管理裝載語音信箱原則</a></p></td>
</tr>
<tr class="odd">
<td><p>啟用使用者的裝載語音信箱。</p></td>
<td><ul>
<li><p>為信箱位於裝載 Exchange 服務上的使用者設定使用者帳戶。</p></li>
</ul></td>
<td><p>RTCUniversalUserAdmins</p></td>
<td><p><a href="lync-server-2013-enable-users-for-hosted-voice-mail.md">在 Lync Server 2013 中為使用者啟用主控語音信箱</a></p></td>
</tr>
<tr class="even">
<td><p>設定裝載連絡人物件。</p></td>
<td><ol>
<li><p>為裝載的 Exchange UM 建立自動語音應答連絡人物件。</p></li>
<li><p>為裝載的 Exchange UM 建立訂戶存取連絡人物件。</p></li>
</ol></td>
<td><p>RTCUniversalUserAdmins</p>
<div class="alert">
> [!NOTE]  
> 若要建立、修改或移除連絡人物件，執行 New-CsExUmContact、Set-CsExUmContact 或 Remove-CsExUmContact Cmdlet 的使用者必須具備儲存新的連絡人物件所在 Active Directory 組織單位的正確權限。執行 Grant-CsOUPermission Cmdlet，即可授與此權限。如需詳細資訊，請參閱 Lync Server 管理命令介面文件。


</div></td>
<td><p><a href="lync-server-2013-create-contact-objects-for-hosted-exchange-um.md">在 Lync Server 2013 中建立主控 Exchange UM 的聯絡人物件</a></p></td>
</tr>
</tbody>
</table>

