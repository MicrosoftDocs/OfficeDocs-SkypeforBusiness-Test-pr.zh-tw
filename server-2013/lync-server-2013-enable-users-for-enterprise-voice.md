---
title: Lync Server 2013：為使用者啟用企業語音
TOCTitle: 為使用者啟用企業語音
ms:assetid: f252b23b-9641-4160-aa81-bf06dc2eced3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413011(v=OCS.15)
ms:contentKeyID: 49292776
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中為使用者啟用企業語音

 

_**上次修改主題的時間：** 2012-11-01_

安裝一部或多部中繼伺服器的檔案、設定撥出電話路由，以及選擇性地部署一項或多項進階 企業語音 功能之後，使用下列程序讓使用者使用 企業語音 撥打電話：

> [!NOTE]  
> 下列程序中，只有第一項程序可以使用 Lync Server 控制台 執行。其餘程序只能使用 Lync Server 管理命令介面。



  - 啟用 企業語音 的使用者帳戶。

  - (選用) 為使用者帳戶指派使用者專屬語音原則。

  - (選用) 為使用者帳戶指派使用者專屬撥號對應表。

## 啟用 企業語音 的使用者帳戶

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，按一下 \[使用者\] 。

4.  在 \[搜尋使用者\] 方塊中，輸入全部或部分的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或您想要啟用的使用者帳戶之線路統一資源識別元 (URI)，然後按一下 \[尋找\] 。

5.  在表格中，按一下要啟用的 企業語音 使用者帳戶。

6.  在 \[編輯\] 功能表上，按一下 \[顯示詳細資料\] 。

7.  在 \[編輯 Lync Server 使用者\] 頁面的 \[電話語音\] 底下，按一下 \[企業語音\] 。

8.  按一下 \[線路 URI\] ，然後輸入唯一的正規化電話號碼 (例如 tel:+14255550200)。

9.  按一下 \[認可\] 。

若要完成啟用使用者的 企業語音，請確定已為使用者指派全域 (預設指派) 或使用者專屬的語音原則和撥號對應表。

依預設，所有的使用者都被指派了全域語音原則和撥號對應表。如果使用者帳戶所在的網站上，其網路層級中有語音原則或撥號對應表，則這些網站原則將會自動套用至使用者。若要依每一使用者語音原則或撥號對應表套用至使用者，您必須執行 **Grant-CsVoicePolicy** 和 **Grant-CsDialPlan** Cmdlet。如需詳細資訊，請參閱 [Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)文件。

## 語音原則指派

全域和網站層級的語音原則會自動指派給啟用 企業語音 的所有使用者帳戶。您也可以建立套用至特定使用者或群組的語音原則。這些每一使用者原則必須明確指派給使用者或群組。如果您要讓所有啟用 企業語音 的使用者使用全域或網站語音原則，可以略過本節，繼續進行本主題稍後的 撥號對應表指派 一節。

## 若要指派使用者專屬的語音原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  若要將現有使用者語音原則指派給使用者，請在命令提示字元中執行下列命令：
    
        Grant-CsVoicePolicy -Identity <UserIdParameter> -PolicyName <String>
    
    例如：
    
        Grant-CsVoicePolicy -Identity "Bob Kelly" -PolicyName VoicePolicyJapan
    
    在此範例中，會指派名稱為 **VoicePolicyJapan** 的語音原則給顯示名稱為 Bob Kelly 的使用者。

如需關於指派使用者專屬語音原則或執行 **Grant-CsVoicePolicy** Cmdlet 的詳細資訊，請參閱 [Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)文件。

## 撥號對應表指派

若要針對 企業語音 使用者或電話撥入式會議使用者完成使用者帳戶設定，必須將撥號對應表指派給使用者。如果您未明確地指派現有的每一使用者撥號對應表，使用者帳戶會自動使用全域撥號對應表或網站層級撥號對應表 (如果有的話)。如果您要為所有啟用 企業語音 的使用者使用全域或網站撥號對應表，可以略過本節。

## 若要指派撥號對應表

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  若要指派使用者專屬撥號對應表，請在命令提示字元中執行下列命令：
    
        Grant-CsDialPlan -Identity <UserIdParameter> -PolicyName <String>
    
    例如：
    
        Grant-CsDialPlan -Identity "Bob Kelly" -PolicyName DialPlanJapan
    
    在此範例中，具有 Bob Kelly 顯示名稱的使用者，會被指派名稱為 **DialPlanJapan** 的使用者撥號對應表。

如需指派使用者撥號對應表或執行 **Grant-CsDialPlan** Cmdlet 的詳細資訊，請參閱 [Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)文件。

## 請參閱

#### 工作

[停用 Enterprise Voice 的使用者](lync-server-2013-disable-a-user-for-enterprise-voice.md)

