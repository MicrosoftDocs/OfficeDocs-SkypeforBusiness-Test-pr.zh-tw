---
title: 檢視用戶端版本組態設定
TOCTitle: 檢視用戶端版本組態設定
ms:assetid: c72df4e6-a889-4cb6-86f7-8334d7774c6e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ923062(v=OCS.15)
ms:contentKeyID: 52056222
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視用戶端版本組態設定

 

_**上次修改主題的時間：** 2013-02-23_

用戶端版本組態設定可用來開啟或關閉用戶端版本控制。全域用戶端版本設定會隨 Lync Server 2013 一併安裝，並用於啟用或停用整個伺服器部署的用戶端版本控制。啟用全域設定時，任何既有的用戶端版本原則都會在使用者嘗試登入時生效。您可從 Lync Server 2013 控制台或 Lync Server 2013 管理命令介面 檢視用戶端版本組態設定。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由於匿名使用者不會與使用者、網站或服務相關聯，因此匿名使用者只會受全域層級原則的影響。</td>
</tr>
</tbody>
</table>


## 使用 Lync Server 控制台 檢視用戶端版本組態設定

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列，按一下 \[用戶端\]，然後按一下 \[用戶端版本設定\] 導覽按鈕。

4.  按兩下您要檢視的用戶端版本設定名稱。

## 使用 Windows PowerShell Cmdlet 檢視用戶端版本組態設定

您可使用 **Get-CsClientVersionConfiguration** Cmdlet 檢視用戶端版本組態設定。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視用戶端版本設定資訊

  - 若要檢視有關您所有用戶端版本組態設定的資訊，請在 Lync Server 管理命令介面中輸入下列命令然後按 ENTER：
    
        Get-CsClientVersionConfiguration
    
    隨即傳回類似下列的資訊：
    
        Identity      : Global
        DefaultAction : Allow
        DefaultURL    :
        Enabled       : True

如需詳細資訊，請參閱＜[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)＞ Cmdlet 的說明主題。

