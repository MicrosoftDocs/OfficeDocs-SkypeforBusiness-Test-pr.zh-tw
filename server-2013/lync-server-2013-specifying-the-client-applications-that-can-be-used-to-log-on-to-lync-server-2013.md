---
title: 指定可用來登入 Lync Server 2013 的用戶端應用程式
TOCTitle: 指定可用來登入 Lync Server 2013 的用戶端應用程式
ms:assetid: d256a581-9a48-4d1a-82cc-2e1f520d7d2e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182591(v=OCS.15)
ms:contentKeyID: 49292398
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指定可用來登入 Lync Server 2013 的用戶端應用程式

 

_**上次修改主題的時間：** 2012-12-11_

Lync Server 2013 可讓您指定環境中支援的用戶端版本。當執行不同版本的兩個用戶端互動時，這兩個用戶端可用的功能會受限於雙方的功能。為了妥善運用 Lync Server 2013 中包含的功能，並且改善整體使用者經驗，您可以使用用戶端版本篩選器來限制 Lync Server 2013 環境中使用的用戶端版本。使用用戶端版本篩選器還可幫助您降低支援多個用戶端版本的相關成本。

除了建立全域原則之外，您還可以為特定服務或網站建立用戶端版本原則，或是建立可指派給個別使用者的使用者範圍原則。使用者範圍用戶端版本原則可以指派給 Lync Server 控制台中 \[使用者\] 群組的個別使用者。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由於匿名使用者不會與使用者、網站或服務產生關聯，因此匿名使用者只會受全域層級的原則影響。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>篩選器會依優先順序列出。例如，如果您有一個可讓執行 1.5 版的用戶端連線的篩選器，後面接著一個封鎖執行 2.0 以前版本之用戶端的篩選器，則第一個篩選器的優先順序高於第二個，而且執行 1.5 版的用戶端可以連線。</td>
</tr>
</tbody>
</table>


## 編輯預設用戶端版本原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[用戶端\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>[用戶端版本原則]</strong> 索引標籤預設為已選取。</td>
    </tr>
    </tbody>
    </table>


4.  在 **\[用戶端版本原則\]** 頁面上，按兩下清單中的 **\[通用\]** 原則。

5.  在 **\[編輯用戶端版本原則\]** 中，執行下列其中一項操作：
    
      - 按一下 **\[新增\]** 建立新的用戶端版本規則。
    
      - 按一下清單中的其中一個已定義的用戶端類型，然後按一下 \[顯示詳細資料\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以使用萬用字元表示用戶端類型。</td>
    </tr>
    </tbody>
    </table>


6.  在 \[使用者代理程式\] 中，選取用戶端類型。

7.  在 **\[版本號碼\]** 下，執行下列操作：
    
      - 在 **\[主要版本\]** 中，輸入對應至用戶端主要版本的號碼。
    
      - 在 **\[次要版本\]** 中，輸入對應至用戶端次要版本的號碼。
    
      - 在 **\[組建\]** 中，輸入對應至用戶端主要和次要版本的號碼。
    
      - 在 **\[更新\]** 中，輸入對應至用戶端更新版本的號碼。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以使用萬用字元表示用戶端版本號碼。</td>
    </tr>
    </tbody>
    </table>


8.  若要指定您在前述步驟中所指定用戶端版本的比對作業，請在 \[比較作業\] 中，按下列其中一項：
    
      - **相同**
    
      - **不相同**
    
      - **新於**
    
      - **新於或相同**
    
      - **舊於**
    
      - **舊於或相同**

9.  若要指定符合前述步驟中的準則時執行的動作，請按一下 \[動作\] 中的下列其中一項：
    
      - 若要允許用戶端登入，請按一下 **\[允許\]**。
    
      - 若要允許用戶端登入並且從 Windows Server Update Service 或 Microsoft Update 接收更新，請按一下 \[允許並升級\]。此動作只有在選取「使用者代理程式 OC」時才可使用。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>選取此動作會在使用者下次登入 Lync 2013 時出現通知。通知指出有可用的更新，即使更新還沒有發佈至 Windows Server Update Service 或 Microsoft Update。為避免混淆，您應該僅在有可用更新時選擇此動作。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要允許用戶端登入並且顯示哪裡可以下載其他用戶端版本的訊息，請按一下 **\[以 URL 允許\]**。您稍後會在此程序中指定 URL。
    
      - 若要防止用戶端登入，請按一下 **\[封鎖\]**。
    
      - 若要防止用戶端登入，但是允許用戶端從 Windows Server Update Service 或 Microsoft Update 接收更新，請按一下 \[封鎖並升級\]。此動作只有在選取「使用者代理程式 OC」時才可使用。
    
      - 若要防止用戶端登入並且顯示哪裡可以下載其他用戶端版本的訊息，請按一下 **\[以 URL 封鎖\]**。您稍後會在此程序中指定 URL。

10. (選用) 如果您已在前一個步驟按一下 **\[以 URL 允許\]** 或 **\[以 URL 封鎖\]**，請在 **\[URL\]** 中輸入要包含在訊息中的用戶端下載 URL。

11. 按一下 **\[確定\]**，然後再按一下 **\[認可\]**。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中管理裝置、電話及用戶端應用程式](lync-server-2013-managing-devices-phones-and-client-applications.md)

