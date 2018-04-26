---
title: Lync Server 2013：啟用 Lync-Skype 連線功能
TOCTitle: 啟用 Lync-Skype 連線功能
ms:assetid: 34c4db3e-582f-41fb-85c4-3438ae02f09f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn440170(v=OCS.15)
ms:contentKeyID: 59602845
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中啟用 Lync-Skype 連線功能

 

_**上次修改主題的時間：** 2014-12-16_

提交佈建要求後，即可專心著眼於設定 Lync-Skype 連線所需的 Lync Server 環境與系統管理工作。本節假定 Lync Server 系統管理員已部署 Lync Server 並設定外部存取。如需為 Lync Server 設定外部存取的額外資訊，請參閱 [在 Lync Server 2013 中規劃外部使用者存取](lync-server-2013-planning-for-external-user-access.md)和 [在 Lync Server 2013 中部署外部使用者存取](lync-server-2013-deploying-external-user-access.md)。

為準備 Lync Server 環境以進行 Lync-Skype 連線，Lync Server 系統管理員必須完成下列三項工作：

## 1\. 設定同盟與 PIC

同盟是 Skype 使用者與組織中的 Lync 使用者進行通訊的必要途徑。公用立即訊息連線 (PIC) 則是一種同盟等級，必須加以設定以讓 Lync 使用者與 Skype 使用者進行通訊。同盟與 PIC 均是使用 Lync Server 控制台進行設定，如下所示。

![顯示 PIC](images/Dn440170.451b94e3-0b38-488c-835f-1f25690e8074(OCS.15).jpg "顯示 PIC")

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PIC 同盟不再受 Live Communication Server 2005 SP1 或 Office Communications Server 2007 支援。PIC 同盟的支援平台包括 Lync Server 2013、Lync Server 2010 以及 Office Communications Server 2007 R2。</td>
</tr>
</tbody>
</table>


## 2\. 設定至少一項原則以支援同盟使用者存取

系統管理員必須使用 Lync Server 控制台設定一或多項外部使用者存取原則以控制 Skype 使用者是否能與內部 Lync Server 使用者共同作業。

![原則](images/Dn440170.8fd46ad1-9749-422c-8c47-c16ac9032cdb(OCS.15).jpg "原則")

## 3\. 針對 Lync 設定 Skype PIC 提供者設定

系統管理員必須使用 Lync Server 管理命令介面設定 Lync 用戶端原則以將 Skype 顯示為額外 PIC 提供者。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>除非您亦有設定至少一項原則 (此程序先前的步驟 2) 以支援公用 IM 連線，否則公用立即訊息連線 (PIC) 服務提供者的使用者將無法參與貴組織中的 IM 或音訊或視訊會議。</td>
</tr>
</tbody>
</table>


1.  若要設定同盟與 PIC，請參閱＜啟用或停用同盟及公用 IM 連線＞： [http://go.microsoft.com/fwlink/p/?LinkId=306063](http://go.microsoft.com/fwlink/p/?linkid=306063)。

2.  若要設定至少一項原則以支援同盟使用者存取，請參閱＜設定原則以控制公用使用者存取＞： [http://go.microsoft.com/fwlink/p/?LinkId=306064](http://go.microsoft.com/fwlink/p/?linkid=306064)。

**若要編輯 Messenger PIC 提供者並針對 Skype 設定**

1.  從 Lync Server 前端伺服器中，開啟 Lync Server 管理命令介面。

2.  執行下列兩項命令：
    
    `Remove-CsPublicProvider -Identity Messenger`
    
    `New-CsPublicProvider -Identity Skype -ProxyFqdn federation.messenger.msn.com -IconUrl "https://images.edge.messenger.live.com/Messenger_16x16.png" -VerificationLevel 2 -Enabled 1`

3.  您現在可從 Lync 用戶端中選取 Skype 作為 PIC 提供者，並且透過指定相關 Microsoft 帳戶的方式來新增 Skype 用戶端。此外，已合併並透過其 Microsoft 帳戶登入的 Skype 使用者可以傳送聯絡人授權請求給 Lync 使用者。如需 Microsoft 帳戶的詳細資訊，請參閱[什麼是 Microsoft 帳戶？](https://support.skype.com/en/faq/fa12059/what-is-a-microsoft-account) (英文)。如需將用戶端新增至 Lync 的額外資訊，請參閱[在 Lync Server 2013 中以使用者身分使用 Lync-Skype 連線](lync-server-2013-using-lync-skype-connectivity-as-an-end-user.md)。
    
    ![新增 Skype 連絡人](images/Dn440170.df0e6ed9-2374-4dfa-a815-87281989487c(OCS.15).jpg "新增 Skype 連絡人")

4.  如需修改裝載提供者的詳細資訊，請參閱＜建立或編輯主控的 SIP 同盟提供者＞： [http://go.microsoft.com/fwlink/p/?LinkId=306065](http://go.microsoft.com/fwlink/p/?linkid=306065)。

如此即完成伺服器上所需執行的系統管理工作。您現在已可進行 Lync-Skype 連線。

