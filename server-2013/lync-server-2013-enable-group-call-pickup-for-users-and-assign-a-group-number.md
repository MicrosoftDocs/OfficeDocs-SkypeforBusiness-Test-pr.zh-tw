---
title: 啟用使用者的群組來電接聽並指派群組號碼
TOCTitle: 啟用使用者的群組來電接聽並指派群組號碼
ms:assetid: c33bb6c2-d43b-4fb6-a0fa-6d82a7b09abe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945650(v=OCS.15)
ms:contentKeyID: 52056193
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用使用者的群組來電接聽並指派群組號碼

 

_**上次修改主題的時間：** 2013-01-30_

將電話接聽群組成員新增至通話駐留範圍表後，您可將群組成員指派給使用者並為他們啟用群組來電接聽。使用次要分機功能啟用 (SEFAUtil) Resource Kit 工具以指派群組成員並啟用群組來電接聽。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在混合部署中，請勿將群組來電接聽群組指派給位於線上的使用者。位於線上的使用者無法參與群組來電接聽，意即其他使用者無法接聽他們的電話，而他們也無法接聽其他使用者的電話。</td>
</tr>
</tbody>
</table>


## 指派群組號碼並為使用者啟用群組來電接聽

1.  以系統管理員權限登入已安裝 SEFAUtil 工具的電腦。

2.  請在命令列執行：
    
        SEFAUtil.exe sip:<sip address of user> /server:<pool FQDN> /enablegrouppickup:<group number>
    
    例如，將群組號碼 199 指派給使用者：
    
        SEFAUtil.exe katarina@contoso.com /server:pool01.contoso.com /enablegrouppickup:199 

## 請參閱

#### 工作

[停用使用者的群組來電接聽](lync-server-2013-disable-group-call-pickup-for-users.md)

