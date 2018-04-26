---
title: 建立或修改新的用戶端版本原則規則
TOCTitle: 建立或修改新的用戶端版本原則規則
ms:assetid: 6f879d99-8401-41e0-a562-195c890d63ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ898478(v=OCS.15)
ms:contentKeyID: 52056149
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改新的用戶端版本原則規則

 

_**上次修改主題的時間：** 2013-01-21_

當使用者嘗試以特定用戶端及用戶端版本登入時，用戶端版本原則規則會定義所要採取的動作。您可以從 Lync Server 2013 控制台建立或修改用戶端版本原則的個別規則。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>規則會依優先順序列出。例如，如果您有一個可讓執行 1.5 版的用戶端連線的規則，後面接著一個封鎖執行 2.0 以前版本之用戶端的規則，則第一個規則的優先順序高於第二個，而且執行 1.5 版的用戶端可以連線。</td>
</tr>
</tbody>
</table>


## 使用 Lync Server 控制台建立或修改用戶端版本原則規則

1.  透過 Lync Server 控制台[建立或修改新的用戶端版本原則](lync-server-2013-create-or-modify-a-new-client-version-policy.md)。

2.  在「編輯用戶端版本原則」頁面中，執行下列其中一項動作：
    
      - 按一下 \[新增\] 建立新的用戶端版本規則。
    
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


3.  在 \[使用者代理程式\] 中，選取用戶端類型。

4.  在 \[版本號碼\] 下，執行下列動作：
    
      - 在 \[主要版本\] 中，輸入對應至用戶端主要版本的號碼。
    
      - 在 \[次要版本\] 中，輸入對應至用戶端次要版本的號碼。
    
      - 在 \[組建\] 中，輸入對應至用戶端主要和次要版本的號碼。
    
      - 在 \[更新\] 中，輸入對應至用戶端更新版本的號碼。
    
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


5.  若要指定您在前述步驟中所指定用戶端版本的比對作業，請在 \[比較作業\] 中，按下列其中一項：
    
      - **相同**
    
      - **不相同**
    
      - **新於**
    
      - **新於或相同**
    
      - **舊於**
    
      - **舊於或相同**

6.  若要指定符合前述步驟中的準則時執行的動作，請按一下 \[動作\] 中的下列其中一項：
    
      - 若要允許用戶端登入，請按一下 \[允許\]。
    
      - 若要允許用戶端登入並且從 Windows Server Update Service 或 Microsoft Update 接收更新，請按一下 \[允許並升級\]。此動作只有在選取使用者代理程式 \[OC\] 時才可使用。
        
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
    
      - 若要允許用戶端登入並且顯示哪裡可以下載其他用戶端版本的訊息，請按一下 \[以 URL 允許\]。您稍後會在此程序中指定 URL。
    
      - 若要防止用戶端登入，請按一下 \[封鎖\]。
    
      - 若要防止用戶端登入，但是允許用戶端從 Windows Server Update Service 或 Microsoft Update 接收更新，請按一下 \[封鎖並升級\]。此動作只有在選取使用者代理程式 \[OC\] 時才可使用。
    
      - 若要防止用戶端登入並且顯示哪裡可以下載其他用戶端版本的訊息，請按一下 \[以 URL 封鎖\]。您稍後會在此程序中指定 URL。

7.  (選用) 如果您已在前一個步驟按一下 \[以 URL 允許\] 或 \[以 URL 封鎖\]，請在 \[URL\] 中輸入要包含在訊息中的用戶端下載 URL。

8.  按一下 \[確定\]，然後再按一下 \[認可\]。

