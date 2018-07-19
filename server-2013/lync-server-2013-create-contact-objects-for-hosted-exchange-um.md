---
title: Lync Server 2013：建立主控 Exchange UM 的聯絡人物件
TOCTitle: 建立主控 Exchange UM 的聯絡人物件
ms:assetid: a39be52f-488a-4523-ad5f-ce1f0d681959
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412765(v=OCS.15)
ms:contentKeyID: 49291885
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立主控 Exchange UM 的聯絡人物件

 

_**上次修改主題的時間：** 2012-09-24_

下列程序說明如何為裝載的 Exchange Unified Messaging (UM) 建立自動語音應答 (AA) 或訂戶存取 (SA) 連絡人物件。

如需詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的主控 Exchange 聯絡人物件管理](lync-server-2013-hosted-exchange-contact-object-management.md)＞。

如需設定連絡人物件的詳細資訊，請參閱 Lync Server 管理命令介面文件中的下列 Cmdlet：

  - [New-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsExUmContact)

  - [Set-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsExUmContact)

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在您可以為裝載的 Exchange UM 啟用 Lync Server 2013 連絡人物件之前，必須先部署適用於這些物件的裝載語音信箱原則。如需詳細資訊，請參閱＜ <a href="lync-server-2013-hosted-voice-mail-policies.md">Lync Server 2013 中的主控語音信箱原則</a>＞。</td>
</tr>
</tbody>
</table>


## 若要為裝載的 Exchange UM 建立 AA 或 SA 連絡人物件

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 New-CsExUmContact Cmdlet 建立部署所需的任何連絡人物件。例如，執行下列命令建立 AA 和 SA 連絡人物件：
    
        New-CsExUmContact -SipAddress "sip:exumaa1@fabrikam.com" -RegistrarPool "RedmondPool.litwareinc.com" -OU "HostedExUM Integration" -DisplayNumber "+14255550101" -AutoAttendant $True
    
        New-CsExUmContact -SipAddress "sip:exumsa1@fabrikam.com" -RegistrarPool "RedmondPool.litwareinc.com" -OU "HostedExUM Integration" -DisplayNumber "+14255550101"
    
    這些範例會設定下列參數：
    
      - **SipAddress** 指定連絡人物件的 SIP 位址。這個位址必須是未在 Active Directory 網域服務中用於設定使用者或連絡人物件的位址。這個值的格式必須為 「sip:\<*SIP 位址* \>」，如上面的範例中所示。
    
      - **RegistrarPool** 指定登錄器服務執行所在集區的完整網域名稱 (FQDN)。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>在 Lync Server 2013 之前，Exchange UM 連絡人物件無法移至屬於 Lync Server 2013 部署的集區中。</td>
        </tr>
        </tbody>
        </table>
    
      - **OU** 指定將要放置這個連絡人物件所在的 Active Directory 組織單位。
    
      - **DisplayNumber** 指定連絡人物件的電話號碼。每個連絡人物件的電話號碼都必須是唯一的。
    
      - **AutoAttendant** 指定連絡人物件是否為自動語音應答。自動語音應答會提供一組語音提示，讓來電者瀏覽電話系統並且連絡上想要連絡的通話方。若此參數的值為 **False** (預設)，表示為訂戶存取連絡人物件。

