---
title: Lync Server 2013：存取 Lync Server 公用 IM 連線佈建網站
TOCTitle: 存取 Lync Server 公用 IM 連線佈建網站
ms:assetid: 77a08234-6bcf-4f59-b43b-ee5fc1926585
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn440174(v=OCS.15)
ms:contentKeyID: 59602856
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 透過 Lync Server 2013 存取 Lync Server 公用 IM 連線佈建網站

 

_**上次修改主題的時間：** 2015-03-09_

相較先前的 PIC 佈建方法，Lync-Skype 連線的佈建程序有所變更。這項佈建程序最多需要三十天才可完成。建議在執行此文件的後續步驟前先開始這項程序。在您的帳戶的 Lync-Skype 佈建程序完成後，系統即會啟用該帳戶與合格使用者的公用 IM 連線功能。

### 若要佈建 Lync-Skype 連線，您需要下列資訊：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ol>
<li><p>Microsoft 合約編號</p></li>
<li><p>Access Edge Service 完整網域名稱 (FQDN)</p></li>
<li><p>工作階段初始通訊協定 (SIP) 網域</p></li>
<li><p>任何額外的 Access Edge Service FQDN</p></li>
<li><p>連絡人資訊</p></li>
</ol></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Microsoft 合約編號</p></li>
<li><p>Access Edge Service 完整網域名稱 (FQDN)</p></li>
<li><p>工作階段初始通訊協定 (SIP) 網域</p></li>
<li><p>任何額外的 Access Edge Service FQDN</p></li>
<li><p>連絡人資訊</p></li>
</ol></td>
</tr>
</tbody>
</table>


### 若要啟動 Lync-Skype 連線的佈建程序：

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ol>
<li><p>使用 Microsoft Windows Live ID 登入網站：<strong>https://pic.lync.com</strong>。</p></li>
<li><p>選取 Microsoft 授權合約類型。</p></li>
<li><p>選取核取方塊，確認您已閱讀並接受 Lync Server 的產品使用權。</p></li>
<li><p>在 [啟動佈建要求] 頁面中，按一下適當連結以啟動佈建要求：</p></li>
<li><p>在 [指定佈建資訊] 頁面中，輸入「Access Edge Service FQDN」，例如 <strong>accessedge.contoso.com</strong>。</p></li>
<li><p>輸入至少一個或多個 SIP 網域名稱，然後按一下 [新增]。</p>


> [!IMPORTANT]  
> 至少需要一部 Access Edge Server 與一個 SIP 網域，才能完成佈建程序。SIP 網域與 Access Edge Server 必須已啟用、正在運作，並可透過網路連線。


</div></li>
<li><p>在 [公用 IM 服務提供者] 清單中，選取 [Skype]，然後按一下 [下一步] 以新增連絡人資訊並提交佈建要求。</p></li>
</ol></td>
</tr>
<tr class="even">
<td><ol>
<li><p>使用 Microsoft Windows Live ID 登入網站：<strong>https://pic.lync.com</strong>。</p></li>
<li><p>選取 Microsoft 授權合約類型。</p></li>
<li><p>選取核取方塊，確認您已閱讀並接受 Lync Server 的產品使用權。</p></li>
<li><p>在 [啟動佈建要求] 頁面中，按一下適當連結以啟動佈建要求：</p></li>
<li><p>在 [指定佈建資訊] 頁面中，輸入「Access Edge Service FQDN」，例如 <strong>accessedge.contoso.com</strong>。</p></li>
<li><p>輸入至少一個或多個 SIP 網域名稱，然後按一下 [新增]。</p>
<div>

> [!IMPORTANT]  
> 至少需要一部 Access Edge Server 與一個 SIP 網域，才能完成佈建程序。SIP 網域與 Access Edge Server 必須已啟用、正在運作，並可透過網路連線。


</div></li>
<li><p>在 [公用 IM 服務提供者] 清單中，選取 [Skype]，然後按一下 [下一步] 以新增連絡人資訊並提交佈建要求。</p></li>
</ol></td>
</tr>
</tbody>
</table>


提交佈建要求後，最多需要 30 天才會啟用帳戶以及使用者的公用 IM 連線功能。

## 啟用同盟與公用 IM 連線 (PIC)

