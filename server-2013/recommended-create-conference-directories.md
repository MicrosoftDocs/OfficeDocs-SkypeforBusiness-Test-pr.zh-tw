---
title: (建議) 建立會議目錄
TOCTitle: (建議) 建立會議目錄
ms:assetid: 787f4c94-1c96-468a-a74d-e06b7bd4b8a3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn832056(v=OCS.15)
ms:contentKeyID: 63232647
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (建議) 建立會議目錄

 

_**上次修改主題的時間：** 2014-10-03_

會議目錄中維護了英數會議 ID (供參與者用來在 Lync 2013 中加入會議) 與純數值會議 ID (供電話撥入式會議參與者用來加入會議) 之間的對應。會議 ID 的格式如下：

    <housekeeping digit (1 digit)><conference directory (usually 1-2 digits)><conference number (variable number of digits><check digit (1 digit)>

建立多個會議目錄可確保在會議總數達到一定數量之前，會議 ID 都不會太長。對於每位使用者平均會議數量不特別多的組織而言，我們建議在集區中為每 999 個使用者建立一個會議目錄。只要按照這個方法，會議 ID 通常可以保持得很簡短。然而，一旦所有集區的會議目錄總數超過 9，為了支援額外的會議，會議 ID 的長度就會增加。

## 建立會議目錄

1.  在 Lync Server 管理命令介面 中輸入下列 cmdlet：
    
        New-CsConferenceDirectory -Identity <XdsGlobalRelativeIdentity> -HomePool <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]
    
    舉例來說，下列命令會建立代碼為 42、位在 atl-cs-001.litwareinc.com 集區的會議目錄：
    
        New-CsConferenceDirectory -Identity 42 -HomePool "atl-cs-001.litwareinc.com"

## 請參閱

#### 概念

[Lync Server 2013 中的電話撥入式會議需求](lync-server-2013-dial-in-conferencing-requirements.md)  

#### 其他資源

[New-CsConferenceDirectory](new-csconferencedirectory.md)

