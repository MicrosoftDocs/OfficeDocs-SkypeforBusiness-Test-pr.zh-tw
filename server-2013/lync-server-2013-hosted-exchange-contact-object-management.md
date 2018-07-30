---
title: Lync Server 2013：主控 Exchange 聯絡人物件管理
TOCTitle: 主控 Exchange 聯絡人物件管理
ms:assetid: eead9d76-bc4f-4c1c-9779-683cb7a88410
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412978(v=OCS.15)
ms:contentKeyID: 49292740
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的主控 Exchange 聯絡人物件管理

 

_**上次修改主題的時間：** 2012-09-25_

您需要為跨部署部署中的每個自動語音應答號碼和訂戶存取號碼，設定連絡人物件。

與裝載的 Exchange UM 整合時，無法使用 ocsumutil.exe 來管理連絡人物件，因為它是依據 Active Directory Exchange UM 設定。在跨部署部署中， Lync Server 2013 和裝載的 Exchange UM 會安裝在不同的樹系中，且它們之間沒有信任關係。基於安全性理由， Lync Server 2013 系統管理員無法直接存取 Exchange UM Active Directory 設定。因此， Lync Server 2013 提供一個不同的模型來管理 *「共用 SIP 位址空間」* (Shared SIP Address Space) 中的連絡人物件，該空間可供 Lync Server 2013 和裝載的 Exchange UM 服務存取。

## 裝載的連絡人物件工作流程

使用裝載的 Exchange 承租人系統管理員來管理連絡人物件的一般步驟如下：

1.  Exchange 系統管理員要求 Exchange UM 訂戶存取和自動語音應答連絡人物件的電話號碼。

2.  Lync Server 2013 系統管理員為每個電話號碼建立連絡人物件，並將裝載的語音信箱原則指派給每個連絡人物件。

3.  Lync Server 2013 系統管理員將電話號碼提供給 Exchange 系統管理員。

4.  Exchange 系統管理員將電話號碼指派給適當的 Exchange UM 撥號對應表，以用於自動語音應答和訂戶存取。

> [!NOTE]  
> 不像內部部署，您不需要在連絡人物件上設定任何 Lync Server 2013 撥號對應表設定。



## 設定裝載的連絡人物件

> [!NOTE]  
> 在您可以為裝載的 Exchange UM 啟用 Lync Server 2013 連絡人物件之前，必須先部署適用於這些物件的裝載語音信箱原則。原則的範圍可以是全域、網站或個別使用者，只要適用於您要啟用的連絡人物件即可。如需詳細資訊，請參閱＜ <a href="lync-server-2013-hosted-voice-mail-policies.md">Lync Server 2013 中的主控語音信箱原則</a>＞。



若要在跨部署部署中設定裝載的自動語音應答和訂戶存取連絡人物件，必須使用下列 Cmdlet：

  - **New-CsExUmContact** 會為裝載的 UM 建立新的連絡人物件。

  - **Set-CsExUmContact** 會為裝載的 Exchange UM 修改現有的連絡人物件。

下列範例會建立自動語音應答連絡人物件：

    New-CsExUmContact -SipAddress sip:exumaa1@fabrikam.com -RegistrarPool RedmondPool.litwareinc.com -OU "OU=ExUmContacts,DC=litwareinc,DC=com" -DisplayNumber 2065559876 -AutoAttendant $True

此範例會使用 SIP 位址 sip:exumaa1@fabrikam.com 建立新的 Exchange UM 連絡人物件。執行 Lync Server 2013 登錄器服務之集區的名稱為 RedmondPool.litwareinc.com。將儲存此資訊的 Active Directory 組織單位是 OU=ExUmContacts,DC=litwareinc,DC=com。連絡人物件的電話號碼為 2065554567。選用的 -AutoAttendant $True 參數會指定此物件為自動語音應答連絡人物件。將 -AutoAttendant 參數設為 False (預設值) 會指定訂戶存取連絡人物件。

如需 New-CsExUmContact 和 Set-CsExUmContact Cmdlet 的詳細資訊，請參閱 Lync Server 管理命令介面文件。

