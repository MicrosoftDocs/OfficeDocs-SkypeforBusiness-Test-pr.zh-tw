---
title: Lync Server 2013：管理混合部署中的使用者
TOCTitle: 管理混合部署中的使用者
ms:assetid: 6924ed7b-30a9-4be7-b952-90655625f2c8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204967(v=OCS.15)
ms:contentKeyID: 49291194
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理 Lync Server 2013 混合部署中的使用者

 

_**上次修改主題的時間：** 2014-05-29_

您可以使用 Microsoft Office 365 線上入口網站提供的使用者管理功能，為移轉至 Lync Online 的使用者管理使用者設定與原則。您必須使用您的租用戶系統管理員帳戶登入，才可執行系統管理工作。

## 將使用者移回內部部署

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本節僅適用於針對 Lync 內部部署所建立並啟用後移至 Lync Online 的使用者。若要移動建立於 Lync Online (且尚未在內部部署中啟用 Lync) 的使用者，請參閱 <a href="lync-server-2013-moving-users-from-lync-online-to-lync-on-premises.md">將使用者從 Lync Online 移至 Lync Server 2013 的 Lync 內部部署</a>。</td>
</tr>
</tbody>
</table>


  - 執行下列 Cmdlet，將使用者從 Lync Online 移回 Lync 內部部署：
    
        $cred=Get-Credential
    
        Move-CsUser -Identity username@contoso.com -Target localpool.contoso.com -Credential $cred -HostedMigrationOverrideUrl <URL>

專用於 **HostedMigrationOverrideUrl** 參數的 URL 格式必須是正在執行裝載移轉服務之集區的 URL，格式如下：

*Https://\<Pool FQDN\>/HostedMigration/hostedmigrationService.svc*。您可以檢視 Office 365 租用戶帳戶的 Lync Online 控制台 URL，以判定裝載移轉服務的 URL。

**決定 Office 365 租用戶的代管移轉服務 URL**

1.  以系統管理員身分登入 Office 365 租用戶。

2.  開啟 **Lync 系統管理中心** 。

3.  顯示 **Lync 系統管理中心** 之後，在位址列中選取並複製 URL **lync.com**。範例 URL 看起來應該像以下這樣：
    
    `https://webdir0a.online.lync.com/lscp/?language=en-US&tenantID=`

4.  將 URL 中的 **webdir** 取代為 **admin**，產生下列結果：
    
    `https://admin0a.online.lync.com`

5.  將下列字串附加至 URL： **/HostedMigration/hostedmigrationservice.svc**。
    
    產生的 URL，其為 **HostedMigrationOverrideUrl** 的值，應該如下所示：
    
    `https://admin0a.online.lync.com/HostedMigration/hostedmigrationservice.svc`

