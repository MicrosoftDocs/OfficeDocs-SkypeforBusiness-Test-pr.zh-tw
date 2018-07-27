---
title: Lync Server 2013：以使用者身分使用 Lync-Skype 連線
TOCTitle: 以使用者身分使用 Lync-Skype 連線
ms:assetid: ad22f731-118c-4349-8790-b1a72941cbdd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn440175(v=OCS.15)
ms:contentKeyID: 59602859
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中以使用者身分使用 Lync-Skype 連線

 

_**上次修改主題的時間：** 2014-12-05_

Lync-Skype 連線可讓 Skype 使用者與 Lync 使用者彼此互加為連絡人、交換立即訊息，並進行音訊和視訊通話。當 Skype 使用者新增 Lync 使用者時，Skype 使用者會在 Skype 中建立包含該 Lync 使用者工作階段初始通訊協定 (SIP) 統一資源識別項 (URI) ) 的連絡人。反之，當 Lync 使用者新增 Skype 連絡人時，Lync 使用者會在 Lync 中建立包含該 Skype 使用者 Microsoft 帳戶 (MSA) (而非 Skype 使用者名稱) 的連絡人。

**什麼是 MSA？** Skype 使用者必須以 Microsoft 帳戶 (前稱為 Windows Live ID) 登入 Skype，才可與 Lync 連絡人通訊。Microsoft 帳戶是由一組電子郵件地址與密碼組成，亦可用於登入各種服務，例如 Microsoft OneDrive 儲存空間技術、Windows Phone、Microsoft Xbox LIVE 線上遊戲服務，以及 Microsoft Outlook 訊息與共同作業用戶端 (以及之前的 Microsoft Hotmail 網路電子郵件服務或 Windows Live Messenger)。若您使用電子郵件地址與密碼登入這些或其他服務，表示您已擁有 Microsoft 帳戶。如需建立 Microsoft 帳戶的詳細資料，請參閱 Microsoft 帳戶註冊頁面： [http://go.microsoft.com/fwlink/p/?LinkId=306061](http://go.microsoft.com/fwlink/p/?linkid=306061)。您可以將現有的 Skype 帳戶與 Microsoft 帳戶合併，以透過單一登入存取各種應用程式與服務。帳戶合併後，Skype 使用者就可以傳送聯絡人授權請求給 Lync 使用者。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要讓 Lync 與 Skype 使用者能夠完全彼此通訊，必須符合下列需求：
<ul>
<li><p>Skype 使用者必須以 Microsoft 帳戶 (MSA) 登入其 Skype 用戶端。</p></li>
<li><p>Lync 使用者必須由其 Lync 系統管理員啟用公用 IM 連線功能。</p></li>
<li><p>在 Skype 使用者新增 Lync 連絡人時，確認連絡人名稱下方顯示 &quot;Lync&quot; 的字樣，代表找到 Lync URI。</p></li>
<li><p>在 Skype 使用者新增 Lync 連絡人而該 Lync 網域沒有傳回任何搜尋結果時，代表 PIC 佈建程序可能尚未完成，或 Lync 網域尚未設定。</p></li>
<li><p>根據 Lync 與 Skype 使用者的隱私權設定，在各個使用者接受新連絡人之前，IM、視訊與目前狀態可能無法運作。</p></li>
</ul></td>
</tr>
</tbody>
</table>


**若要新增 Skype 連絡人至 Lync 2013**

1.  從 Lync 中，依序按下 \[新增連絡人\] 與 \[新增非組織內部的連絡人\] 。

2.  從可用聯絡人提供者清單中，選擇 \[Skype\] ，如下所示。
    
    ![顯示如何新增 Skype 連絡人的 Lync 用戶端](images/Dn440175.ac4e2f21-c1d9-47d8-b99e-d49fe4eb36d7(OCS.15).jpg "顯示如何新增 Skype 連絡人的 Lync 用戶端")

3.  在 \[IM 位址\] 欄位中，輸入 Skype 使用者的 Microsoft 帳戶 (MSA)。

4.  在 \[新增至連絡人群組\] 下拉式方塊中，選取要新增使用者的連絡人群組。

5.  在 \[設定隱私權關係\] 下拉式方塊中，選取適當的連絡人設定並按下 **\[確定\]**。

6.  使用者現在將顯示為 Lync 中的連絡人。選取使用者，以滑鼠右鍵按一下使用者名稱，然後按一下 \[查看連絡人卡片\] 以檢視使用者內容。如下所示，您也可以依序按下 \[通話\] 與 \[Lync 通話\]，藉此與新增的 Skype 使用者建立音訊或視訊通話。
    
    ![啟動撥打到連絡人之 Lync 電話的 Lync 用戶端](images/Dn440175.cd7cb21a-87f7-4bfa-b30c-980d4098d226(OCS.15).jpg "啟動撥打到連絡人之 Lync 電話的 Lync 用戶端")

如需連絡人支援的額外資訊，請參閱＜ [在 Lync 中新增連絡人](http://office.microsoft.com/zh-tw/office365-lync-online-help/add-a-contact-in-lync-ha102828922.aspx)＞以及＜ [在 Lync 中新增外部連絡人](http://office.microsoft.com/zh-tw/office365-lync-online-help/add-an-external-contact-in-lync-ha104038998.aspx?ctt=5%26origin=ha102828922)＞

當 Skype 使用者的 Microsoft 帳戶使用自訂網域名稱 (例如 **bob@contoso.com**) 時，Lync 使用者將該 Microsoft 帳戶新增至 Lync 的方法有二：

1.  使用 \[新增連絡人\] 圖示，或是

2.  使用 \[尋找某人或某間聊天室，或是撥打某個號碼\] 欄位。

在各個案例中，Lync 使用者必須以下列格式輸入 Skype 使用者的電子郵件： **user(domain name)@msn.com**。

> [!IMPORTANT]  
> 使用下列網域名稱的 Microsoft 帳戶無需執行此步驟： <strong>@live.com、@hotmail.com 或 @outlook.com</strong>。如需支援的自訂網域名稱的詳細資訊，請參閱＜ <a href="http://support.microsoft.com/kb/897567">支援的公用 IM 網域</a>＞。



**若要使用自動網域名稱將 Skype 連絡人新增至 Lync**

1.  從 Lync 中，依序按下 \[新增連絡人\] 與 \[新增非組織內部的連絡人\] 。

2.  從可用聯絡人提供者清單中，選擇 \[Skype\] ，如下所示。
    
    ![顯示如何新增 Skype 連絡人的 Lync 用戶端](images/Dn440175.ac4e2f21-c1d9-47d8-b99e-d49fe4eb36d7(OCS.15).jpg "顯示如何新增 Skype 連絡人的 Lync 用戶端")

3.  在 \[IM 位址\] 欄位中，以 **user(domain name)@msn.com** 的格式輸入 Skype 使用者的 Microsoft 帳戶 (MSA)。因此就使用者 bob@contoso.com 來說，輸入內容應為 **bob(contoso.com)@msn.com**，如下所示。
    
    ![Lync 用戶端的 \[新建連絡人\] 設定](images/Dn440175.422e69b5-2c0c-4260-858f-f10309af772f(OCS.15).jpg "Lync 用戶端的 [新建連絡人] 設定")

4.  在 \[新增至連絡人群組\] 下拉式清單方塊中，選取要新增使用者的連絡人群組。

5.  在 \[設定隱私權關係\] 下拉式清單方塊中，選取適當的連絡人設定，然後按一下 \[確定\] 。

6.  Lync 使用者亦可使用 Lync 中的 \[尋找某人或某間聊天室，或是撥打某個號碼\] 欄位，並新增類似 **user(domain name)@msn.com** 的地址。因此對於 Microsoft 帳戶 bob@contoso.com 來說，輸入內容應為 **bob(contoso.com)@msn.com**，如下所示。
    
    ![在 Lync 用戶端中搜尋連絡人](images/Dn440175.69787db8-f9b9-49e5-b197-b90b10393301(OCS.15).jpg "在 Lync 用戶端中搜尋連絡人")

7.  按照本程序先前的步驟 4 與 5 操作，將連絡人新增至連絡人群組並選取適當的隱私權關係。

**若要新增 Lync 連絡人至 Skype**

1.  登入至 Skype。Skype 使用者必須以 Microsoft 帳戶 (MSA) 登入至其 Skype 用戶端。
    
    ![Skype 用戶端的 \[登入\] 頁面](images/Dn440175.b4fd7c5a-be35-4205-80c7-872863b7a91d(OCS.15).jpg "Skype 用戶端的 [登入] 頁面")

2.  選取 \[新增連絡人\] 圖示。

3.  輸入 Lync 使用者的 SIP URI，例如 bob@contoso.com。

4.  當 Skype 在搜尋結果中找到相符項目時，請在 Lync 使用者名稱下方尋找 **Lync** 的字樣，代表 Skype 已成功找到 Lync 用戶端的 SIP URI。請按下該名稱。
    
    ![顯示 Lync 連絡人的 Skype 用戶端](images/Dn440175.4e690a72-1a54-4442-89cf-0fb45ac5f56a(OCS.15).jpg "顯示 Lync 連絡人的 Skype 用戶端")

5.  在視窗的右上角，按一下 \[新增至連絡人\]。

6.  新連絡人現已新增至您的連絡人清單，但除非對方接受您的要求，否則畫面上只會顯示問號，而非其狀態圖示。當您的新連絡人接受您的要求後，您將能夠看到對方何時上線、啟動 IM 交談，以及進行音訊和視訊通話。
    
    ![與 Lync 連絡人的 Skype 用戶端 IM 交談](images/Dn440175.86ca6f81-4db9-45ba-8511-1f7541aaf066(OCS.15).jpg "與 Lync 連絡人的 Skype 用戶端 IM 交談")
    
    > [!IMPORTANT]  
    > Lync Server 系統管理員必須將 Lync 使用者的原則設定設為允許傳入要求。如果沒有，則 Lync 使用者將不會收到來自 Skype 使用者的連絡人要求。根據 Lync 使用者的原則設定而定，新增 Skype 使用者的要求將顯示在 Lync 用戶端的 [新增] 索引標籤中。若要開始與 Skype 使用者進行通訊，Lync 使用者必須將 Skype 使用者新增至 [我的最愛] 清單或連絡人清單。下方影像顯示 [新增] 索引標籤在 Lync 用戶端中的位置。
    
    
    ![Lync 用戶端的 \[新建連絡人\] 頁面](images/Dn440175.b1cf8570-1401-47d9-ab14-b04f0d7e8a7a(OCS.15).jpg "Lync 用戶端的 [新建連絡人] 頁面")

Lync 使用者必須設定 Lync 通知，確保由 Skype 使用者傳送的要求會顯示於畫面中，並可供 Lync 使用者搜尋。若要設定 Lync 通知，請完成下列程序。

**若要設定 Lync 通知**

1.  從 Lync 用戶端中，按一下 \[選項\] 圖示。

2.  選取 \[通知\] 。

3.  在 \[一般通知\] 下，勾選 \[有人將我加入連絡人清單時通知我\] 。

4.  在 \[未使用 Lync 的連絡人\] 下，選取 \[允許邀請，但封鎖其他所有通訊\] 。

5.  按一下 \[確定\] 以關閉 \[選項\] 視窗。

![Lync 用戶端的 \[選項\] 對話方塊，\[警示\] 頁面](images/Dn440175.b36ed67f-f394-4f66-b60a-b74793001bfc(OCS.15).jpg "Lync 用戶端的 [選項] 對話方塊，[警示] 頁面")

