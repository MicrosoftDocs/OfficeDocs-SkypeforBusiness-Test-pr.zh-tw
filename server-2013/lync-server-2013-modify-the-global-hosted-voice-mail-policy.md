---
title: 修改全域主控語音信箱原則
TOCTitle: 修改全域主控語音信箱原則
ms:assetid: f059b3ce-a7d8-4ea9-b10b-0052222ec2ce
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412994(v=OCS.15)
ms:contentKeyID: 49292750
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 修改全域主控語音信箱原則

 

_**上次修改主題的時間：** 2012-09-24_

*全域*裝載語音信箱原則會隨 Lync Server 2013 一起安裝。您可以修改該原則以符合您的需求，但無法將它重新命名或刪除。若要修改全域原則，請使用 Set-CsHostedVoicemailPolicy Cmdlet，將參數設為適合您的特定部署的值。

如需[Set-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsHostedVoicemailPolicy) Cmdlet 的詳細資訊，請參閱 Lync Server 管理命令介面文件。

## 修改全域裝載語音信箱原則

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 Set-CsHostedVoicemailPolicy Cmdlet，為您的環境設定全域原則參數。例如，執行：
    
        Set-CsHostedVoicemailPolicy -Destination ExUM.fabrikam.com -Organization "corp1.litwareinc.com"
    
    此命令不會指定原則的 Identity 參數，因此，Windows PowerShell 命令列介面會在全域裝載語音信箱原則上設定下列值：
    
      - **Destination** 指定主控之 Exchange UM 服務的完整網域名稱 (FQDN)。此參數是選用的，但如果您企圖啟用使用者的主控語音信箱，且指派給使用者的原則沒有 Destination 值，則啟用作業會失敗。
    
      - **Organization** 指定 Lync Server 使用者隸屬之 Exchange 承租人的逗號分隔清單。必須以主控之 Exchange UM 服務上的承租人的 FQDN 來指定每一個承租人。
    
    > [!NOTE]  
    > 在先前的範例 Cmdlet 中，“corp1.litwareinc.com” 值會取代可能已存在於 Organization 參數中的任何值。例如，如果原則已經包含組織的逗號分隔清單，則會取代完整清單。如果您要將某個組織新增至清單中，而非取代整個清單，請執行類似以下的命令。
    
    
        $a = Get-CsHostedVoicemailPolicy
        $a.Organization += ",corp3.litwareinc.com"
        Set-CsHostedVoicemailPolicy -Organization $a.Organization