提交佈建要求後，即可專心著眼於設定 Lync-Skype 連線所需的 Lync Server 環境與系統管理工作。本節假定 Lync Server 系統管理員已部署 Lync Server 並設定外部存取。如需針對 Lync Server 設定外部存取的額外資訊，請參閱＜規劃外部使用者存取＞( [http://go.microsoft.com/fwlink/p/?LinkID=273772](http://go.microsoft.com/fwlink/p/?linkid=273772)) 以及＜部署外部使用者存取＞( [http://go.microsoft.com/fwlink/p/?LinkID=27378](http://go.microsoft.com/fwlink/p/?linkid=27378))。

為準備 Lync Server 環境以進行 Lync-Skype 連線，Lync Server 系統管理員必須完成下列三項工作：

## 1\. 設定同盟與 PIC

同盟是 Skype 使用者與組織中的 Lync 使用者進行通訊的必要途徑。公用立即訊息連線 (PIC) 則是一種同盟等級，必須加以設定以讓 Lync 使用者與 Skype 使用者進行通訊。同盟與 PIC 均是使用 Lync Server 控制台進行設定，如下所示。

> [!IMPORTANT]  
> PIC 同盟不再受 Live Communication Server 2005 SP1 或 Office Communications Server 2007 支援。PIC 同盟的支援平台包括 Lync Server 2013、Lync Server 2010 以及 Office Communications Server 2007 R2。



## 2\. 設定至少一項原則以支援同盟使用者存取

系統管理員必須使用 Lync Server 控制台設定一或多項外部使用者存取原則以控制 Skype 使用者是否能與內部 Lync Server 使用者共同作業。

## 3\. 針對 Lync 設定 Skype PIC 提供者設定

系統管理員必須使用 Lync Server 管理命令介面設定 Lync 用戶端原則以將 Skype 顯示為額外 PIC 提供者。

> [!NOTE]  
> 除非您亦有設定至少一項原則 (此程序先前的步驟 2) 以支援公用 IM 連線，否則公用立即訊息連線 (PIC) 服務提供者的使用者將無法參與貴組織中的 IM 或會議。<br />
若要設定同盟與 PIC，請參閱＜啟用或停用同盟及公用 IM 連線＞： <a href="http://go.microsoft.com/fwlink/p/?linkid=306063">http://go.microsoft.com/fwlink/p/?LinkId=306063</a>。<br />
若要設定至少一項原則以支援同盟使用者存取，請參閱＜設定原則以控制公用使用者存取＞： <a href="http://go.microsoft.com/fwlink/p/?linkid=306064">http://go.microsoft.com/fwlink/p/?LinkId=306064</a>。


1.  從 Lync Server 前端伺服器中，開啟 Lync Server 管理命令介面。

2.  執行下列兩項命令：
    
      - Remove-CsPublicProvider -Identity Messenger
    
      - New-CsPublicProvider -Identity Skype -ProxyFqdn federation.messenger.msn.com -IconUrl "https://images.edge.messenger.live.com/Messenger\_16x16.png" -VerificationLevel 2 -Enabled 1

3.  您現在可從 Lync 用戶端中選取 Skype 作為 PIC 提供者，並且透過指定相關 Microsoft 帳戶的方式來新增 Skype 用戶端。此外，已合併並透過其 Microsoft 帳戶登入的 Skype 使用者可以傳送聯絡人授權請求給 Lync 使用者。如需 Microsoft 帳戶的詳細資訊，請參閱[什麼是 Microsoft 帳戶？](https://support.skype.com/en/faq/fa12059/what-is-a-microsoft-account) (英文)。如需將用戶端新增至 Lync 的額外資訊，請參閱[在 Lync Server 2013 中以使用者身分使用 Lync-Skype 連線](lync-server-2013-using-lync-skype-connectivity-as-an-end-user.md)。

4.  如需修改裝載提供者的詳細資訊，請參閱＜建立或編輯主控的 SIP 同盟提供者＞： [http://go.microsoft.com/fwlink/p/?LinkId=306065](http://go.microsoft.com/fwlink/p/?linkid=306065)。

如此即完成伺服器上所需執行的系統管理工作。您現在已可進行 Lync-Skype 連線。

## 其他資源

[在 Lync Server 2013 中以使用者身分使用 Lync-Skype 連線](lync-server-2013-using-lync-skype-connectivity-as-an-end-user.md)

[Provisioning guide for Lync-Skype connectivity in Lync Server 2013](lync-server-2013-provisioning-guide-for-lync-skype-connectivity.md)

