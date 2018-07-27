---
title: 指派群組來電接聽號碼給使用者
TOCTitle: 指派群組來電接聽號碼給使用者
ms:assetid: b8e79275-8e7e-4799-b908-f34f61df22f0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945647(v=OCS.15)
ms:contentKeyID: 52056187
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指派群組來電接聽號碼給使用者

 

_**上次修改主題的時間：** 2013-01-30_

將群組來電接聽群組號碼新增至通話駐留範圍表後，您可以將群組指派給使用者。使用次要副檔名功能啟用 (SEFAUtil ) Resource Kit 工具以將來電接聽指派給使用者。

> [!NOTE]  
> 在混合部署中，請勿將群組來電接聽群組指派給在家上網的使用者。在家上網的使用者無法參與群組來電接聽，因為其他使用者無法接聽他們的來電，而他們也無法接聽其他使用者的來電。



## 將群組來電接聽群組指派給使用者

1.  以系統管理員權限登入已安裝 SEFAUtil 工具的電腦。

2.  請在命令列執行：
    
        SEFAUtil.exe sip:<sip address of user> /server:<pool FQDN> /enablegrouppickup:<group number>
    
    例如：
    
        SEFAUtil.exe katarina@contoso.com /server:pool01.contoso.com /enablegrouppickup:199

## 請參閱

#### 工作

[啟用使用者的群組來電接聽](lync-server-2013-enable-group-call-pickup-for-users.md)  
[停用使用者的群組來電接聽](lync-server-2013-disable-group-call-pickup-for-users.md)

