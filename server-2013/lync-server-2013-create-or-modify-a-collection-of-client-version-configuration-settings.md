---
title: 建立或修改用戶端版本組態設定的集合
TOCTitle: 建立或修改用戶端版本組態設定的集合
ms:assetid: 4e6faffd-a36f-40f1-8734-78d84b7df921
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ898477(v=OCS.15)
ms:contentKeyID: 52056124
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改用戶端版本組態設定的集合

 

_**上次修改主題的時間：** 2013-02-23_

用戶端版本組態設定可用來開啟或關閉用戶端版本控制。全域用戶端版本設定會隨 Lync Server 一併安裝，並用於啟用或停用整個伺服器部署的用戶端版本控制。您也可以針對個別網站設定用戶端版本組態設定。您可以從 Lync Server 2013 控制台或 Lync Server 2013 管理命令介面，建立或修改用戶端版本組態設定。

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


## 使用 Lync Server 控制台建立或修改用戶端版本組態設定

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列，按一下 \[用戶端\]，然後按一下 \[用戶端版本設定\] 導覽按鈕。

4.  在「用戶端版本設定」頁面上，執行下列動作：
    
      - 若要建立新的設定，請按一下 \[新增\]，選取網站，接著按一下 \[確定\]，然後更新設定。
    
      - 若要修改設定，請選取設定，依序按一下 \[編輯\] 和 \[顯示詳細資料\]，然後變更設定。

## 使用 Windows PowerShell Cmdlet 建立或修改用戶端版本組態設定

您可以使用 **New-CsClientVersionConfiguration** Cmdlet 建立用戶端版本組態設定，或使用 **Set-CsClientVersionConfiguration** Cmdlet 進行修改。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行這些 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 建立新的用戶端版本組態設定集合

  - 下列命令會建立套用至 Redmond 網站的新用戶端版本組態設定集合。此範例會停用 Redmond 網站的用戶端版本設定。
    
        New-CsClientVersionConfiguration -Identity "site:Redmond" -Enabled $False

## 啟用網站的用戶端版本設定

  - 此命令會啟用 Redmond 網站的用戶端版本設定。
    
        Set-CsClientVersionConfiguration -Identity "site:Redmond" -Enabled $True

## 停用全組織的用戶端版本設定

  - 此範例會針對組織中所有使用中的用戶端版本組態設定，停用用戶端版本設定。
    
        Get-CsClientVersionConfiguration | Set-CsClientVersionConfiguration  -Enabled $False

如需詳細資訊，請參閱＜[New-CsClientVersionConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientVersionConfiguration)＞和＜[Set-CsClientVersionConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientVersionConfiguration)＞ Cmdlet 的說明主題。

