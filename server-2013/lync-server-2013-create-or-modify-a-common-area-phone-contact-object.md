---
title: 建立或修改公共區域電話連絡人物件
TOCTitle: 建立或修改公共區域電話連絡人物件
ms:assetid: eec33ad1-e4f2-49b2-91d6-d5a9d2e1714b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994083(v=OCS.15)
ms:contentKeyID: 52056253
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改公共區域電話連絡人物件

 

_**上次修改主題的時間：** 2013-02-20_

若要為您的所有公共區域電話建立 Active Directory 網域服務 連絡人物件，請使用 **New-CsCommonAreaPhone** Cmdlet。此 Cmdlet 可用於建立搭配公用區電話使用的新連絡人物件，或是讓現有的連絡人物件與新的公用區電話產生關聯。若要修改與公共區域電話相關聯的連絡人物件屬性，請使用 **Set-CsCommonAreaPhone** Cmdlet。**Set-CsCommonAreaPhone** 的選用參數可讓您變更項目，例如連絡人的 Active Directory 顯示名稱或與電話相關聯的線路統一資源識別元 (URI)，以及可啟用和停用與 Lync Server 搭配使用的帳戶。如需所有可用修改的詳細資訊，請參閱＜[Set-CsCommonAreaPhone](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCommonAreaPhone)＞的＜參數＞一節。如需 **New-CsCommonAreaPhone** 參數的詳細資訊，請參閱＜[New-CsCommonAreaPhone](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsCommonAreaPhone)＞。

您可以從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行這兩個 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。


## 建立公共區域電話連絡人物件

  - 若要建立新的公共區域電話連絡人物件，請使用 **New-CsCommonAreaPhone** Cmdlet。在建立連絡人物件時，您至少必須提供下列資訊：
    
      - **LineUri**：指派為公共區域電話的電話號碼。請注意，指定電話號碼時，必須使用 E.164 格式。
    
      - **RegistrarPool**：將代管連絡人物件之登錄集區的完整網域名稱 (FQDN)。
    
      - **OU**：將建立連絡人物件之 Active Directory 容器的辨別名稱。
    
    同時建議您提供 Active Directory 網域服務 顯示名稱，否則您將必須使用 GUID 指定電話身分識別碼。例如：
    
        New-CsCommonAreaPhone -LineUri "tel:+12065551219" -RegistrarPool "atl-cs-001.litwareinc.com" -OU "OU=Phones,dc=litwareinc,dc=com" -DisplayName "Lobby"

## 修改公共區域電話連絡人物件

  - 若要修改現有公共區域電話和連絡人物件屬性，請使用 **Set-CsCommonAreaPhone** Cmdlet。例如，此命令可設定具有 DisplayName Lobby 之公共區域電話的 SIP 位址：
    
        Set-CsCommonAreaPhone -Identity "Lobby" -SipAddress "sip:lobby@litwareinc.com"

如需詳細資訊，請參閱＜[New-CsCommonAreaPhone](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsCommonAreaPhone)＞ Cmdlet 和＜[Set-CsCommonAreaPhone](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCommonAreaPhone)＞ Cmdlet 的說明主題。

