---
title: 移轉撥入存取號碼
TOCTitle: 移轉撥入存取號碼
ms:assetid: e0dfaed2-64c7-45cb-aaa9-d6117a26625d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721909(v=OCS.15)
ms:contentKeyID: 49890347
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉撥入存取號碼

 

_**上次修改主題的時間：** 2012-10-19_

將撥入存取號碼從 Lync Server 2010 移轉至 Lync Server 2013 需要執行 **Move-CsApplicationEndpoint** Cmdlet，以移轉連絡人物件。在 Lync Server 2010 與 Lync Server 2013 共存期間，您在 Lync Server 2013 建立的撥入存取號碼行為類似於您在 Lync Server 2010 建立的撥入存取號碼，如本節所述。

您在 Lync Server 2010 建立但已移至 Lync Server 2013 的撥入存取號碼，或是您在移轉之前、移轉期間或移轉之後，在 Lync Server 2013 建立的撥入存取號碼，具備下列特性：

  - 不會出現在 Office Communications Server 2007 R2 會議邀請或撥入存取號碼頁面上。

  - 出現在 Lync Server 2010 會議邀請及撥入存取號碼頁面。

  - 出現在 Lync Server 2013 會議邀請及撥入存取號碼頁面。

  - 無法以 Office Communications Server 2007 R2 系統管理工具檢視或修改。

  - 無法以 Lync Server 2010 控制台和以 Lync Server 2010 管理命令介面檢視或修改。

  - 無法以 Lync Server 2013 控制台和以 Lync Server 2013 管理命令介面檢視或修改。

  - 可以使用 Set-CsDialinConferencingAccessNumber Cmdlet 搭配 Priority 參數在此區域中進行重新排序。

您必須在解除委任 Lync Server 2010 集區之前，完成指向 Lync Server 2010 之撥入存取號碼的移轉作業。若未完成下列程序所述的撥入存取號碼移轉，所有傳入該存取號碼的通話將會失敗。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須在解除委任 Lync Server 2010 集區之前執行此程序。</td>
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
<td>建議在網路使用量較低時移動撥入存取號碼，以避免服務出現短暫中斷的情況。</td>
</tr>
</tbody>
</table>


**識別及移動撥入存取號碼**

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  將每組撥入存取號碼移至 Lync Server 2013 上所執行的集區，然後從命令列中執行：
    
        Move-CsApplicationEndpoint -Identity <SIP URI of the access number to be moved> -Target <FQDN of the pool to which the access number is moving>

3.  開啟 Lync Server 控制台。

4.  在左導覽列中，按一下 \[會議\] 。

5.  按一下 \[撥入存取號碼\] 索引標籤。

6.  確認您在移轉的 Lync Server 2010 集區中已無任何撥入存取號碼。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當所有撥入存取號碼均指向 Lync Server 2013 集區時，即可解除委任 Lync Server 2010 集區。</td>
    </tr>
    </tbody>
    </table>


**使用 Lync Server 控制台驗證移轉的撥入存取號碼**

1.  使用指派到 **CsUserAdministrator** 角色或 **CsAdministrator** 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟 Lync Server 控制台。

3.  在左導覽列中，按一下 \[會議\] 。

4.  按一下 \[撥入存取號碼\] 索引標籤。

5.  確認所有撥入存取號碼均已移轉到 Lync Server 2013 上裝載的集區。

**使用 Lync Server 管理命令介面驗證移轉的撥入存取號碼**

1.  開啟 Lync Server 管理命令介面。

2.  若要傳回移轉的所有撥入會議存取號碼，請從命令列中執行：
    
        Get-CsDialInConferencingAccessNumber -Filter {Pool -eq "<FQDN of the pool to which the access number is moved>"}

3.  確認所有撥入存取號碼均已移轉到 Lync Server 2013 上裝載的集區。

