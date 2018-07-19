---
title: 建立網站層級的主控語音信箱原則
TOCTitle: 建立網站層級的主控語音信箱原則
ms:assetid: 145892c8-a6ca-45fb-9e83-786f709dd775
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398216(v=OCS.15)
ms:contentKeyID: 49290173
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立網站層級的主控語音信箱原則

 

_**上次修改主題的時間：** 2012-09-24_

「網站」原則會影響定義該原則之網站上所屬的全部使用者。如果使用者已針對主控 Exchange UM 存取進行設定，且未獲指派個別使用者原則，便會套用網站原則。如果您尚未部署網站原則，則會套用全域原則。

如需設定網站原則的詳細資訊，請參閱 Lync Server 管理命令介面文件中關於下列 Cmdlet 的部分：

  - [New-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsHostedVoicemailPolicy)

  - [set-cshostedvoicemailpolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsHostedVoicemailPolicy)

  - [Get-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsHostedVoicemailPolicy)

## 建立網站主控的語音信箱原則

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 New-CsHostedVoicemailPolicy Cmdlet，建立原則。例如，執行：
    
        New-CsHostedVoicemailPolicy -Identity site:Redmond -Destination ExUM.fabrikam.com -Description "Hosted voice mail policy for the Redmond site." -Organization "corp1.litwareinc.com, corp2.litwareinc.com"
    
    此範例會建立網站範圍的主控語音信箱原則，並設定下列參數：
    
      - **Identity** 指定原則的唯一識別碼，包含範圍。若是網站範圍的原則，Identity 參數值必須以 `site:`*\<名稱\>* 格式指定，例如 `site:Redmond`。
    
      - **Destination** 指定主控之 Exchange UM 服務的完整網域名稱 (FQDN)。此參數是選用的，但如果您企圖啟用使用者的主控語音信箱，且指派給使用者的原則沒有 Destination 值，則啟用作業會失敗。
    
      - **Description** 提供關於原則的選用說明資訊。
    
      - **Organization** 指定 Lync Server 2013 使用者隸屬之 Exchange 租用戶的逗號分隔清單。必須以主控之 Exchange UM 服務上的租用戶之 FQDN 來指定每一個租用戶。

