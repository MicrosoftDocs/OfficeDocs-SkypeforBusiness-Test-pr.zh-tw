---
title: 建立或修改會議的組態設定集合
TOCTitle: 建立或修改會議的組態設定集合
ms:assetid: ce6773c1-a0d5-4405-8e32-33a6f3a46a1a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721889(v=OCS.15)
ms:contentKeyID: 49890318
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改會議的組態設定集合

 

_**上次修改主題的時間：** 2013-02-23_

您可以使用 \[會議設定\] 頁面上的設定來定義各種不同會議加入經驗的特性。根據預設，全域設定會定義加入經驗。您也可以建立網站層級和集區層級的會議加入設定。如果您建立集區層級的設定，這些設定會套用至該集區裝載的所有會議。如果您未建立集區層級的設定，則會套用網站層級的設定 (如果有的話)。如果您未定義網站層級的定義，則全域設定會套用至所有會議。

## 建立新的會議加入設定

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[會議\]，然後按一下 \[會議設定\]。

4.  在 \[會議設定\] 頁面上按一下 \[新增\]，然後執行下列其中一項操作：
    
      - 若要建立網站層級原則，請按一下 \[站台組態\]。在 \[選取站台\] 搜尋欄位中，輸入您要定義會議加入設定之網站的完整或部分名稱。在產生的網站清單中按一下所需的網站，然後按一下 \[確定\]。
    
      - 若要建立集區層級原則，請按一下 \[集區組態\]。在 \[選取服務\] 搜尋欄位中，輸入您要定義會議加入設定之集區服務的完整或部分名稱。在產生的服務清單中，按一下您需要的集區，然後按一下 \[確定\]。

5.  若要透過大廳路由傳送從公用交換電話網路 (PSTN) 撥入的參與者，請清除 \[PSTN 來電者略過大廳\] 核取方塊。根據預設，從 PSTN 撥入的參與者會直接進入會議。

6.  若要設定誰能當會議簡報者，請在 \[指定為簡報者\] 中執行下列其中一項：
    
      - 若不要允許召集人以外的任何人當簡報者，請按一下 \[無\]。
    
      - 若只要允許組織成員的參與者當簡報者，請按一下 \[公司\]。此設定為預設值。
    
      - 若要允許任何參與者當簡報者，請按一下 \[任何人\]。

7.  若要讓召集人在排程會議時選取會議類型，請清除 \[預設指派的會議類型\] 核取方塊。根據預設，會議類型會自動指派。

8.  若要避免自動核准匿名 (未經授權) 的使用者，請清除 \[預設允許匿名使用者\] 核取方塊。根據預設，匿名使用者會自動允許進入會議。

9.  若要自訂送出給參與者的會議邀請，請執行下列動作。請注意，URL 和自訂頁尾文字的長度上限是 1KB。(\[說明 URL\] 除外) 如果您不指定自訂值，它們將不會包含在會議中。如果您不包含自訂說明 URL，邀請中將顯示 Lync 的預設說明 URL。
    
      - 若要自訂出現在會議邀請上的標誌，請在 \[標誌 URL\] 中輸入標誌的位置。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>標誌必須是 GIF 或 JPG 影像，大小為 188 x 30 像素。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要自訂出現在會議邀請上的說明文字，請在 \[說明 URL\] 中輸入說明文字的位置。
    
      - 若要自訂出現在會議邀請上的法律聲明文字，請在 \[標誌 URL\] 中輸入標誌的位置。
    
      - 若要自訂出現在會議邀請上的頁尾文字，請在 \[自訂頁尾文字\] 中輸入文字。

10. 按一下 \[認可\]。

## 修改現有的會議設定集合

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[會議\]，然後按一下 \[會議設定\]。

4.  在會議設定清單中，按一下您要變更的設定，並按一下 \[編輯\]，然後按一下 \[顯示詳細資料\]。

5.  在 \[編輯會議設定\] 中，修改任何組態設定，但不包括組態名稱，因為這無法修改。

6.  按一下 \[認可\]。

## 使用 Windows PowerShell Cmdlet 建立新的會議組態設定

您可以使用 Windows PowerShell 和 New-CsMeetingConfiguration Cmdlet 建立會議組態設定 (僅在網站範圍)。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 建立使用預設值的會議組態設定

  - 此命令會為 Redmond 網站建立一組新的會議組態設定：
    
        New-CsMeetingConfiguration -Identity "site:Redmond"
    
    由於上述的命令除了指定必要的 Identity 參數以外，並未指定任何其他參數，因此新會議組態設定的所有屬性都將使用預設值。

## 在建立會議組態設定時變更一個屬性值

  - 若要建立使用不同屬性值的設定，只要加上適當的參數和參數值即可。例如，若要建立預設允許會議的任何參與者擔任簡報者的會議組態設定集合，請使用如下的命令：
    
        New-CsMeetingConfiguration -Identity "site:Redmond" -DesignateAsPresenter "Everyone"

## 在建立會議組態設定時變更多個屬性值

  - 您可以加上多個參數來修改多個屬性值。例如，此命令會允許會議的任何參與者擔任簡報者，並同時強迫 PSTN 使用者必須先在大廳等候，直到正式獲准進入會議：
    
        New-CsMeetingConfiguration -Identity "site:Redmond" -DesignateAsPresenter "Everyone" -PSTNUCallersBypassLobby $True

如需詳細資訊，請參閱 [New-CsMeetingConfiguration](new-csmeetingconfiguration.md) Cmdlet 的說明主題。

