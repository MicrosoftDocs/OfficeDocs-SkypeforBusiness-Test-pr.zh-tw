---
title: 移除裝置更新規則
TOCTitle: 移除裝置更新規則
ms:assetid: ad6e0c6a-cda4-4147-92d5-48bc393ac456
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994066(v=OCS.15)
ms:contentKeyID: 52056181
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除裝置更新規則

 

_**上次修改主題的時間：** 2013-02-23_

移除裝置更新規則會將其永遠移出裝置更新佇列。

移除規則與在部署中的裝置或從測試裝置中解除安裝更新有所不同。若要從部署中解除安裝已核准的更新，請還原裝置更新規則。如需詳細資訊，請參閱＜[還原裝置更新規則](lync-server-2013-restore-a-device-update-rule.md)＞。若要解除安裝尚未從測試裝置核准的更新，請重新設定。如需詳細資訊，請參閱＜[重設裝置更新規則](lync-server-2013-reset-a-device-update-rule.md)＞。

您可以使用 Lync Server 控制台或 Windows PowerShell 移除裝置更新規則。

## 使用 Lync Server 控制台移除裝置更新規則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列，按一下 \[用戶端\]，然後按一下 \[裝置更新\] 導覽按鈕。

4.  在「裝置更新」頁面中，執行下列其中一項動作：
    
      - 若要移除一項規則，請選取您要刪除的規則。
    
      - 若要移除所有規則，請按一下 \[編輯\]，然後按一下 \[全選\]。

5.  按一下 \[編輯\]，然後按一下 \[刪除\]。

## 使用 Windows PowerShell Cmdlet 移除裝置更新規則

裝置更新規則僅可使用 Windows PowerShell 和 **Remove-CsDeviceUpdateRule** Cmdlet 來移除。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 將單一裝置更新規則從伺服器移除

  - 下列命令會將裝置更新規則 d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 從 atl-cs-001.litwareinc.com 上的 Web 伺服器移除。
    
        Remove-CsDeviceUpdateRule -Identity "service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9"

## 將所有裝置更新規則從伺服器移除

  - 此命令會將所有裝置更新規則從 atl-cs-001.litwareinc.com 上的 Web 伺服器移除。
    
        Get-CsDeviceUpdateRule -Filter "service:WebServer:atl-cs-001.litwareinc.com*" | Remove-CsDeviceUpdateRule

如需詳細資訊，請參閱＜[Remove-CsDeviceUpdateRule](remove-csdeviceupdaterule.md)＞ Cmdlet 的說明主題。

## 請參閱

#### 工作

[核准裝置更新規則](lync-server-2013-approve-a-device-update-rule.md)

