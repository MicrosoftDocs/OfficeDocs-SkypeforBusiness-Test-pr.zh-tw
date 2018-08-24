---
title: 重設裝置更新規則
TOCTitle: 重設裝置更新規則
ms:assetid: d1f597e7-dffd-4756-af07-10613a5d8729
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994069(v=OCS.15)
ms:contentKeyID: 52056227
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 重設裝置更新規則

 

_**上次修改主題的時間：** 2013-02-23_

如果您不喜歡更新在測試裝置上的運行方式，您可以重新設定裝置更新規則，其會移除規則的擱置狀態並從測試裝置解除安裝更新。

您可以使用 Lync Server 控制台或 Windows PowerShell 移除裝置更新規則。

> [!NOTE]  
> 若要解除安裝已經您核准的規則 (即已部署的規則)，請將其還原。如需詳細資訊，請參閱＜<a href="lync-server-2013-restore-a-device-update-rule.md">還原裝置更新規則</a>＞。



## 使用 Lync Server 控制台重設裝置更新規則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列，按一下 \[用戶端\]，然後按一下 \[裝置更新\] 導覽按鈕。

4.  在「裝置更新」頁面中，執行下列其中一項動作：
    
      - 若要重設規則，請選取您要加以重設的規則。
    
      - 若要重設所有規則，請在 \[編輯\] 功能表，按一下 \[全選\]。
    
      - 若要重設某個品牌的所有規則，請使用 \[Brand\] 欄功能表。

5.  按一下 \[動作\]，然後按一下 \[取消擱置更新\]。
    
    > [!TIP]
    > 如果您確定不會再部署所取消的裝置更新，您可能會想要予以刪除。如需詳細資訊，請參閱＜<a href="lync-server-2013-remove-a-device-update-rule.md">移除裝置更新規則</a>＞。


## 使用 Windows PowerShell Cmdlet 重設裝置更新規則

可使用 Windows PowerShell 和 **Reset-CsDeviceUpdateRule** Cmdlet 重設裝置更新規則。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。

> [!NOTE]  
> 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</a>。



## 在伺服器上重設特定裝置更新規則

  - 下列命令可在 Web 伺服器 atl-cs-001.litwareinc.com 上重設裝置更新規則 d5ce3c10-2588-420a-82ac-dc2d9b1222ff9：
    
        Reset-CsDeviceUpdateRule -Identity "service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9"

## 在伺服器上重設所有裝置更新規則

  - 此命令會在 Web 伺服器 atl-cs-001.litwareinc.com 上重設所有裝置更新規則：
    
        Get-CsDeviceUpdateRule -Filter "service:WebServer:atl-cs-001.litwareinc.com*"  | Reset-CsDeviceUpdateRule

## 重設所有具有特定品牌的裝置更新規則

  - 在此範例中，組織所有 Brand 等於 Microsoft 的裝置更新會重設為：
    
        Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "Microsoft"} | Reset-CsDeviceUpdateRule

如需詳細資訊，請參閱＜[Reset-CsDeviceUpdateRule](https://docs.microsoft.com/en-us/powershell/module/skype/Reset-CsDeviceUpdateRule)＞ Cmdlet 的說明主題。

## 請參閱

#### 工作

[核准裝置更新規則](lync-server-2013-approve-a-device-update-rule.md)

