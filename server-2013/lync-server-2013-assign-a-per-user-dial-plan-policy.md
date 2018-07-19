---
title: 指派每位使用者的撥號對應表原則
TOCTitle: 指派每位使用者的撥號對應表原則
ms:assetid: 9fea861f-7770-4cae-9b1f-2a960595bfc9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688156(v=OCS.15)
ms:contentKeyID: 49890232
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指派每位使用者的撥號對應表原則

 

_**上次修改主題的時間：** 2013-02-22_

若要針對 Enterprise Voice 使用者或電話撥入式會議使用者完成使用者帳戶設定，必須將撥號對應表指派給使用者。如果您未明確地指派現有的每一使用者撥號對應表，使用者帳戶會自動使用全域撥號對應表或網站層級撥號對應表 (如果有的話)。如果您要為所有啟用 Enterprise Voice 的使用者使用全域或網站撥號對應表，可以略過本節。

## 使用 Lync Server 2013 控制台指派撥號對應表

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[使用者\]。

4.  在 \[搜尋使用者\] 方塊中，輸入全部或部分的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或您想要啟用的使用者帳戶之線路統一資源識別元 (URI)，然後按一下 \[尋找\]。

5.  在表格中，按一下要指派撥號對應表的使用者帳戶。

6.  在 \[編輯\] 功能表上，按一下 \[顯示詳細資料\]。

7.  在 \[編輯 Lync Server 使用者\] 頁面的 \[電話語音\] 底下，按一下 \[企業語音\]。

8.  按一下 \[撥號對應表原則\]，然後選擇所需的撥號對應表。

9.  按一下 \[認可\]。

如需設定撥號對應表的詳細資訊，請參閱「[在 Lync Server 2013 中設定撥號對應表](lync-server-2013-configuring-dial-plans.md)」主題。

## 使用 Lync Server 2013 管理命令介面指派撥號對應表

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  若要指派使用者專屬撥號對應表，請在命令提示字元中執行下列命令：
    
        Grant-CsDialPlan -Identity <UserIdParameter> -PolicyName <String>
    
    例如：
    
        Grant-CsDialPlan -Identity "Bob Kelly" -PolicyName DialPlanJapan
    
    在此範例中，具有 Bob Kelly 顯示名稱的使用者，會被指派名稱為 **DialPlanJapan** 的使用者撥號對應表。

如需指派使用者撥號對應表或執行 **Grant-CsDialPlan** Cmdlet 的詳細資訊，請參閱「[Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)」文件。

## 使用 Windows PowerShell Cmdlet 指派個別使用者撥號對應表

使用 Windows PowerShell 和 **Grant-CsdialPlan** Cmdlet 也可以指派個別使用者撥號對應表。您可以從 Lync Server 2013 管理命令介面 或從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 將個別使用者撥號對應表指派給單一使用者

  - 下列命令會將個別使用者撥號對應表 RedmondDialPlan 指派給使用者 Ken Myer。
    
        Grant-CsDialPlan -Identity "Ken Myer" -PolicyName "RedmondDialPlan"

## 將個別使用者撥號對應表指派給多個使用者

  - 此命令會將個別使用者撥號對應表 RedmondDialPlan 指派給在 Redmond 市工作的所有使用者。如需此命令中使用的 LdapFilter 參數的詳細資訊，請參閱 [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser) Cmdlet 的文件。
    
        Get-CsUser -LdapFilter "l=Redmond" | Grant-CsDialPlan -PolicyName "RedmondDialPlan"

## 指派取消個別使用者撥號對應表

  - 下列命令會取消指派先前指派給 Ken Myer 的所有個別使用者撥號對應表。取消指派個別使用者撥號對應表後，系統就會自動使用全域撥號對應表、其本機網站撥號對應表 (如果存在的話) 或已指派至其登錄器或 PSTN 閘道的服務範圍撥號對應表來管理 Ken Myer。服務範圍撥號對應表的優先順序高於所有網站撥號對應表，而網站撥號對應表的優先順序則高於全域撥號對應表。
    
        Grant-CsDialPlan -Identity "Ken Myer" -PolicyName $Null

如需詳細資訊，請參閱 [Grant-CsDialPlan](grant-csdialplan.md) Cmdlet 的說明主題。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中設定撥號對應表](lync-server-2013-configuring-dial-plans.md)  
[針對 Lync Server 2013 啟用的使用者帳戶](lync-server-2013-user-accounts-enabled-for-lync-server.md)

