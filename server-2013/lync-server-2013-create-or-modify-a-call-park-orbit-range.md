---
title: Lync Server 2013：建立或修改通話駐留軌道範圍
TOCTitle: 建立或修改通話駐留軌道範圍
ms:assetid: 549ec118-eee5-4333-9416-80929ec057e0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398361(v=OCS.15)
ms:contentKeyID: 49290940
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立或修改通話駐留軌道範圍

 

_**上次修改主題的時間：** 2012-11-01_

使用下列其中一個程序來建立或修改通話駐留軌道範圍。

## 使用 Lync Server 控制台建立或修改駐留通話號碼範圍

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[語音功能\]** 、 **\[通話駐留\]** 。

4.  在 **\[通話駐留\]** 頁面上，執行下列其中一項動作：
    
      - 若要建立新的軌道範圍，可按一下 **\[新增\]** 。在 **\[名稱\]** 中，輸入此號碼範圍的識別名稱。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>當您將軌道範圍認可至資料庫之後，就無法變更此名稱。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要修改現有的軌道範圍，可在搜尋欄位中輸入軌道範圍的所有或部分名稱。在軌道的結果清單中，按一下您想要的軌道，接著依序按一下 **\[編輯\]** 及 **\[顯示詳細資料\]** 。

5.  在第一個 **\[號碼範圍\]** 欄位中，輸入此項通話駐留軌道分機號碼範圍的開頭號碼，並在第二個 **\[號碼範圍\]** 欄位中，輸入該範圍的結束號碼。
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><ul>
    <li><p>該範圍的起始號碼必須小於或等於範圍的結束號碼。</p></li>
    <li><p>該範圍的起始號碼值的長度必須等於範圍的結束號碼值長度。</p></li>
    <li><p>軌道範圍必須是唯一的。此範圍不得與其他任何範圍重疊。</p></li>
    <li><p>如果軌道範圍開頭為 * 或 #，則範圍必須大於 100。</p></li>
    <li><p>有效值：必須符合規則運算式字串 ([\*|#]?[1-9]\d{0,7})|([1-9]\d{0,8})。這表示值必須是開頭為字元 * 或 # 或數字 1 至 9 的字串 (第一個字元不得為零)。如果第一個字元是 * 或 #，則後續字元必須是數字 1 至 9 (不得為零)。後續字元可以是 0 至 9 的任何數字，最多加上七個字元 (例如，&quot;#6000&quot;、&quot;*92000&quot;、&quot;*95551212&quot; 及 &quot;915551212&quot;)。如果第一個字元不是 * 或 #，則第一個字元必須是數字 1 至 9 (不得為零)，後面最多接著八個字元，每一個字元都是數字 0 至 9 (例如，&quot;915551212&quot;、&quot;41212&quot;、&quot;300&quot;)。</p></li>
    <li><p>每個集區的軌道總數不得超過 50,000 個。每個軌道範圍通常會涵蓋 100 個以下的軌道，但只要總數不超過 10,000 個軌道，可以大一些。例如，與其指定開頭號碼 7000000 與結束號碼 8000000，請考慮指定開始號碼 7000000 與結束號碼 7000100。</p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>


6.  在 **\[目的地伺服器的 FQDN\]** 中，按一下裝載 通話駐留應用程式的應用程式服務之完整網域名稱 (FQDN) 或服務識別碼。駐留給軌道範圍中由開始號碼與結束號碼所指定之範圍內的號碼的所有通話，將會路由傳送至此伺服器或集區。

7.  按一下 \[認可\] 。

## 使用 Windows PowerShell建立或修改駐留通話號碼範圍

1.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  使用 **New-CsCallParkOrbit** 來建立新的軌道號碼範圍。使用 **Set-CsCallParkOrbit** 來修改現有的軌道號碼範圍。
    
    在命令列中執行：
    
        New-CsCallParkOrbit -Identity <name of orbit range> -NumberRangeStart <first number in orbit range> -NumberRangeEnd <last number in orbit range> -CallParkService <FQDN or service ID of the Application service that hosts the Call Park application>
    
    例如：
    
        New-CsCallParkOrbit -Identity "Redmond orbit 1" -NumberRangeStart 100 -NumberRangeEnd 199 -CallParkService redmond-applicationserver-1
    
    下列範例示範如何修改現有軌道範圍中的號碼，
    
        Set-CsCallParkOrbit -Identity "Redmond orbit 1" -NumberRangeStart 500 -NumberRangeEnd 699

## 請參閱

#### 工作

[刪除通話保留範圍](lync-server-2013-delete-a-call-park-orbit-range.md)  

#### 其他資源

[New-CsCallParkOrbit](new-cscallparkorbit.md)  
[Set-CsCallParkOrbit](set-cscallparkorbit.md)

