---
title: 檢視電話撥入式會議存取號碼
TOCTitle: 檢視電話撥入式會議存取號碼
ms:assetid: 41a7dfb4-0c89-4650-b61b-0e1bf875c62b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688037(v=OCS.15)
ms:contentKeyID: 49890038
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視電話撥入式會議存取號碼

 

_**上次修改主題的時間：** 2013-02-23_

您在 Lync Server 2013 控制台中提供撥入存取號碼給使用者，讓使用者能夠從外部加入會議。

## 檢視撥入存取號碼

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[會議\]**，然後按一下 **\[撥入存取號碼\]**。

4.  在 **\[撥入存取號碼\]** 頁面中，按一下要檢視的存取號碼。

5.  在 **\[編輯\]** 中，選取 **\[顯示詳細資料...\]** 核取方塊。

## 使用 Lync Server PowerShell Cmdlet 檢視電話撥入式會議存取號碼

也可使用 Lync Server PowerShell 和 Get-CsDialInConferencingAccessNumber Cmdlet 檢視電話撥入式會議存取號碼。此 Cmdlet 可以從 Lync Server 2013 管理命令介面或 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視 SIP 主幹組態資訊

  - 若要檢視所有電話撥入式會議存取號碼的相關資訊，請在 Lync Server 管理命令介面中輸入下列命令，然後按 ENTER 鍵：
    
        Get-CsDialInConferencingAccessNumber
    
    便會傳回像這樣的資訊：
    
        Identity           : CN={20ca8dc8-5ff8-41f4-b5bb-22ba9972ae2e},
                             CN=Application Contacts,CN=RTCService=Services,
                             CN=Configuration,DC=litwareinc,DC=com
        PrimaryUri         : sip:testnumber@litwareinc.com
        DisplayName        : Test
        DisplayNumber      : 1-425-555-1019
        LineUri            : tel:+14255551019
        PrimaryLanguage    : en-US
        SecondaryLanguages : {}
        Pool               : atl-cs-001.litwareinc.com
        HostingProvider    :
        Regions            : {US}

如需詳細資訊，請參閱 [Get-CsDialInConferencingAccessNumber](get-csdialinconferencingaccessnumber.md) Cmdlet 的說明主題。

