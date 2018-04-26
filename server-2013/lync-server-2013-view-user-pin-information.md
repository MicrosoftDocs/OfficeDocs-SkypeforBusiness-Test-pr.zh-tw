---
title: 檢視使用者 PIN 資訊
TOCTitle: 檢視使用者 PIN 資訊
ms:assetid: 59e38117-8112-4851-82ac-a746ffa0f89d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688067(v=OCS.15)
ms:contentKeyID: 49890081
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視使用者 PIN 資訊

 

_**上次修改主題的時間：** 2013-02-23_

若要以經過驗證的使用者身分加入電話撥入式會議，具有 Active Directory 網域服務 (AD DS) 認證的 Lync Server 2013 使用者需要個人識別碼 (PIN)。您可以從 Lync Server 2013 控制台檢視使用者的 PIN 資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以檢視諸如是否已設定 PIN 或上次變更 PIN 的時間之類的 PIN 狀態資訊，但無法藉由查看 PIN 狀態來查看目前的 PIN。如果使用者遺失他們的 PIN，您可以遵循<a href="lync-server-2013-set-a-user-s-dial-in-conferencing-pin.md">在 Lync Server 2013 中設定使用者的電話撥入式會議 PIN</a>中的程序來重設 PIN</td>
</tr>
</tbody>
</table>


## 在 Lync Server 控制台中檢視使用者的 PIN

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[使用者\]。

4.  使用下列其中一個方法來尋找使用者：
    
      - 在 \[搜尋使用者\] 方塊中，鍵入完整或第一個部分的顯示名稱、姓氏、名字、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或使用者帳戶的統一資源識別項 (URI)，然後按一下 \[尋找\]。
    
      - 如果您已儲存查詢，請按一下 \[開啟查詢\] 圖示、使用 \[開啟\] 對話方塊來擷取查詢 (.usf 檔)，然後按一下 \[尋找\]。

5.  (選用) 指定其他搜尋條件，縮減結果：
    
    1.  按一下 \[新增篩選\]。
    
    2.  輸入使用者內容，您可以自行輸入或按一下下拉式清單的箭頭以選取內容。
    
    3.  在 \[等於\] 下拉式清單中，按一下運算子 (例如 \[等於\] 或 \[不等於\])。
    
    4.  視您選取的使用者內容而定，透過直接輸入文字或按下拉式清單中的箭頭，輸入您要用來篩選搜尋結果的準則。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>若要將更多搜尋子句加入至查詢，請按一下 [新增篩選]。</td>
        </tr>
        </tbody>
        </table>
    
    5.  按一下 \[尋找\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果 PIN 已鎖定，您必須解除鎖定 PIN，才能設定 PIN。若要解除鎖定 PIN，請依序按一下使用者、[執行] 和 [解除鎖定 PIN]。</td>
    </tr>
    </tbody>
    </table>


6.  依序按一下搜尋結果中的使用者、\[執行\] 和 \[檢視 PIN 狀態\]。

## 使用 Lync Server 管理命令介面 Cmdlet 來檢視使用者 PIN 資訊

您可以使用 Get-CsClientPinInfo Cmdlet 來檢視使用者 PIN 資訊。此 Cmdlet 可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視使用者 PIN 資訊

  - 若要檢視使用者的 PIN 資訊，請在 Lync Server 管理命令介面中鍵入如下的命令，然後按 ENTER：
    
        Get-CsClientPinInfo -Identity "Ken Myer"
    
    即會傳回類似下列的資訊：
    
        Identity          : sip:kenmyer@litwareinc.com
        IsPinSet          : False
        IsLockedOut       : False
        LastPinChangeTime : 9/25/2012 1:35:03 PM
        PinExpirationTime :

如需詳細資訊，請參閱適用於 [Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md) Cmdlet 的說明主題。

## 請參閱

#### 工作

[在 Lync Server 2013 中設定使用者的電話撥入式會議 PIN](lync-server-2013-set-a-user-s-dial-in-conferencing-pin.md)  
[鎖定或解除鎖定使用者 PIN](lync-server-2013-lock-or-unlock-a-user-pin.md)

