---
title: Lync Server 2013：(選用) 驗證電話撥入式會議設定
TOCTitle: (選用) 驗證電話撥入式會議設定
ms:assetid: a85efdda-97b0-4f3b-bd26-04416bee8ef5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412789(v=OCS.15)
ms:contentKeyID: 49291930
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (選用) 在 Lync Server 2013 中驗證電話撥入式會議設定

 

_**上次修改主題的時間：** 2010-11-02_

在最後確認電話撥入式會議設定時，您可以搜尋包含未由任何存取號碼使用之電話撥入式會議地區的撥號對應表，以及搜尋未指定電話撥入式會議地區的存取號碼。這是選用步驟。

## 若要尋找包含未由任何存取號碼使用之電話撥入式會議地區的撥號對應表

1.  以 RTCUniversalServerAdmins 群組成員或 **Cs-ServerAdministrator** 、 **CsAdministrator** 角色成員的身分登入電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令提示字元中執行下列命令：
    
        Get-CsDialinConferencingAccessNumber -EmptyRegion
    
    這個 Cmdlet 會傳回所有包含未由任何存取號碼使用之電話撥入式會議地區的撥號對應表。

## 若要尋找沒有指派之地區的存取號碼

1.  以 RTCUniversalServerAdmins 群組成員或 **Cs-ServerAdministrator** 、 **CsAdministrator** 角色成員的身分登入電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令提示字元中執行下列命令：
    
        Get-CsDialinConferencingAccessNumber -Region NULL
    
    這個 Cmdlet 會傳回所有沒有與地區關聯的電話撥入式會議存取號碼。

