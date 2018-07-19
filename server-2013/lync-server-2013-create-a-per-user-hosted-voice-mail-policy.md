---
title: 建立每個使用者的主控語音信箱原則
TOCTitle: 建立每個使用者的主控語音信箱原則
ms:assetid: 39018a7c-e0c3-46a2-be4e-05604ec67a50
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425867(v=OCS.15)
ms:contentKeyID: 49290615
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立每個使用者的主控語音信箱原則

 

_**上次修改主題的時間：** 2012-09-24_

*「個別使用者的」*原則只會影響個別使用者、群組和連絡人物件。若要部署個別使用者的原則，您必須明確指派原則給一個或多個使用者、群組或連絡人物件。如需詳細資訊，請參閱＜[指派每位使用者的主控語音信箱原則](lync-server-2013-assign-a-per-user-hosted-voice-mail-policy.md)＞。

如需如何使用個別使用者的裝載語音信箱原則的詳細資訊，請參閱 Lync Server 管理命令介面文件中關於下列 Cmdlet 的部分：

  - [New-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsHostedVoicemailPolicy)

  - [set-cshostedvoicemailpolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsHostedVoicemailPolicy)

  - [Get-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsHostedVoicemailPolicy)

## 若要建立個別使用者的裝載語音信箱原則

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 New-CsHostedVoicemailPolicy Cmdlet，建立原則。例如，執行：
    
        New-CsHostedVoicemailPolicy -Identity ExRedmond -Destination ExUM.fabrikam.com -Description "Hosted voice mail policy for Redmond users." -Organization "corp1.litwareinc.com, corp2.litwareinc.com"
    
    上述範例會建立個別使用者範圍的裝載語音信箱原則，並設定下列參數：
    
      - **Identity** 指定原則的唯一識別碼，包含範圍。若是個別使用者範圍的原則，此參數值必須以單一字串格式指定，例如 ExRedmond。
    
      - **Destination** 指定主控之 Exchange UM 服務的完整網域名稱 (FQDN)。此參數是選用的，但如果您企圖啟用使用者的主控語音信箱，且指派給使用者的原則沒有 Destination 值，則啟用作業會失敗。
    
      - **Description** 提供關於原則的選擇性說明資訊。
    
      - **Organization** 指定 Lync Server 2013 使用者隸屬之 Exchange 租用戶的逗號分隔清單。必須以主控之 Exchange UM 服務上的租用戶的 FQDN 來指定每一個租用戶。

## 請參閱

#### 工作

[指派每位使用者的主控語音信箱原則](lync-server-2013-assign-a-per-user-hosted-voice-mail-policy.md)

