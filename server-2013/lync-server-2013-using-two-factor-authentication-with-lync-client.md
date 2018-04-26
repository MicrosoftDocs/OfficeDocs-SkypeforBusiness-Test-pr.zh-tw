---
title: 配合 Lync 用戶端使用雙因素驗證
TOCTitle: 配合 Lync 用戶端使用雙因素驗證
ms:assetid: d4136e61-c3ab-4b26-85c8-c1b2c24f5ee3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn338071(v=OCS.15)
ms:contentKeyID: 56269154
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 配合 Lync 用戶端使用雙因素驗證

 

_**上次修改主題的時間：** 2015-03-09_

此主題說明如何配合 Lync 2013 用戶端運用雙因素驗證。

## 第一次登入 Lync 2013

您的 Lync 登入資訊通常是在安裝 Lync 2013 時自動設定。然而當您第一次使用 Lync 時，可能需要手動啟動用戶端。

**第一次登入 Lync**

1.  登入貴組織的網路。

2.  選取 **\[開始\]** \> **\[所有程式\]** \> **\[Microsoft Lync\] \> \[Lync 2013\]**。
    
    您應會看見 Lync 登入畫面。
    
      - 如果登入位址方塊已填入內容，請確認顯示的位址是正確的。
    
      - 如果位址不正確，或方塊內容為空白，請輸入您的 Lync 登入位址 (一般會是您的電子郵件地址)。
    
      - 如果顯示空白的密碼方塊，請新增密碼。

3.  選取 **\[登入\]**。

## 登出 Lync

使用完 Lync 後，可以關閉顯示畫面、登出工作階段，或是結束程式，這些動作全部都可從 \[檔案\] 功能表中執行。 下表說明選項之間的差異。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>選項</th>
<th>功能</th>
<th>執行方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>關閉</p></td>
<td><p>關閉 Lync 顯示畫面，但允許您使用者 ID 所識別的 Lync 工作階段繼續執行，以便您繼續取得通知，並且與其他人互動。</p>
<p>您可以隨時恢復顯示畫面，按一下工作列中的 Lync 圖示，或是按一下螢幕底部的通知區域即可。</p></td>
<td><p>在 Lync 主視窗中，執行下列其中一個動作：</p>
<ol>
<li><p>選取 <strong>[選項]</strong> 按鈕，接著選取 <strong>[檔案]</strong> &gt; <strong>[關閉]</strong>。</p></li>
<li><p>按一下視窗右上角的 <strong>[關閉]</strong> 按鈕 (X)。</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>登出</p></td>
<td><p>結束與您使用者識別碼相關聯的 Lync 工作階段，但 Lync 仍會在背景中繼續執行。您登出後，就會顯示登入視窗。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以在登出時，選取 <strong>[刪除我的登入資訊]</strong>，即可從電腦移除您的登入識別碼與密碼記錄。 這樣做可能會讓支援人員更容易疑難排解登入問題。也會讓未經授權的使用者更難使用您的認證登入，進而有助於確保您的登入資訊更加安全。</td>
</tr>
</tbody>
</table>

</div></td>
<td><p>在 Lync 主視窗中，選取 [選項] 按鈕，然後按一下 [檔案] <strong>&gt; [登出]</strong>。</p></td>
</tr>
<tr class="odd">
<td><p>結束</p></td>
<td><p>結束您的 Lync 工作階段，並關閉電腦上的 Lync。結束之後，如果要重新啟動 Lync ，請按一下 <strong>[開始]</strong> &gt; <strong>[所有程式]</strong> &gt; <strong>[Microsoft Lync]</strong> &gt; <strong>[Lync 2013]</strong>。</p></td>
<td><p>在 Lync 主視窗中，選取 <strong>[選項]</strong> 按鈕，然後選取 <strong>[檔案]</strong> &gt; <strong>[結束]</strong>。</p></td>
</tr>
</tbody>
</table>


## 使用智慧卡登入 Lync

現在部分組織使用稱為雙因素驗證的多步驟登入程序，為 Lync 2013 使用者提升安全性。如果您預期將會採用此一方式，您將需要使用「智慧卡」登入 Lync。智慧卡有兩種類型，分別是實體與虛擬智慧卡。

  - **實體**   大小與信用卡相若。登入時需要將卡片插入智慧卡讀卡機。

  - **虛擬**   並非實體物件，而是寫入您電腦上特殊晶片的電子識別碼，本質上來說就是將智慧卡建置於電腦中。只能與配備有 TPM (信賴平台模組) 晶片的 Windows 8 電腦配合使用。

