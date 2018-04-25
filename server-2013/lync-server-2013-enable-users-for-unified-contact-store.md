---
title: Lync Server 2013：為使用者啟用整合連絡人存放區
TOCTitle: 為使用者啟用整合連絡人存放區
ms:assetid: 7b46a01f-beb5-4a33-adb0-35f0502b168d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205024(v=OCS.15)
ms:contentKeyID: 49291427
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中為使用者啟用整合連絡人存放區

 

_**上次修改主題的時間：** 2012-10-07_

部署 Lync Server 2013 並發布該拓撲時，預設會對所有使用者啟用整合連絡人存放區。您必須要採取其他任何動作，即可在部署 Lync Server 2013 後起用整合連絡人存放區。不過，您可以使用 **Set-CsUserServicesPolicy** Cmdlet 自訂哪些連絡人有整合連絡人存放區可用。您可以全域、依網站、依承租人或依個人或個人群組啟用此功能。

## 啟用整合連絡人存放區的使用者

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行下列任何一項動作：
    
      - 若要對於所有 Lync Server 使用者全域啟用整合連絡人存放區，請在命令列中輸入：
        
            Set-CsUserServicesPolicy -Identity global -UcsAllowed $True
    
      - 若要對特定網站的使用者啟用整合連絡人存放區，請在命令列中輸入：
        
            New-CsUserServicesPolicy -Identity site:<site name> -UcsAllowed $True
        
        例如：
        
            New-CsUserServicesPolicy -Identity site:Redmond -UcsAllowed $True
    
      - 若要依承租人啟用整合連絡人存放區，請在命令列中輸入：
        
            Set-CsUserServicesPolicy -Tenant <tenantId> -UcsAllowed $True
        
        例如：
        
            Set-CsUserServicesPolicy -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308" -UcsAllowed $True
    
      - 若要對特定使用者啟用整合連絡人存放區，請在命令列中輸入：
        
            New-CsUserServicesPolicy -Identity "<policy name>" -UcsAllowed $True
            Grant-CsUserServicesPolicy -Identity "<user display name>" -PolicyName <"policy name">
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>您也可以使用使用者別名或 SIP URI，而不使用使用者顯示名稱。</td>
        </tr>
        </tbody>
        </table>
        
        例如：
        
            New-CsUserServicesPolicy -Identity "UCS Enabled Users" -UcsAllowed $True
            Grant-CsUserServicesPolicy -Identity "Ken Myer" -PolicyName "UCS Enabled Users"
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>在上一個範例中，第一個命令建立名稱為「UCS 已啟用使用者」 的新個別使用者原則，而且將 UcsAllowed 旗標設定為 True。第二個指令將該原則指派給顯示名稱為 Ken Myer 的使用者，這表示目前已針對 Ken Myer 啟用整合連絡人存放區。</td>
        </tr>
        </tbody>
        </table>

