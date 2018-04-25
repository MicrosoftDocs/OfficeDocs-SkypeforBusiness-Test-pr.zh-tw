---
title: 在 Lync Server 2013 中設定語音信箱逸出功能
TOCTitle: 在 Lync Server 2013 中設定語音信箱逸出功能
ms:assetid: a1d19e6c-82ff-4768-8ae5-da981368ce40
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688157(v=OCS.15)
ms:contentKeyID: 49890235
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定語音信箱逸出功能

 

_**上次修改主題的時間：** 2013-02-22_

當使用者設定行動電話同時響鈴時，如果電話已關機、電池不足或收不到訊號，通常會將來電者路由傳送至使用者的個人語音信箱。使用 Microsoft Lync Server 2013，使用者可以選擇將業務相關電話路由傳送至其公司語音信箱系統。此外，還可以設定計時器，如果電話在定義的時間範圍內由電信業者的語音信箱接聽，則 Lync Server 2013 會與電信業者的語音信箱系統 (和使用者的個人語音信箱) 中斷連線，而公司系統中使用者的其餘端點會繼續發出鈴聲。如此一來，來電者便會自動路由傳送至使用者的公司語音信箱。

此設定是使用 Lync Server 管理命令介面 Cmdlet Set-CsVoicePolicy 在語音原則層級執行，包含下列參數。

## 設定語音信箱逸出

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  將下列參數指定為 \[Set-CsVoicePolicy\]：
    
      - **EnableVoicemailEscapeTimer** - 啟用或停用逸出計時器。
    
      - **PSTNVoicemailEscapeTimer** - 指定逾時值 (毫秒)。設定值為 1500 毫秒，此值的範圍是 0 毫秒至 8000 毫秒。

## 範例

    Set-CsVoicePolicy UserVoicePolicy -EnableVoiceMailEscapeTimer $true - PSTNVoicemailEscapeTimer 2000
    
    Set-CsVoicePolicy -Identity site:SitePolicy -EnableVoiceMailEscapeTimer $true -PSTNVoicemailEscapeTimer 1500

## 請參閱

#### 其他資源

[在 Lync Server 2013 中設定用於授權撥號功能和權限的語音原則和 PSTN 使用方式記錄](lync-server-2013-configuring-voice-policies-and-pstn-usage-records-to-authorize-calling-features-and-privileges.md)

