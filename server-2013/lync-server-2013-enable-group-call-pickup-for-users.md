---
title: 啟用使用者的群組來電接聽
TOCTitle: 啟用使用者的群組來電接聽
ms:assetid: 20ec5f41-6ba2-4156-82ed-b91d05b62a6d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945620(v=OCS.15)
ms:contentKeyID: 52056065
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用使用者的群組來電接聽

 

_**上次修改主題的時間：** 2013-01-30_

您可使用 SEFAUtil Resource Kit 工具來啟用使用者的群組來電接聽。您必須在通話駐留範圍表中將類型為 GroupPickup 的群組號碼指派給使用者，才能啟用群組來電接聽。執行 SEFAUtil.exe 時使用 /enablegrouppickup 參數，即可指派電話接聽群組號碼並同時啟用群組來電接聽。

## 啟用使用者的群組來電接聽

1.  以系統管理員權限登入已安裝 SEFAUtil 工具的電腦。

2.  請在命令列執行：
    
        SEFAUtil.exe sip:<sip address of user> /server:<pool FQDN> /enablegrouppickup:<group number>
    
    例如：
    
        SEFAUtil.exe katarina@contoso.com /server:pool01.contoso.com /enablegrouppickup:199

## 請參閱

#### 工作

[指派群組來電接聽號碼給使用者](lync-server-2013-assign-group-call-pickup-numbers-to-users.md)  
[停用使用者的群組來電接聽](lync-server-2013-disable-group-call-pickup-for-users.md)

