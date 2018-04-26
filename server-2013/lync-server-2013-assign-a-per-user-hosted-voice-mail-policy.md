---
title: 指派每位使用者的主控語音信箱原則
TOCTitle: 指派每位使用者的主控語音信箱原則
ms:assetid: d44c71a0-4407-4ab4-b7e0-d671dde3425f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398919(v=OCS.15)
ms:contentKeyID: 49292438
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指派每位使用者的主控語音信箱原則

 

_**上次修改主題的時間：** 2010-11-07_

您可以選擇部署一個或多個個別使用者裝載語音信箱原則。如果您有部署個別使用者原則，就必須明確地將其指派給使用者、群組或連絡人物件。

如需指派或移除個別使用者裝載語音信箱原則之指派的詳細資訊，請參閱 Lync Server 管理命令介面文件中的下列 Cmdlet：

  - Grant-CsHostedVoicemailPolicy

  - Remove-CsHostedVoicemailPolicy

## 若要指派個別使用者裝載語音信箱原則

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 Grant-CsHostedVoicemailPolicy Cmdlet，以將個別使用者裝載語音信箱原則指派給個別使用者、群組和連絡人物件。例如，執行：
    
        Grant-CsHostedVoicemailPolicy -Identity "Ken Myer" -PolicyName ExRedmond
    
    此範例會將 ExRedmond 裝載語音信箱原則指派給使用者 Ken Myer。
    
    **Identity** 會指定要修改的使用者帳戶。Identity 值可以使用下列任何格式來指定：
    
      - 使用者的 SIP 位址
    
      - 使用者的 Active Directory 使用者主體名稱
    
      - 使用者的網域\\登入名稱 (例如，contoso\\kenmyer)
    
      - 使用者的 Active Directory 網域服務顯示名稱 (例如，Ken Myer)。如果使用顯示名稱做為 Identity 值，您可以使用星號 (\*) 萬用字元。例如，若 Identity 為 "\* Smith"，則會傳回所有顯示名稱結尾為字串值 " Smith" 的使用者。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>使用者的 Active Directory SAM 帳戶名稱無法當做 Identity 值使用，因為 SAM 帳戶名稱在樹系中不一定是唯一的。</td>
    </tr>
    </tbody>
    </table>

