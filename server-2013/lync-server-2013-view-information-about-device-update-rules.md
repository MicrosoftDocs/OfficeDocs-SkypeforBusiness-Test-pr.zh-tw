---
title: 檢視裝置更新規則的資訊
TOCTitle: 檢視裝置更新規則的資訊
ms:assetid: d6677ca4-024b-4816-8511-8d7630788107
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994077(v=OCS.15)
ms:contentKeyID: 52056229
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視裝置更新規則的資訊

 

_**上次修改主題的時間：** 2013-02-23_

檢視有關已匯入之裝置更新規則的詳細資訊，包括更新所適用的類型、模式和裝置品牌；更新的版本和類型；以及更新的地區設定和集區。資訊可用於所有已匯入的裝置更新規則，這些規則為等待核准的、已部署 (已核准) 的、已回復 (已還原) 的，以及您決定不使用 (重設) 的規則。從 Lync Server 控制台或 Windows PowerShell 存取此資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需如何匯入、核准、重設、還原以及移除規則的詳細資訊，請參閱列於＜<a href="lync-server-2013-device-update-rules.md">Lync Server 2013 中的裝置更新規則</a>＞中的主題。</td>
</tr>
</tbody>
</table>


## 使用 Lync Server 控制台檢視裝置更新規則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列，按一下 \[用戶端\]，然後按一下 \[裝置更新\] 導覽按鈕。匯入的規則會列於「裝置更新」頁面上。

## 使用 Windows PowerShell Cmdlet 檢視裝置更新規則

亦可使用 Windows PowerShell 和 **Get-CsDeviceUpdateRule** Cmdlet 檢視所有裝置更新的詳細資訊。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</a>。</td>
</tr>
</tbody>
</table>


## 檢視所有裝置更新規則

  - 下列命令會傳回設定供組織使用之所有裝置更新規則的詳細資訊：
    
        Get-CsDeviceUpdateRule
    
    命令會傳回類似下列的每項裝置更新規則資訊：
    
        Identity        : Service:WebServer:pool0.vdomain.com/2de8cbf6-9441-4f61-b755-1e4bef1effde
        Id              : 2de8cbf6-9441-4f61-b755-1e4bef1effde
        DeviceType      : UCPhone
        Brand           : Microsoft
        Model           : CPE
        Revision        : A
        Locale          : ENU
        UpdateType      : CPE
        ApprovedVersion :
        RestoreVersion  :
        PendingVersion  : 4.0.7577.4066

## 檢視特定 Web 伺服器上的所有裝置更新規則

  - 若要檢視特定電腦上的裝置更新規則，請使用伺服器身分識別碼後的 Filter 參數和萬用字元 (\*)。例如：
    
        Get-CsDeviceUpdateRule -Filter "service:WebServer:atl-cs-001.litwareinc.com*"

如需詳細資訊，請參閱 [Get-CsDeviceUpdateRule](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsDeviceUpdateRule) Cmdlet 的說明主題。

