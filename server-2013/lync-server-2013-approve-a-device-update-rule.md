---
title: 核准裝置更新規則
TOCTitle: 核准裝置更新規則
ms:assetid: 9dbb1c9a-be0f-4e13-9234-05501ab43ac5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994053(v=OCS.15)
ms:contentKeyID: 52056197
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 核准裝置更新規則

 

_**上次修改主題的時間：** 2013-02-23_

匯入裝置更新規則之後，會安裝在您的測試裝置上。如果測試成功，而且您希望部署更新至組織中，請使用 Lync Server 控制台或 Windows PowerShell 來核准。

## 使用 Lync Server 控制台核准裝置更新規則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在「裝置更新」頁面中，執行下列其中一項動作：
    
      - 若要核准一個規則，請選取該規則。
    
      - 若要核准所有規則，請按一下 \[編輯\]，然後按一下 \[全選\]。

4.  按一下 \[動作\]，然後按一下 \[核准\]。

## 使用 Windows PowerShell Cmdlet 核准裝置更新規則

裝置更新規則僅可使用 Windows PowerShell 和 **Approve-CsDeviceUpdateRule** Cmdlet 來核准。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。

> [!NOTE]  
> 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</a>。



## 核准單一裝置更新規則

  - 下列命令核准在 Web 伺服器 atl-cs-001.litwareinc.com 上找到的裝置更新規則 d5ce3c10-2588-420a-82ac-dc2d9b1222ff9：
    
        Approve-CsDeviceUpdateRule -Identity service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9

## 核准多個裝置更新規則

  - 此命令核准 Microsoft 品牌裝置的所有裝置更新規則：
    
        Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "Microsoft"} | Approve-CsDeviceUpdateRule

如需詳細資訊，請參閱＜[Approve-CsDeviceUpdateRule](https://docs.microsoft.com/en-us/powershell/module/skype/Approve-CsDeviceUpdateRule)＞ Cmdlet 的說明主題。

## 請參閱

#### 工作

[匯入裝置更新規則](lync-server-2013-import-device-update-rules.md)  
[還原裝置更新規則](lync-server-2013-restore-a-device-update-rule.md)

