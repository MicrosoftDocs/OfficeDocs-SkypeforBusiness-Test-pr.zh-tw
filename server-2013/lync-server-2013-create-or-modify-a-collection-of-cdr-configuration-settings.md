---
title: 建立或修改 CDR 組態設定集合
TOCTitle: 建立或修改 CDR 組態設定集合
ms:assetid: c830be5a-2a82-468d-9c46-d3fec0f79fd0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721878(v=OCS.15)
ms:contentKeyID: 49890308
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改 CDR 組態設定集合

 

_**上次修改主題的時間：** 2015-03-09_

詳細通話記錄 (CDR) 可讓您追蹤對等立即訊息工作階段、Voice over Internet Protocol (VoIP) 電話通話以及會議通話的使用情形。這項使用資料包括撥號方、收話方、通話時間及通話時間長度等資訊。

當您安裝 Microsoft Lync Server 2013 時，系統會為您建立單一的全域 CDR 組態設定集合。系統管理員也可以選擇建立網站範圍的自訂設定。這些網站範圍的設定在每次使用時，都會蓋過全域設定。例如，如果您為 Redmond 網站建立網站範圍的設定，則系統會使用那些設定 (而非全域設定) 來管理 Redmond 的 CDR。

您可以使用 Lync Server 控制台或 [New-CsCdrConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsCdrConfiguration) Cmdlet 建立 CDR 組態設定。您可以使用 Lync Server 控制台或 [Set-CsCdrConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCdrConfiguration) Cmdlet 修改現有的設定。如果您使用 Lync Server 控制台建立或修改設定，將可以使用下列選項：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>UI 設定</th>
<th>PowerShell 參數</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>名稱</p></td>
<td><p>Identity</p></td>
<td><p>所建立 CDR 組態設定的唯一識別碼。您只能在網站範圍建立這些設定。</p></td>
</tr>
<tr class="even">
<td><p>啟用監視 CDR</p></td>
<td><p>EnableCDR</p></td>
<td><p>表示是否啟用 CDR。</p></td>
</tr>
<tr class="odd">
<td><p>啟用清除 CDR</p></td>
<td><p>EnablePurging</p></td>
<td><p>表示是否要從 CDR 資料庫定期刪除 CDR 記錄。</p></td>
</tr>
<tr class="even">
<td><p>將 CDR 保留最大持續期限 (天)</p></td>
<td><p>KeepCallDetailForDays</p></td>
<td><p>表示在 CDR 資料庫保留 CDR 記錄的天數。任何超過指定天數的記錄都將自動刪除。(請注意，只有在啟用清除時，才會進行清除)。</p></td>
</tr>
<tr class="odd">
<td><p>將錯誤報告資料保留最大持續期限 (天)</p></td>
<td><p>KeepErrorReportForDays</p></td>
<td><p>表示保留 CDR 錯誤報告的天數。任何超過指定天數的報告都將自動刪除。CDR 錯誤報告是由用戶端應用程式所上傳的診斷報告。</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>New-CsCdrConfiguration 和 Set-CsCdrConfiguration Cmdlet 包含 Lync Server 控制台 中沒有的其他選項。如需詳細資訊，請參閱 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsCdrConfiguration">New-CsCdrConfiguration</a> 和 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCdrConfiguration">Set-CsCdrConfiguration</a> 說明主題。</td>
</tr>
</tbody>
</table>


## 使用 Lync Server 控制台 建立 CDR 組態設定

1.  在 Lync Server 控制台中，按一下 \[監控和封存\]。

2.  在 \[詳細通話記錄\] 索引標籤上，按一下 \[新增\]。

3.  在 \[選取站台\] 對話方塊中，選取要建立新組態設定的網站。如果對話方塊是空的，那表示您的網站已全都被指派一組 CDR 組態設定的集合。每個網站都只能有一組這樣的集合。在那種情況下，您可以刪除再重新建立設定，或是只修改現有的設定。

4.  在 \[新的詳細通話記錄 (CDR) 設定\] 對話方塊中，進行想要的選擇然後按一下 \[認可\]。

## 使用 Lync Server 控制台修改現有的 CDR 組態設定

1.  在 Lync Server 控制台中，按一下 \[監控和封存\]。

2.  按兩下要修改的設定集合，或者是選取集合、按一下 \[編輯\]，然後按一下 \[顯示詳細資料\]。請注意，您一次只能修改單一集合。若要對多個集合進行相同的變更，請改用 Lync Server 管理命令介面。

3.  在 \[編輯詳細通話記錄 (CDR) 設定\] 對話方塊中，進行想要的選擇然後按一下 \[認可\]。

## 使用 Lync Server 管理命令介面 Cmdlet 建立 CDR 組態設定

您可以使用 Windows PowerShell 及 **New-CsCdrConfiguration** Cmdlet 建立 CDR 組態設定。您可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 建立新的 CDR 組態設定集合

  - 此命令會建立套用於 Redmond 網站的新 CDR 組態設定集合：
    
        New-CsCdrConfiguration -Identity "site:Redmond"

## 建立停用詳細通話記錄的 CDR 組態設定集合

  - 由於上述的命令除了指定必要的 Identity 參數以外，並未指定任何其他參數，因此新組態設定集合的所有屬性都將使用預設值。若要建立使用不同屬性值的設定，只要加上適當的參數和參數值即可。例如，若要建立預設允許停用詳細通話記錄的詳細通話組態設定集合，請使用類似如下的命令：
    
        New-CsCdrConfiguration -Identity "site:Redmond" -EnableCDR $False

## 建立新的 CDR 組態設定集合時指定多個屬性值

  - 您可以加上多個參數來修改多個屬性值。例如，此命令會將新的設定設成保留詳細通話記錄 30 天，並保留錯誤報告 90 天：
    
        New-CsCdrConfiguration -Identity "site:Redmond" -KeepCallDetailForDays 30 -KeepErrorReportForDays 90

如需詳細資訊，請參閱 [New-CsCdrConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsCdrConfiguration) Cmdlet 的說明主題。

