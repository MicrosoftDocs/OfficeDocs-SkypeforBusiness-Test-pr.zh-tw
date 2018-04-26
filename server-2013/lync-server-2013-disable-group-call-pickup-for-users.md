---
title: 停用使用者的群組來電接聽
TOCTitle: 停用使用者的群組來電接聽
ms:assetid: 91b06f9e-2840-45a2-bbb3-6a29179b9a9f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945638(v=OCS.15)
ms:contentKeyID: 52056192
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 停用使用者的群組來電接聽

 

_**上次修改主題的時間：** 2013-01-30_

使用下列程序為使用者停用群組來電接聽。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您為使用者停用群組來電接聽時，不會保留指派給使用者的來電接聽群組號碼。如果您後續想要為使用者重新啟用群組來電接聽，則必須以 /enablegrouppickup 參數重新指派來電接聽群組號碼。</td>
</tr>
</tbody>
</table>


## 停用使用者的群組來電接聽

1.  以系統管理員權限登入已安裝 SEFAUtil 工具的電腦。

2.  請在命令列執行：
    
        SEFAUtil.exe sip:<sip address of user> /server:<pool FQDN> /disablegrouppickup
    
    例如：
    
        SEFAUtil.exe katarina@contoso.com /server:pool01.contoso.com /disablegrouppickup

## 請參閱

#### 工作

[指派群組來電接聽號碼給使用者](lync-server-2013-assign-group-call-pickup-numbers-to-users.md)  
[啟用使用者的群組來電接聽](lync-server-2013-enable-group-call-pickup-for-users.md)

