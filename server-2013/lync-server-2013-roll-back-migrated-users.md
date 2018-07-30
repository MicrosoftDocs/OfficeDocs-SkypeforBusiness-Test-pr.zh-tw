---
title: Lync Server 2013：復原已移轉的使用者
TOCTitle: 復原已移轉的使用者
ms:assetid: bfabaf0b-9a42-4057-b729-a7ab9eee8c72
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205224(v=OCS.15)
ms:contentKeyID: 49292188
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中復原已移轉的使用者

 

_**上次修改主題的時間：** 2012-10-07_

如果您需要復原統一的連絡人存放區功能，請只在將使用者移回 Exchange 2010 或 Lync Server 2010 時，才復原連絡人。若要復原，請停用使用者的原則，然後執行 **Invoke-CsUcsRollback** Cmdlet。僅執行 **Invoke-CsUcsRollback** 並無法保證永遠復原，因為如果未停用原則，可能會再次啟動統一的連絡人存放區移轉。例如，如果由於 Exchange 2013 復原為 Exchange 2010 因而復原使用者，接著使用者信箱被移至 Exchange 2013，則只要使用者服務原則中仍啟用統一的連絡人存放區，那麼統一的連絡人存放區移轉會在復原後七天再次啟動。

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
<td><strong>Move-CsUser</strong> Cmdlet 在下列情形會自動將使用者的連絡人存放區從 Exchange 2013 復原為 Lync Server 2013:
<ul>
<li><p>使用者從 Lync Server 2013 移至 Lync Server 2010。</p></li>
<li><p>使用者跨部署移轉，例如使用者從內部部署 商務用 Skype Online 移至 Lync Server 2013，或相反方向。</p></li>
</ul></td>
</tr>
</tbody>
</table>


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
<td>從備份資料庫匯入統一的連絡人存放區資料時，如果統一的連絡人存放區改變了匯出和匯入模式，可能會造成統一的連絡人存放區資料和使用者資料損毀。例如：
<ul>
<li><p>如果您在使用者的連絡人移轉至 Exchange 2013 前就匯出連絡人清單，接著在移轉後匯入相同的資料，統一的連絡人存放區資料和連絡人清單就會損毀。</p></li>
<li><p>如果您在將使用者移轉至 Exchange 2013 後匯出使用者資料、復原移轉，然後在移轉後，因故又匯入資料，統一的連絡人存放區資料和連絡人清單也會損毀。</p></li>
</ul></td>
</tr>
</tbody>
</table>


> [!IMPORTANT]  
> 在您將 Exchange 信箱從 Exchange 2013 移至 Exchange 2010 前， Exchange 系統管理員必須確定 Lync Server 系統管理員已先將 Lync Server 使用者連絡人從 Exchange 2013 復原至 Lync Server。若要將統一的連絡人存放區連絡人復原至 Lync Server，請參閱本節稍後的＜若要將統一的連絡人存放區連絡人從 Exchange 2013 復原至 Lync Server 2013＞程序。



下列程序說明如何復原使用者連絡人。如果您使用 **Move-CsUser** Cmdlet 在 Lync Server 2013 和 Lync Server 2010 之間移動使用者，則可略過這些步驟，因為 **Move-CsUser** Cmdlet 在將使用者從 Lync Server 2013 移至 Lync Server 2010 時，會自動復原統一的連絡人存放區。 **Move-CsUser** 不會停用統一的連絡人存放區原則，所以如果使用者移回 Lync Server 2013，便會再次移轉統一的連絡人存放區。

## 若要將使用者連絡人從 Lync Server 2013 復原到 Lync Server 2010

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  停用要復原之使用者的統一的連絡人存放區，如此在復原後就不會再次移轉。(您需確保使用者日後不會再次移轉時，才需執行此步驟)，若要停用個別使用者的統一的連絡人存放區，請在命令列中輸入：
    
        Set-CsUserServicesPolicy -Identity "<policy name>" -UcsAllowed $False
    
    例如：
    
        Set-CsUserServicesPolicy -Identity "UCS Enabled Users" -UcsAllowed $False

3.  將使用者從 Lync Server 2013 移至 Lync Server 2010 前，先在 Lync Server 上復原指定使用者的朋友清單。
    
    > [!IMPORTANT]  
    > 如果略過此步驟，將會遺失朋友清單。
    


4.  復原指定的使用者。在命令列中輸入：
    
        Invoke-CsUcsRollback -Identity "<user display name>"
    
    例如：
    
        Invoke-CsUcsRollback -Identity "Ken Myer"
    
    > [!IMPORTANT]  
    > 不建議使用 –Force 選項強制復原。如果使用此選項，使用者的連絡人將會遺失。
    


## 若要將統一的連絡人存放區連絡人從 Exchange 2013 復原至 Lync Server 2013

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  停用要復原之使用者的統一的連絡人存放區，如此在復原後就不會再次移轉。若要停用個別使用者的統一的連絡人存放區，請在命令列中輸入：
    
        Set-CsUserServicesPolicy -Identity "<policy name>" -UcsAllowed $False
    
    例如：
    
        Set-CsUserServicesPolicy -Identity "UCS Enabled Users" -UcsAllowed $False

3.  復原指定的使用者。在命令列中輸入：
    
        Invoke-CsUcsRollback -Identity "<user display name>"
    
    例如：
    
        Invoke-CsUcsRollback -Identity "Ken Myer"
    
    > [!IMPORTANT]  
    > 您必須先復原 Lync Server 使用者，之後再移動 Exchange 2013 信箱。在 Lync Server 復原完成前，Exchange 系統管理員將無法復原 Exchange。不建議使用 –Force 選項強制復原。如果使用此選項，使用者的連絡人將會遺失。
    


4.  將使用者復原至 Lync Server 後，Exchange 系統管理員就能將 Exchange 使用者從 Exchange 2013 復原至 Exchange 2010。