## 註冊您的智慧卡

您必須先註冊智慧卡，才能使用該卡登入—也就是說，卡片身分必須等同您的使用者認證。無論智慧卡為實體或虛擬形式皆為如此。您的 Lync Server 系統管理員可能已進行過此程序。如果您不確定是否已進行此程序，請詢問您的系統管理員。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由於每個虛擬智慧卡只會與其安裝所在的裝置相關聯，因此您需要針對每部使用的 Windows 8 電腦註冊個別的智慧卡。</td>
</tr>
</tbody>
</table>


**手動註冊智慧卡**

1.  登入將要執行 Lync 的電腦。

2.  使用 Internet Explorer，瀏覽到您組織的憑證授權單位網頁註冊頁面。
    
    請向您的 Lync Server 系統管理員取得此資源的網址 (如果您尚未取得)。URL 會類似下列範例：https://MyCA.\[yourcompanyname\].com/certsrv。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您使用的是 Internet Explorer 10，您可能需要使用相容模式檢視此網站。</td>
    </tr>
    </tbody>
    </table>


3.  當系統提示您登入憑證頁面，請使用您的網域帳戶 (而不要以電腦的系統管理員身分) 登入。

4.  在網站的歡迎頁面上，選取 **\[要求憑證\]**。

5.  選取 **\[進階要求\]**。

6.  選取 **\[向這個 CA 建立並提交一個要求\]**，接著按 **\[下一步\]**。

7.  現在您會看到名稱為 \[智慧卡註冊站\] 的頁面。核准要求以安裝 ActiveX 控制項，接著完成 \[進階憑證要求\] 表單，如下所示：
    
    1.  從 **\[憑證範本\]** 下拉式清單中選取 **\[智慧卡使用者\]**。
    
    2.  選取 **\[建立新的金鑰組\]**。
    
    3.  找出智慧卡標籤上的製造商資訊，並從 **\[CSP\]** 下拉式清單中選取該製造商。
    
    4.  如果尚未選取要求格式，請選取 **\[CSP\]**。
    
    5.  如果尚未選取，請從 \[雜湊演算法\] 下拉式清單中選取 **\[sha1\]**。
    
    6.  為憑證使用便於識別的名稱，然後按一下 **\[送出\]**。

8.  現在將空白的智慧卡插入連接到註冊站的讀卡機，然後按一下 **\[註冊\]**。

9.  收到提示時，輸入您的個人識別碼 (PIN)，然後按一下 **\[確定\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您的技術支援人員尚未給您用以註冊智慧卡的特殊 PIN，請使用預設智慧卡 PIN 值，亦即 12345678。</td>
    </tr>
    </tbody>
    </table>


10. 請選取於第一次使用智慧卡時強制使用者 (亦即您本身) 變更 PIN 的選項。

11. 現在將空白的智慧卡插入連接到註冊站的讀卡機，然後按一下 **\[註冊\]**。

12. 收到提示時，輸入您的個人識別碼 (PIN)，然後按一下 **\[確定\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您的技術支援人員尚未給您用以註冊智慧卡的特殊 PIN，請使用預設智慧卡 PIN 值，亦即 12345678。</td>
    </tr>
    </tbody>
    </table>


13. 請選取於第一次使用智慧卡時強制使用者 (亦即您本身) 變更 PIN 的選項。

14. 按一下 **\[確定\]** 以確認顯示的憑證含有您的資訊。

15. 當您看到憑證已核發的通知時，請按一下 **\[安裝這個憑證\]** 以完成註冊程序。

## 使用智慧卡認證登入 Lync

在您第一次使用智慧卡之前，建議您在 Lync 登入頁面上按一下 **\[刪除我的登入資訊\]**。如此可以清除任何儲存在您電腦上的登入認證，並去除可能的錯誤來源。

**使用智慧卡認證登入 Lync**

1.  啟動 Lync 用戶端。

2.  在 \[登入\] 畫面上，在 **\[登入位址\]** 方塊中輸入您的登入使用者帳戶名稱，然後按一下 **\[登入\]**。

3.  如果您使用的是虛擬智慧卡，請略過此步驟。
    
    如果您使用的是實體智慧卡，請在收到提示時將智慧卡插入智慧卡讀卡機，然後在偵測到卡片時按一下 **\[確定\]**。

4.  輸入智慧卡的 PIN 號碼，然後按一下 **\[確定\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您的支援人員並未指派智慧卡 PIN 號碼給您，請使用預設值，亦即 12345678。</td>
    </tr>
    </tbody>
    </table>

