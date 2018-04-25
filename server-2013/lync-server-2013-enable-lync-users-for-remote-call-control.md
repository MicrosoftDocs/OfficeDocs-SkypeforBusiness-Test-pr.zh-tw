---
title: Lync Server 2013：允許 Lync 使用者進行遠端呼叫控制
TOCTitle: 允許 Lync 使用者進行遠端呼叫控制
ms:assetid: f39bc10d-034c-4875-a0b8-554e1109e7e6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615048(v=OCS.15)
ms:contentKeyID: 49292794
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中允許 Lync 使用者進行遠端呼叫控制

 

_**上次修改主題的時間：** 2012-09-21_

您可以設定 Lync 使用者，以使用伺服器架構的頻內佈建原則進行遠端呼叫控制。您可以使用 Lync Server 控制台 或 Lync Server 管理命令介面 命令列介面管理頻內佈建設定。這些工具取代了用來管理舊版中群組原則設定的 Windows Management Instrumentation (WMI) 嵌入式管理單元。

如果您希望允許使用者在 Lync 中設定自己的遠端呼叫控制，可以在伺服器上為使用者設定遠端呼叫控制選項，但是不指定 \[線路伺服器 URI\] 和 \[線路 URI\] 的值。確定您將適當的 \[線路伺服器 URI\] 和 \[線路 URI\] 值傳達給使用者，並且為使用者提供進行這些設定的指示。如需在 Lync Server 中手動設定遠端呼叫控制的程序，請參閱 Microsoft Office 網站上 Lync 用戶端文件中的設定電話選項和電話號碼，網址為 [http://go.microsoft.com/fwlink/?linkid=210132\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=210132%26clcid=0x404)。

如果您有現有的 Communications Server 2007 R2 或 Communications Server 2007 部署， Communicator 2007 R2 和 Communicator 2007 用戶端將在並存移轉時繼續使用原則設定。不過，如果您想要將原則設定沿用至 Lync 用戶端，則需要設定對等的 Lync Server 頻內佈建設定。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要啟用使用者的遠端呼叫控制功能，必須同時提供使用者 [線路 URI] 和 [線路伺服器 URI]。如 <a href="lync-server-2013-deployment-tasks-for-remote-call-control.md">Lync Server 2013 中遠端呼叫控制的部署工作</a>中所述，您必須確認使用這些設定之閘道所需的語法。<br />
請確定 [線路伺服器 URI] 中的網域與您設定閘道的靜態路由時，在 MatchUri 參數中指定的目的地網域相同。<br />
[線路 URI] 會指定指派給使用者的 E.164 格式電話號碼，並且以 &quot;TEL:&quot; 做為首碼。(例如，tel:+14255550150)。如果您想要設定分機號碼，則格式為 tel:+14255550150;ext=111。如果您之前已設定使用者的 [線路 URI] 而且值並未變更，則不需要在啟用使用者的遠端呼叫控制功能時指定 [線路 URI]。</td>
</tr>
</tbody>
</table>


## 使用管理命令介面啟用已啟用 Lync 之使用者的遠端呼叫控制

1.  以 RTCUniversalServerAdmins 群組成員的身分，或是已對其指派 **Set-CsUser** Cmdlet 的角色存取控制角色，登入已安裝 Lync Server 管理命令介面 的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  若要使用 **Set-CsUser** Cmdlet 設定已啟用 Lync 之現有使用者的遠端呼叫控制功能，請執行下列操作：
    
        Set-CsUser -Identity <User ID> -EnterpriseVoiceEnabled $false -LineServerUri <SIP URI of the SIP/CSTA gateway> -LineUri <TEL URI of the user> -RemoteCallControlTelephonyEnabled $true
    
    例如：
    
        Set-CsUser -Identity "Katie Jordan" -EnterpriseVoiceEnabled $false -LineServerUri sip:rccgateway@contoso.net -LineUri tel:+14255550150 -RemoteCallControlTelephonyEnabled $true

## 使用 Lync Server 控制台設定使用者的遠端呼叫控制功能

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，按一下 \[使用者\] 。

4.  在 \[搜尋使用者\] 方塊中，輸入您要的使用者帳戶的完整 (或開頭部分) 顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或線路統一資源識別項 (URI)，然後按一下 \[尋找\] 。

5.  在表格中，按一下您要修改的使用者帳戶。

6.  在 \[編輯\] 功能表中，按一下 \[修改\] 。

7.  在 \[電話語音\] 中，執行下列其中一項操作：
    
      - 若要啟用遠端呼叫控制，讓使用者從 Lync 2013 控制其專用交換機 (PBX) 電話以撥打電腦對電腦音訊電話或電腦對電話的電話，則按一下 \[遠端呼叫控制\] 。在 \[線路 URI\] 中，指定使用者的電話號碼。在 \[線路伺服器 URI\] 中，指定 SIP/CSTA 閘道的 SIP URI。
    
      - 若要啟用遠端呼叫控制，但是停用電腦對電腦音訊電話，並且只讓使用者從 Lync 2013 控制其 PBX 電話以撥打電腦對電話的電話，則按一下 \[僅限遠端呼叫控制\] 。在 \[線路 URI\] 中，指定使用者的電話號碼。在 \[線路伺服器 URI\] 中，指定 SIP/CSTA 閘道的 SIP URI。

8.  完成時，按一下 \[認可\] 。

