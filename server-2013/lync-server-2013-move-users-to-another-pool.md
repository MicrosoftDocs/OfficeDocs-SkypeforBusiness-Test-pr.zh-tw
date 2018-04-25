---
title: 在 Lync Server 2013 中將使用者移動到其他集區
TOCTitle: 在 Lync Server 2013 中將使用者移動到其他集區
ms:assetid: e7b4968c-0e9d-4d56-b5f1-9edf0f7206f8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182600(v=OCS.15)
ms:contentKeyID: 49292651
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將使用者移動到其他集區

 

_**上次修改主題的時間：** 2013-03-11_

您可以使用 Lync Server 控制台將使用者指派至特定伺服器或集區。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>將所有現有使用者從執行 Microsoft Office Communications Server 2007 R2 或早於 Lync Server 2013 的來源集區，移至複雜 Active Directory 環境中，可能會導致 Active Directory 複寫速度變慢。為避免這種情況，您可以使用搜尋篩選，將使用者從執行 Microsoft Office Communications Server 2007 R2 或更早版本的集區各別移動，或是使用 Lync Server 管理命令介面透過 Cmdlet 移動使用者。而且，篩選器功能可用於 Lync Server 2013 使用者。</td>
</tr>
</tbody>
</table>


## 若要將選取的使用者移至不同的伺服器或集區

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[使用者\]**。

4.  在 **\[搜尋使用者\]** 方塊中，輸入您要的使用者帳戶的完整或開頭部分的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或線路統一資源識別項 (URI)，然後按一下 **\[尋找\]**。

5.  在表格中，選取清單中的特定使用者。

6.  在 **\[執行\]** 功能表上，按一下 **\[將選取的使用者移至集區\]**。

7.  在 **\[移動使用者\]** 的 **\[目的地登錄器集區\]** 中，選取要將使用者移至其中的集區。

8.  (選用) 如果目的地伺服器或集區無法使用，請選取 **\[強制\]** 核取方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若選取 [強制]，將會移動使用者帳戶，但刪除所有相關的使用者資料 (例如該使用者所排定的會議)。若未選取此選項，將會移動帳戶及其相關資料。</td>
    </tr>
    </tbody>
    </table>


## 若要從某部伺服器或集區將所有使用者移至不同的伺服器或集區

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[使用者\]**。

4.  在 **\[執行\]** 功能表上，按一下 **\[將所有使用者移至集區\]**。

5.  在 **\[移動使用者\]** 的 **\[來源登錄器集區\]** 中，選取包含您要移動之使用者帳戶的集區。

6.  在 **\[在目的地登錄器集區\]** 中，選取要將使用者移至其中的集區。

7.  (選用) 如果目的地伺服器或集區無法使用，請選取 **\[強制\]** 核取方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若選取 [強制]，將會移動使用者帳戶，但刪除所有相關的使用者資料 (例如該使用者所排定的會議)。若未選取此選項，將會移動帳戶及其相關資料。</td>
    </tr>
    </tbody>
    </table>


## 利用篩選在集區之間移動使用者

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[尋找\]**\[使用者\]**。

4.  在 \[使用者搜尋\] 中，按一下 \[搜尋\]，然後按一下 \[新增篩選\]。

5.  在 \[搜尋準則\] 中，依序選取 \[登錄器集區\]、\[等於\] 及 \[目前集區 FQDN\]，然後按一下 \[尋找\]。

6.  在 \[執行\] 功能表上，按一下 \[將所有使用者移至集區\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>為一組現有使用者套用篩選時，選項 [將所有使用者移至集區] 會出現在經篩選的一組使用者子集之內容中，而非「所有」 可能的使用者中。</td>
    </tr>
    </tbody>
    </table>


7.  在 \[移動使用者\] 的 \[來源登錄器集區\] 中，選取包含您要移動之使用者帳戶的集區。

8.  在 \[目的地登錄器集區\] 中，選取想要容納移動使用者的集區。

9.  (選用) 如果目的地伺服器或集區無法使用，請選取 \[強制\] 核取方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若選取 [強制]，將會移動使用者帳戶，但刪除所有相關的使用者資料 (例如該使用者所排定的會議及連絡人)。若未選取此選項，將會移動帳戶及其相關資料。</td>
    </tr>
    </tbody>
    </table>


## 使用 Lync Management 命令介面將使用者從某一集區移至另一集區

1.  隨您執行 Windows PowerShell 命令之方式的不同 (亦即從本機或從遠端)，您必須使用正確之 Lync Server 2013 系統管理角色的成員身分登入，如下所示：
    
    1.  若是在本機機器上執行命令 (例如您直接登入前端伺服器)：以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。
    
    2.  若是透過其他電腦從遠端執行命令 (例如登入您的電腦，然後從遠端的 Standard Edition 前端伺服器上執行命令)：使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  使用 Move-CsUser Cmdlet 移動單一使用者，如下所示：
    
        Move-CsUser -Identity "Pilar Ackerman" -Target "pool01.contoso.net"
    
    要移動的使用者為 Pilar Ackerman，而且使用者會從其目前指派的主集區移至集區 pool01.contoso.net

4.  若要移動大量的使用者，可並用篩選與 **Get-CsUser** Cmdlet，然後再將得到的使用者集傳遞給 **Move-CsUser**：
    
        Get-CsUser -Filter {RegistrarPool -eq "CurrentPoolFqdn"} | Move-CsUser -Target "TargetPoolFQDN"
    
    並用 **Get-CsUser** 命令與 **Move-CsUser** 命令可能會得到下列結果：
    
        Get-CsUser -Filter {RegistrarPool -eq "pool02.contoso.net"} | Move-CsUser -Target "pool01.contoso.net"

## 請參閱

#### 其他資源

[修改使用者帳戶屬性](lync-server-2013-modifying-user-account-properties.md)

