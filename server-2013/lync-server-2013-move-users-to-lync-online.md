---
title: Lync Server 2013：將使用者移至 Lync Online
TOCTitle: 將使用者移至 Lync Online
ms:assetid: 6a523c86-2eac-4fa4-973a-4406872c9a7d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204969(v=OCS.15)
ms:contentKeyID: 49291208
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將使用者移至 Lync Online

 

_**上次修改主題的時間：** 2014-05-29_

您開始將使用者移轉至 Lync Online 前，應先備份所要移動之帳戶相關聯的使用者資料。並非所有使用者資料都會與使用者帳戶一併移動。如需相關資訊，請參閱 [備份和還原需求：資料](lync-server-2013-backup-and-restoration-requirements-data.md)。

## 將使用者設定移轉至 Lync Online

使用者設定會與使用者帳戶一起移動。某些內部部署設定不會與使用者帳戶一起移動。

## 將試驗使用者移至 Lync Online

開始將使用者移至 Lync Online 之前，您可能會想要移動一些試驗使用者以確認您的環境已正確設定。接著可確認 Lync 功能與服務函數是否如預期般運作，然後再嘗試移動其他使用者。

若要將內部部署使用者移至 商務用 Skype Online 租用戶，請使用 Microsoft Office 365 租用戶的管理員認證，在 Lync Server 管理命令介面中執行下列 Cmdlet。利用您想要移動的使用者資訊取代 "username@contoso.com"。

```
$creds=Get-Credential
```

```
Move-CsUser -Identity username@contoso.com -Target sipfed.online.lync.com -Credential $creds -HostedMigrationOverrideUrl <URL>
```

為 **HostedMigrationOverrideUrl** 參數指定的 URL 格式必須是正在執行裝載移轉服務之集區的 URL，格式如下：*Https://\<Pool FQDN\>/HostedMigration/hostedmigrationService.svc*。

您可以檢視 Office 365 租用戶帳戶的 Lync Online 控制台 URL，以判定裝載移轉服務的 URL。

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

## 將使用者移至 Lync Online

若要移動多位使用者，請使用 [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser) Cmdlet 搭配 –Filter 參數，以選取使用者帳戶有獲指派特定屬性的使用者，例如 RegistrarPool。接著，您可以將傳回的使用者結果輸送至 [Move-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Move-CsUser) Cmdlet，如以下範例所示。

    Get-CsUser -Filter {UserProperty -eq "UserPropertyValue"} | Move-CsUser -Target sipfed.online.lync.com -Credential $creds -HostedMigrationOverrideUrl <URL>

您也可以使用 –OU 參數以擷取特定 OU 中的所有使用者，如下例所示。

    Get-CsUser -OU "cn=hybridusers,cn=contoso.." | Move-CsUser -Target sipfed.online.lync.com -Credentials $creds -HostedMigrationOverrideUrl <URL>

## 確認 Lync Online 使用者設定與功能

您可以透過下列方式確認使用者是否移動成功：

  - 在 Lync Online 控制台檢視使用者的狀態。內部部署使用者與線上使用者的視覺化指標不同。

  - 執行下列 Cmdlet：
    
        Get-CsUser -Identity

