---
title: Lync Server 2013：設定使用者的電話撥入式會議 PIN
TOCTitle: 設定使用者的電話撥入式會議 PIN
ms:assetid: 4252b5a5-4267-4513-b18e-0253a8d66f72
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520985(v=OCS.15)
ms:contentKeyID: 49290734
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定使用者的電話撥入式會議 PIN

 

_**上次修改主題的時間：** 2014-06-10_

若要以經過驗證的使用者身分加入電話撥入式會議，具有 Active Directory 網域服務 (AD DS) 認證的 Lync Server 2013 使用者需要個人識別碼 (PIN)。如果使用者忘記電話撥入式會議 PIN 或未使用 Lync Server 來設定 PIN，您可以從 Lync Server 控制台設定使用者的 PIN。您可以讓系統自動產生 PIN 或自行手動建立 PIN。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PIN 的特定特性 (例如最小長度) 可以以原則形式設定。除了全域原則，您還可以為個別網站或使用者設定 PIN 原則。如需設定 PIN 原則的詳細資訊，請參閱＜ <a href="lync-server-2013-configure-dial-in-conferencing-personal-identification-number-pin-rules.md">在 Lync Server 2013 中設定電話撥入式會議個人識別碼 (PIN) 規則</a>＞。</td>
</tr>
</tbody>
</table>


## 設定使用者的 PIN

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，按一下 \[使用者\] 。

4.  使用下列其中一種方法，找到使用者：
    
      - 在 \[搜尋使用者\] 方塊中，輸入該使用者帳戶的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或線路統一資源識別項 (URI) 的全部或頭幾個字，然後按一下 \[尋找\] 。
    
      - 如果有儲存的查詢，請按一下 \[開啟查詢\] 圖示、使用 \[開啟\] 對話方塊擷取查詢 (.usf 檔)，然後按一下 \[尋找\] 。

5.  (選用) 指定其他搜尋條件，縮減結果：
    
    1.  按一下 \[新增篩選\] 。
    
    2.  輸入使用者內容，您可以自行輸入或按一下下拉式清單的箭頭以選取內容。
    
    3.  在 \[等於\] 下拉式清單中，按一下運算子 (例如\[等於\] 或 \[不等於\] )。
    
    4.  視您選取的使用者內容而定，透過直接輸入文字或按下拉式清單中的箭頭，輸入您要用來篩選搜尋結果的準則。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>若要將更多搜尋子句加入至查詢，請按一下 [新增篩選] 。</td>
        </tr>
        </tbody>
        </table>
    
    5.  按一下 \[尋找\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果 PIN 已鎖定，您必須解除鎖定 PIN，才能設定 PIN。若要解除鎖定 PIN，請依序按一下使用者、 <strong>[執行]</strong> 和 <strong>[解除鎖定 PIN]</strong> 。</td>
    </tr>
    </tbody>
    </table>


6.  依序按一下搜尋結果中的使用者、 **\[執行\]** 和 **\[設定 PIN\]** 。

7.  在 **\[設定 PIN\]** 對話方塊中，執行下列其中一個動作：
    
      - 若要允許 Lync Server 2013 產生使用者的 PIN，請選取 **\[自動產生有效的 PIN\]** (預設)。
    
      - 若要建立您自己的 PIN，請按一下 **\[手動輸入特定的 PIN\]** ，按一下文字方塊，然後輸入符合 PIN 原則設定中指定的 PIN 需求的 PIN。

8.  按一下 \[確定\] 。

9.  在 **\[設定 PIN\]** 中，執行下列其中一個動作：
    
      - 選取 **\[顯示 PIN\]** 核取方塊來查看 PIN，然後使用組織的慣用方法，複製 PIN 並傳送給使用者。
    
      - 按一下 **\[開啟我的電子郵件應用程式，將新的 PIN 傳送給使用者\]** ，以電子郵件傳送 PIN。如果電子郵件用戶端是 Microsoft Office Outlook，PIN 會自動複製到新的電子郵件。如果您使用不同的電子郵件用戶端，請選取 **\[顯示 PIN\]** 核取方塊來查看 PIN，然後複製到電子郵件。

10. 按一下 \[關閉\] 。

## 使用 Windows PowerShell Cmdlet 指派使用者 PIN

您可以使用 Set-CsClientPin Cmdlet 指派 PIN 號碼。您可從 Lync Server 2013 管理命令介面 或 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 自動指派 PIN 號碼給使用者

  - 下列命令指派 PIN 號碼給使用者 Ken Myer。由於不包含 Pin 參數， Lync Server 將自動產生並指派 PIN 號碼。
    
        Set-CsClientPin -Identity "Ken Myer" 

## 指派特定 PIN 號碼給使用者

  - 此命令使用 Pin 參數指派 PIN 號碼 121989 給使用者 Ken Myer。
    
        Set-CsClientPin -Identity "Ken Myer" -Pin 121989

如需詳細資訊，請參閱 [Set-CsClientPin](set-csclientpin.md) Cmdlet 的說明主題。

## 請參閱

#### 概念

[電話撥入式會議存取號碼](https://technet.microsoft.com/zh-tw/library/gg133674\(v=ocs.15\))  

#### 其他資源

[在 Lync Server 2013 中設定電話撥入式會議個人識別碼 (PIN) 規則](lync-server-2013-configure-dial-in-conferencing-personal-identification-number-pin-rules.md)

