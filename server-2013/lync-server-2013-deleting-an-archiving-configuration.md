---
title: 刪除封存設定
TOCTitle: 刪除封存設定
ms:assetid: a8744d39-5cf2-474c-9a99-a0f3a37f846f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205167(v=OCS.15)
ms:contentKeyID: 49291933
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除封存設定

 

_**上次修改主題的時間：** 2013-02-23_

您可以刪除網站組態或集區組態，但無法移除全域組態。如果您刪除全域組態，全域組態就會自動重設為預設值。如需如何實作封存組態 (包含可以指定哪些選項以及封存組態的階層) 的詳細資訊，請參閱規劃文件、部署文件或作業文件中的＜[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)＞。

## 刪除網站或集區組態進行封存

1.  使用指派給 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存組態\]。

4.  在封存組態清單中，依序按一下您要刪除的網站或集區組態、\[編輯\] 和 \[刪除\]。

5.  按一下 \[認可\]。

## 使用 Lync Server 管理命令介面 Cmdlet 移除封存組態設定

使用 Windows PowerShell 和 Remove-CsArchivingConfiguration Cmdlet 也可以刪除封存組態設定。此 Cmdlet 可以從 Lync Server 2013 管理命令介面 或從 Windows PowerShell 的遠端工作階段執行。如需關於使用遠端 Windows PowerShell 的詳細資訊。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 移除指定的封存組態設定集合

  - 下列命令會移除已套用至 Redmond 網站的封存組態設定：
    
        Remove-CsArchivingConfiguration -Identity "site:Redmond"

## 移除已套用到網站範圍的所有封存組態設定

  - 此命令會移除已套用至服務範圍的所有封存組態設定：
    
        Get-CsArchivingConfiguration -Filter "site:*" | Remove-CsArchivingConfiguration

## 根據指定的內容值移除封存組態設定

  - 此命令會移除已停用 Exchange 封存功能的所有封存組態設定：
    
        Get-CsArchivingConfiguration | Where-Object {$_.EnableExchangeArchiving -eq $False} | Remove-CsArchivingConfiguration

如需詳細資訊，請參閱 [Remove-CsArchivingConfiguration](remove-csarchivingconfiguration.md) Cmdlet 的說明主題。

## 請參閱

#### 概念

[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)  

#### 其他資源

[在 Lync Server 2013 中管理內部與外部通訊的封存](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md)

