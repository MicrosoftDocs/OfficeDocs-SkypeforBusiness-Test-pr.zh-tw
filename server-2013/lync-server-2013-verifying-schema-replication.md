---
title: Lync Server 2013：驗證結構描述複寫
TOCTitle: 驗證結構描述複寫
ms:assetid: ad01a7cf-aa79-4648-ba5a-a7a09172db36
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412822(v=OCS.15)
ms:contentKeyID: 49291971
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中驗證 Active Directory 結構描述複寫

 

_**上次修改主題的時間：** 2012-10-29_

請手動驗證架構分割已複寫，再執行樹系準備。

## 若要手動驗證架構複寫

1.  以 Enterprise Admins 群組成員的身分，登入網域控制站。

2.  依序按一下 **\[開始\]** 、 **\[系統管理工具\]** 和 **\[ADSI 編輯器\]** ，以開啟 \[ADSI 編輯器\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>或者，也可以從命令列執行 <strong>adsiedit.msc</strong> 。</td>
    </tr>
    </tbody>
    </table>


3.  在 Microsoft Management Console (MMC) 樹狀目錄中按一下 **\[ADSI 編輯器\]** (若尚未選取)。

4.  在 **\[執行\]** 功能表上，按一下 **\[連線到\]** 。

5.  在 **\[選取熟知的命名內容\]** 的 **\[連線設定\]** 對話方塊中，選取 **\[架構\]** ，然後按一下 \[確定\] 。

6.  在架構容器下，搜尋 CN=ms-RTC-SIP-SchemaVersion。如果此物件存在，且 **rangeUpper** 屬性值為 1150、 **rangeLower** 屬性值為 3，便是已成功更新且複寫了架構。如果此物件不存在，或是 **rangeUpper** 和 **rangeLower** 屬性值不等於指定的值，則架構尚未經過修改或複寫。

## 請參閱

#### 工作

[在 Lync Server 2013 中執行 Active Directory 架構準備](lync-server-2013-running-schema-preparation.md)  

#### 概念

[在 Lync Server 2013 中準備 Active Directory 結構描述](lync-server-2013-preparing-the-active-directory-schema.md)

